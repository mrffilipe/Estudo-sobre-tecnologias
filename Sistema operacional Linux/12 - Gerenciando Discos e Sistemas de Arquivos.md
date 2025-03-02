## **Capítulo 12: Gerenciando Discos e Sistemas de Arquivos**

### **Compreendendo o Armazenamento de Disco**
Os discos rígidos e dispositivos de armazenamento são fundamentais para manter dados de maneira persistente no Linux. O sistema operacional organiza esses dispositivos em **partições**, e cada partição recebe um sistema de arquivos específico.

#### **Tipos de Partições**
- **MBR (Master Boot Record)**: Método tradicional, suporta até **4 partições primárias** ou **3 primárias + 1 estendida** com várias partições lógicas.
- **GPT (GUID Partition Table)**: Suporta até **128 partições** e é recomendado para discos maiores que 2 TB.

Cada partição pode ser formatada com diferentes tipos de **sistemas de arquivos**, como **ext4, XFS, Btrfs**, entre outros.

---

### **Particionamento de Discos**
No Linux, o particionamento pode ser feito com ferramentas como `fdisk`, `parted` ou `gparted` (interface gráfica).

#### **Visualizando Partições**
Para listar partições no sistema:
```bash
sudo fdisk -l
```
Ou utilizando `parted` para discos com GPT:
```bash
sudo parted /dev/sdb print
```

#### **Criando uma Partição**
1. Iniciar o utilitário:
   ```bash
   sudo fdisk /dev/sdb
   ```
2. Criar uma nova partição:
   - Pressione **"n"** para criar uma partição.
   - Escolha **primária** ou **lógica**.
   - Defina o tamanho desejado.
3. Salvar e sair:
   - Pressione **"w"** para gravar as alterações.

Se for utilizar **partições GPT**, recomenda-se o `parted`:
```bash
sudo parted /dev/sdb mklabel gpt
sudo parted /dev/sdb mkpart primary ext4 1MiB 100%
```

---

### **Gerenciando Volume Lógico com LVM**
O **LVM (Logical Volume Manager)** permite criar volumes lógicos flexíveis, que podem ser redimensionados sem reiniciar o sistema.

#### **Criando um Volume LVM**
1. Criar um **volume físico**:
   ```bash
   sudo pvcreate /dev/sdb1
   ```
2. Criar um **grupo de volumes**:
   ```bash
   sudo vgcreate meuGrupo /dev/sdb1
   ```
3. Criar um **volume lógico**:
   ```bash
   sudo lvcreate -L 10G -n meuVolume meuGrupo
   ```
4. Formatar o volume lógico:
   ```bash
   sudo mkfs.ext4 /dev/meuGrupo/meuVolume
   ```

#### **Expandindo um Volume Lógico**
Para aumentar o tamanho de um volume lógico:
```bash
sudo lvextend -L +5G /dev/meuGrupo/meuVolume
sudo resize2fs /dev/meuGrupo/meuVolume
```
Isso adiciona **5GB** ao volume e ajusta o sistema de arquivos.

---

### **Montagem de Sistemas de Arquivos**
A montagem permite conectar partições ao sistema de arquivos do Linux.

#### **Montando uma Partição**
Para montar manualmente uma partição:
```bash
sudo mount /dev/sdb1 /mnt
```

Para que a partição seja montada automaticamente no boot, adicione uma linha ao `/etc/fstab`:
```
/dev/sdb1  /mnt  ext4  defaults  0  2
```
Isso garante que a partição seja montada toda vez que o sistema for iniciado.

#### **Desmontando um Sistema de Arquivos**
Antes de remover um dispositivo, ele deve ser desmontado:
```bash
sudo umount /mnt
```
Se o dispositivo estiver em uso, utilize:
```bash
sudo fuser -mv /mnt
```
Para forçar a desmontagem:
```bash
sudo umount -l /mnt
```

---

### **Criando um Sistema de Arquivos com `mkfs`**
Após particionar o disco, é necessário formatar a partição com um sistema de arquivos adequado.

#### **Formatando Partições**
1. **ext4**:
   ```bash
   sudo mkfs.ext4 /dev/sdb1
   ```
2. **XFS**:
   ```bash
   sudo mkfs.xfs /dev/sdb1
   ```
3. **Swap** (memória virtual):
   ```bash
   sudo mkswap /dev/sdb2
   sudo swapon /dev/sdb2
   ```

Esses comandos criam sistemas de arquivos que podem ser montados e utilizados pelo Linux.

---

### **Gerenciando Armazenamento com Cockpit**
O **Cockpit** é uma interface web para administração de servidores Linux, incluindo gerenciamento de discos e volumes.

#### **Instalação do Cockpit**
```bash
sudo dnf install cockpit
sudo systemctl enable --now cockpit.socket
```
Para acessar, abra um navegador e vá para:
```
https://localhost:9090
```

Dentro do Cockpit, é possível:
- Criar e formatar partições.
- Gerenciar volumes LVM.
- Configurar e monitorar RAID e swap.