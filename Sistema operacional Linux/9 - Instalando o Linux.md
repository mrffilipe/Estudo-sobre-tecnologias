## **Capítulo 9: Instalando o Linux**

### **Escolhendo um Computador**
O Linux pode ser instalado em diversos tipos de hardware, desde dispositivos móveis até computadores antigos. No entanto, para obter uma boa experiência em desktop, é necessário escolher o hardware adequado.

- **Processador**: Para instalações gráficas, recomenda-se pelo menos um processador **Pentium de 1 GHz**. Para virtualização, um processador de **64 bits** (x86_64) é essencial.
- **Memória RAM**: O Fedora recomenda pelo menos **1 GB**, mas **2 GB ou mais** são preferíveis para um melhor desempenho.
- **Armazenamento**: O Fedora requer no mínimo **20 GB** para uma instalação padrão. Sistemas minimalistas podem exigir apenas **600 MB** e servidores completos podem ocupar **7 GB** ou mais.
- **Dispositivo de Boot**: Um **DVD ou USB bootável** é necessário para iniciar a instalação.

Se o hardware não suportar boot por USB ou DVD, pode-se utilizar a instalação via rede com **PXE Boot**.

---

### **Instalando o Fedora a Partir de Mídia Live**
A instalação a partir de **mídia Live** é uma forma simples de instalar o Fedora. Esse método copia o sistema em execução do Live ISO para o disco rígido.

1. **Download da Imagem Live**
   - A imagem ISO deve ser baixada e gravada em um **DVD ou pendrive USB**.
   ```bash
   dd if=fedora.iso of=/dev/sdX bs=4M status=progress
   ```
   (Substitua `/dev/sdX` pelo dispositivo correto)

2. **Inicializando a Imagem Live**
   - O computador deve ser inicializado a partir do pendrive ou DVD.
   - No menu de boot, selecione **"Start Fedora-Workstation-Live"**.

3. **Iniciando a Instalação**
   - Dentro do ambiente Live, clique em **"Instalar no Disco Rígido"**.
   - Escolha o idioma e siga os passos do instalador.

4. **Opções de Instalação**
   - **Instalação única**: Remove todos os outros sistemas operacionais.
   - **Dual Boot**: Mantém um sistema operacional existente, como o Windows.
   - **Instalação em Máquina Virtual**: Pode ser feita usando VirtualBox, KVM ou VMware.

---

### **Instalando o Red Hat Enterprise Linux (RHEL)**
O RHEL é instalado geralmente a partir de **mídia de instalação completa** (DVD ou imagem ISO). Esse método permite maior controle sobre os pacotes instalados.

#### **Passos para Instalação**
1. **Obter a Mídia de Instalação**
   - O RHEL pode ser baixado do site oficial da Red Hat ou, para alternativas gratuitas, pode-se usar o CentOS ou Rocky Linux.

2. **Inicializar o Instalador**
   - Insira o USB/DVD e reinicie o computador.
   - Selecione **"Test this media & install"** para verificar erros na mídia antes da instalação.

3. **Configuração do Sistema**
   - Escolha idioma, teclado e fuso horário.
   - Defina **senha para root** e crie um usuário administrador.

4. **Configuração de Rede e Pacotes**
   - O instalador permite configurar a rede e repositórios online.
   - O usuário pode optar por instalar um servidor mínimo ou uma estação de trabalho completa.

5. **Conclusão e Primeiro Boot**
   - Após a instalação, reinicie o sistema.
   - Para atualizações:
     ```bash
     sudo dnf upgrade
     ```
     Isso garante que o sistema esteja atualizado.

---

### **Entendendo Instalações Baseadas na Nuvem**
Diferente das instalações convencionais, sistemas baseados na **nuvem** são gerenciados por um controlador de virtualização, como:
- **Amazon EC2**
- **Google Compute Engine**
- **OpenStack**

Esses sistemas utilizam **imagens pré-configuradas**, onde metadados são adicionados para definir:
- Nome do host.
- Configuração de rede.
- Tamanho do armazenamento e alocação de CPU/RAM.

---

### **Explorando Temas Comuns de Instalação**
1. **Atualizando ou Instalando do Zero**
   - Pode-se optar por manter arquivos e configurações ao atualizar para uma nova versão do Linux, ou fazer uma instalação limpa.

2. **Dual Boot (Linux + Windows)**
   - Para instalar Linux ao lado do Windows, deve-se:
     - Criar espaço livre no disco.
     - Instalar o Linux em uma partição separada.
     - Configurar o **GRUB** para gerenciar o boot dos dois sistemas.

---

### **Executando o Linux em Máquinas Virtuais**
Linux pode ser instalado em **ambientes virtuais**, como:
- **KVM** (Kernel-based Virtual Machine)
- **VirtualBox**
- **VMware**
- **Hyper-V**

Vantagens:
- Permite testar diferentes distribuições sem alterar o sistema principal.
- Facilidade para snapshots e backups.

---

### **Opções de Boot na Instalação**
1. **Desativar recursos problemáticos**
   ```bash
   linux noapic nolapic acpi=off
   ```

2. **Corrigir problemas de vídeo**
   ```bash
   linux nomodeset
   ```

3. **Boot com configurações específicas**
   - **Kickstart**: Automatiza instalações em massa com um arquivo de configuração.
   - **Repositórios remotos**: Instala pacotes diretamente da internet.

---

### **Particionamento de Discos**
O particionamento adequado melhora a organização e desempenho do sistema.

1. **Tipos de Partições**
   - **MBR**: Suporta até 4 partições primárias, limitado a discos de **2 TB**.
   - **GPT**: Suporta até **128 partições** e discos de **mais de 2 TB**.

2. **Dicas para Particionamento**
   - `/` (Raiz): Mínimo de **20 GB**.
   - `/home`: Para arquivos pessoais.
   - `swap`: Entre **1 e 2 vezes** o tamanho da RAM, dependendo do uso.

---

### **Usando o GRUB Boot Loader**
O **GRUB** gerencia múltiplos sistemas operacionais e opções de inicialização.

- Para atualizar o GRUB após mudanças:
  ```bash
  sudo grub2-mkconfig -o /boot/grub2/grub.cfg
  ```

- Para reinstalar o GRUB:
  ```bash
  sudo grub2-install /dev/sda
  ```

O GRUB também pode ser personalizado para definir opções de inicialização padrão.