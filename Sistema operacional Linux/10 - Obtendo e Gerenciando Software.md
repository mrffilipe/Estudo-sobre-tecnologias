## **Capítulo 10: Obtendo e Gerenciando Software**

### **Gerenciando Software no Desktop**
As distribuições modernas de Linux, como Fedora e Ubuntu, possuem ferramentas gráficas que facilitam a instalação de software sem precisar interagir diretamente com a linha de comando. No Fedora, por exemplo, o **Software Center** permite:
- Pesquisar pacotes de software.
- Instalar e remover aplicações com um clique.
- Atualizar softwares já instalados.

No Ubuntu, o **Ubuntu Software Center** desempenha uma função semelhante, permitindo a instalação de pacotes `.deb` sem a necessidade de comandos manuais.

---

### **Entendendo a Empacotação de Software no Linux (RPM e DEB)**
Historicamente, os softwares no Linux eram instalados manualmente a partir do código-fonte, o que exigia a compilação do programa antes do uso. Para facilitar esse processo, foram criados **gerenciadores de pacotes**, que padronizaram a instalação de softwares.

Os dois principais formatos de pacotes usados nas distribuições Linux são:
- **DEB (`.deb`)** – Criado pelo projeto Debian, utilizado pelo **Ubuntu, Debian, Linux Mint**, entre outras distribuições.
- **RPM (`.rpm`)** – Originalmente criado pela Red Hat, utilizado no **Fedora, RHEL, CentOS, Oracle Linux** e distribuições derivadas.

Cada um desses formatos contém não apenas os arquivos do software, mas também metadados como:
- Dependências.
- Informações sobre versões.
- Tamanho e licenciamento.

As distribuições que utilizam o formato DEB fazem uso dos comandos **`apt` e `dpkg`** para gerenciar pacotes, enquanto as distribuições baseadas em RPM utilizam **`dnf`, `yum` e `rpm`**.

---

### **Gerenciando Pacotes RPM com YUM e DNF**
O **YUM (Yellowdog Updater Modified)** foi desenvolvido para resolver o problema de dependências no RPM, permitindo que pacotes fossem instalados automaticamente com suas dependências resolvidas. No **Fedora 22+ e RHEL 8+**, o YUM foi substituído pelo **DNF**, que possui uma arquitetura mais eficiente.

#### **Comandos Essenciais do DNF**
1. **Procurando pacotes**:
   ```bash
   dnf search nome-do-pacote
   ```

2. **Instalando pacotes**:
   ```bash
   sudo dnf install nome-do-pacote
   ```

3. **Removendo pacotes**:
   ```bash
   sudo dnf remove nome-do-pacote
   ```

4. **Atualizando pacotes**:
   ```bash
   sudo dnf update
   ```

5. **Listando pacotes instalados**:
   ```bash
   dnf list installed
   ```

6. **Baixando pacotes sem instalar**:
   ```bash
   dnf download nome-do-pacote
   ```

O DNF também suporta repositórios de terceiros, como **EPEL e RPMFusion**, que oferecem pacotes não incluídos nos repositórios oficiais.

---

### **Gerenciando Pacotes com o Comando RPM**
O comando `rpm` permite manipular pacotes diretamente, sem depender do `dnf` ou `yum`.

#### **Comandos Básicos do RPM**
1. **Instalar um pacote local**:
   ```bash
   sudo rpm -i pacote.rpm
   ```
2. **Atualizar um pacote**:
   ```bash
   sudo rpm -U pacote.rpm
   ```
3. **Remover um pacote**:
   ```bash
   sudo rpm -e nome-do-pacote
   ```
4. **Verificar se um pacote está instalado**:
   ```bash
   rpm -q nome-do-pacote
   ```
5. **Listar todos os pacotes instalados**:
   ```bash
   rpm -qa
   ```
6. **Verificar a origem de um pacote**:
   ```bash
   rpm -qi nome-do-pacote
   ```

Embora o `rpm` seja útil, ele não gerencia automaticamente dependências como o `dnf`, tornando o gerenciamento manual de pacotes mais trabalhoso.

---

### **Gerenciando Software na Empresa**
Em ambientes corporativos, é comum utilizar **servidores de repositórios internos** para distribuir pacotes de software de maneira centralizada. Ferramentas como:
- **Satellite Server (Red Hat)**
- **Spacewalk**
- **Katello**

Permitem controlar versões, aplicar atualizações automáticas e garantir que todos os sistemas tenham o software adequado. Além disso, algumas empresas utilizam **containers** (Docker, Podman) para empacotamento e distribuição de aplicações.