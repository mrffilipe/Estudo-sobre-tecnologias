## **Capítulo 6: Gerenciando Processos em Execução**

### **Entendendo Processos no Linux**
No Linux, um **processo** é uma instância de um programa em execução. Cada processo possui um **ID único (PID)** e pode estar associado a um usuário e grupo específicos. O gerenciamento eficiente de processos é fundamental para administrar o desempenho do sistema.

Os principais conceitos relacionados a processos incluem:
- **Processos Foreground e Background** – Processos podem ser executados em primeiro plano ou em segundo plano.
- **Sinais de Processos** – Sinais como `SIGTERM` e `SIGKILL` permitem encerrar ou pausar processos.
- **Prioridade de CPU** – O **nice value** define a prioridade de um processo em relação aos demais.

---

### **Listando Processos**
O Linux oferece diversas ferramentas para visualizar processos ativos:

1. **Comando `ps`** – Exibe processos em execução.
   ```bash
   ps aux
   ```
   - `a` – Lista processos de todos os usuários.
   - `u` – Mostra detalhes como usuário, PID e uso de memória/CPU.
   - `x` – Inclui processos que não estão associados a um terminal.

2. **Comando `top`** – Exibe uma visão dinâmica dos processos.
   ```bash
   top
   ```
   - Pressione `q` para sair.
   - Use `M` para ordenar por uso de memória.
   - Pressione `k` e digite um **PID** para encerrar um processo.

3. **Gerenciador de Tarefas Gráfico (System Monitor)** – Disponível em desktops GNOME e KDE, permitindo visualizar e encerrar processos de forma gráfica.

---

### **Gerenciando Processos Foreground e Background**
Um processo pode ser iniciado em segundo plano adicionando um `&` ao final do comando:
```bash
ping google.com > ping.log &
```
Para listar processos em background:
```bash
jobs
```
Para trazer um processo de volta ao foreground:
```bash
fg %1
```
Para continuar um processo suspenso no background:
```bash
bg %1
```
Para suspender um processo em execução, use `Ctrl + Z`.

---

### **Matando e Priorizando Processos**
#### **Encerrando Processos (`kill`, `killall`)**
1. **Encerrar um processo pelo PID**:
   ```bash
   kill PID
   ```
2. **Forçar a finalização do processo**:
   ```bash
   kill -9 PID
   ```
3. **Encerrar todos os processos com um nome específico**:
   ```bash
   killall firefox
   ```

#### **Alterando a Prioridade de Processos (`nice` e `renice`)**
O comando `nice` define a prioridade ao iniciar um processo:
```bash
nice -n 10 comando
```
Para alterar a prioridade de um processo já em execução:
```bash
renice -n -5 -p PID
```
- Valores menores de **nice** dão **mais prioridade**.
- Apenas o **root** pode definir valores negativos.

---

### **Limitando Processos com `cgroups`**
Os **cgroups** permitem restringir recursos de CPU, memória e rede para processos específicos, sendo amplamente utilizados em servidores e containers.

Principais tipos de controle do `cgroups`:
- **cpu** – Define a alocação de tempo de CPU.
- **memory** – Limita o uso de RAM.
- **blkio** – Controla o acesso a dispositivos de armazenamento.
- **cpuset** – Associa processos a CPUs específicas.
- **net_cls** – Restringe largura de banda de rede.

Exemplo de criação de um grupo com limitação de CPU:
```bash
sudo cgcreate -g cpu:/meugrupo
echo 50000 | sudo tee /sys/fs/cgroup/cpu/meugrupo/cpu.cfs_quota_us
```
Isso limita os processos do grupo a **50%** da capacidade da CPU.