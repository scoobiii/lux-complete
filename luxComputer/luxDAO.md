// SPDX-License-Identifier: MIT pragma solidity ^0.8.20;

interface ILUXToken { function transferFrom(address from, address to, uint256 value) external returns (bool); function transfer(address to, uint256 value) external returns (bool); function balanceOf(address owner) external view returns (uint256); }

contract LuxDAO { struct Proposal { uint256 id; string description; address recipient; uint256 amount; uint256 votesFor; uint256 votesAgainst; uint256 deadline; bool executed; mapping(address => bool) voted; }

ILUXToken public luxToken;
address public owner;
uint256 public proposalCount;
uint256 public quorum = 1000 * 10**18;
uint256 public votingPeriod = 3 days;

mapping(uint256 => Proposal) public proposals;
mapping(address => bool) public isMember;

event ProposalCreated(uint256 id, string description, address recipient, uint256 amount);
event Voted(uint256 proposalId, address voter, bool support);
event ProposalExecuted(uint256 proposalId, address recipient, uint256 amount);

modifier onlyOwner() {
    require(msg.sender == owner, "Not owner");
    _;
}

modifier onlyMember() {
    require(isMember[msg.sender], "Not a member");
    _;
}

constructor(address _luxToken) {
    luxToken = ILUXToken(_luxToken);
    owner = msg.sender;
    isMember[msg.sender] = true;
}

function joinDAO() external {
    require(luxToken.balanceOf(msg.sender) >= 100 * 10**18, "Min 100 LUX required");
    isMember[msg.sender] = true;
}

function createProposal(string memory _description, address _recipient, uint256 _amount) external onlyMember {
    proposalCount++;
    Proposal storage p = proposals[proposalCount];
    p.id = proposalCount;
    p.description = _description;
    p.recipient = _recipient;
    p.amount = _amount;
    p.deadline = block.timestamp + votingPeriod;

    emit ProposalCreated(proposalCount, _description, _recipient, _amount);
}

function vote(uint256 _id, bool support) external onlyMember {
    Proposal storage p = proposals[_id];
    require(block.timestamp <= p.deadline, "Voting ended");
    require(!p.voted[msg.sender], "Already voted");

    p.voted[msg.sender] = true;
    uint256 weight = luxToken.balanceOf(msg.sender);

    if (support) {
        p.votesFor += weight;
    } else {
        p.votesAgainst += weight;
    }

    emit Voted(_id, msg.sender, support);
}

function executeProposal(uint256 _id) external onlyMember {
    Proposal storage p = proposals[_id];
    require(!p.executed, "Already executed");
    require(block.timestamp > p.deadline, "Voting still open");
    require(p.votesFor >= quorum, "Quorum not met");
    require(p.votesFor > p.votesAgainst, "Not enough support");

    p.executed = true;
    require(luxToken.transfer(p.recipient, p.amount), "Transfer failed");

    emit ProposalExecuted(_id, p.recipient, p.amount);
}

function updateQuorum(uint256 _newQuorum) external onlyOwner {
    quorum = _newQuorum;
}

function updateVotingPeriod(uint256 _newPeriod) external onlyOwner {
    votingPeriod = _newPeriod;
}

}

