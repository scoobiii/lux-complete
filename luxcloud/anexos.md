# **Anexos Técnicos do Projeto Lux Cloud**

## **1. Esquemas do Protótipo**

### **1.1 Diagramas Eletrônicos (KiCad)**
- **LuxNode v1.0 Schematic**:  
  - Controle de laser RGB via PWM.  
  - Circuito de leitura do sensor TCS34725 (I²C).  
  - [Download: `LuxNode_v1.sch`](fake-link-kicad/luxnode)  

- **Layout da Placa**:  
  - Design compacto para montagem em OpenRack.  
  - [Download: `LuxNode_PCB.layout`](fake-link-kicad/pcb)  

### **1.2 Modelos 3D (STL)**
- **Suporte para Alinhamento Óptico**:  
  - Peças impressas em 3D para laser/fotodiodos.  
  - [Download: `Optical_Mount.stl`](fake-link-stl/mount)  
- **Chassis Modular**:  
  - Compatível com padrão OpenCompute.  
  - [Download: `LuxChassis_v2.stl`](fake-link-stl/chassis)  

---

## **2. Código do Emulador (GitHub)**  
Repositório público com todas as ferramentas de simulação:  
🔗 **[github.com/lux-cloud/emulator](https://github.com/lux-cloud/emulator)**  

### **2.1 Principais Módulos**
- **PhotonSim**:  
  ```python
  def simulate_interferometer(phase_shift):
      # Simula interferência Mach-Zehnder
      return output_intensity
  ```
- **LuxDSL Translator**:  
  - Converte algoritmos binários para lógica multinária.  
  - Exemplo: `lux_translate hello_world.c --base=256`.  

- **Visualizador WDM**:  
  ![WDM Visualization](fake-link-img/wdm-screenshot.png)  

### **2.2 Dependências**
- Python 3.10+, NumPy, Matplotlib.  
- Instalação:  
  ```bash
  pip install lux-emulator
  ```

---

## **3. Dataset de Validação Matemática**  
Dados brutos e scripts para reproduzir os resultados:  
📊 **[Dataset no Zenodo](https://zenodo.org/lux-data)**  

### **3.1 Arquivos Incluídos**
- `channel_capacity.csv`: Cálculos de Shannon para canais ópticos.  
- `lambda_calculus_proofs.txt`: Derivações formais em λ-cálculo.  
- `energy_benchmark.xlsx`: Comparativo energia (Lux vs Binário).  

### **3.2 Exemplo de Análise**
```python
import pandas as pd
df = pd.read_csv("channel_capacity.csv")
print(df.groupby("base").mean())  # Capacidade média por base
```

---

## **4. Licença e Autoria**  
**Autores**: Equipe Lux Cloud (MPK Labs) | **Contato**: contact@lux-cloud.org  
**Licença**: [CC-BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)  
- **Permitido**: Uso não-comercial, modificação, distribuição com atribuição.  
- **Restrito**: Aplicações comerciais exigem licença especial.  

---

### **Como Contribuir**  
1. Faça um fork do lux complete, refine, surpreenda!
2. Submeta pull requests para:  
   - Novos modelos de codificação óptica.  
   - Otimizações no PhotonSim.  
3. Participe da discussão em [Discord](em construção) link-discord).  

**Próxima Fase**: Protótipo físico em escala de data center (2025). 🚀
