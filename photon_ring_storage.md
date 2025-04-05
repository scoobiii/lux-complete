# PhotonRingStorage

Experimento de Armazenamento e Processamento de Luz por Reflexão Circular

Visão Geral

O projeto PhotonRingStorage é uma prova de conceito para armazenamento e processamento de informação utilizando um feixe de luz circulando em um anel de fibra óptica. O sistema visa demonstrar funcionalidades como buffer óptico, delay analógico, e potencial armazenamento quântico.

Requisitos

Impressora 3D (PLA ou PETG)

Cortadora a laser (acrilíco)

Fonte laser (Ex: Thorlabs CPS635R)

Fibra óptica monomodo (Corning SMF-28 Ultra)

Acoplador FC/APC

Fotodetector (Ex: Thorlabs DET36A2)

Osciloscópio ou DAQ

Arduino ou ESP32

Computador com Python 3


Estrutura do Repositório

PhotonRingStorage/
├── hardware/
│   ├── suporte-anel.stl
│   ├── base-montagem.dxf
├── software/
│   ├── arduino_modulador.ino
│   ├── leitura_python_serial.py
│   ├── photon_api.py (FastAPI)
├── docs/
│   ├── instrucoes_montagem.pdf
│   ├── teoria_optica_reflexao.md
├── tests/
│   ├── test_leitura.py
├── README.md

Instruções de Montagem

1. Imprima o suporte circular em 3D e corte a base de acrílico.


2. Fixe o anel de fibra na estrutura, evitando curvaturas agudas.


3. Conecte o laser ao acoplador de entrada.


4. Instale o fotodetector em ponto de leitura após 1 ou mais voltas.


5. Opcional: adicione um EOM (modulador de fase) entre os ciclos.


6. Execute o script leitura_python_serial.py para monitoramento.



Execução do Software

Arduino

Use o arduino_modulador.ino para modular a luz com padrões binários.


Python

pip install pyserial fastapi uvicorn
python software/leitura_python_serial.py

Iniciar API de Controle

uvicorn software.photon_api:app --reload

APIs Disponíveis

POST /laser/on: Liga o feixe laser

POST /laser/off: Desliga

POST /modular: Envia padrão binário para o Arduino

GET /status: Estado atual do sistema


Experimentos

Persistência do Pulso: injete pulso e meça perdas

Buffer Binário: envie padrões como 101010 via modulador

Interferência: combine feixes e analise no fotodetector


Contribuição

1. Fork o repositório


2. Crie uma branch com seu experimento: feature/nova-funcionalidade


3. Envie um Pull Request



Licença

MIT License


---

Desenvolvido por comunidade aberta e Fab Labs.

