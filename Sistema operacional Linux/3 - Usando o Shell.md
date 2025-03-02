## **Capítulo 3: Usando o Shell**

### **Sobre Shells e Janelas de Terminal**
O shell no Linux é uma interface de linha de comando usada para interagir com o sistema operacional. Existem várias maneiras de acessá-lo:
- **Shell Prompt**: Se o sistema não tiver uma interface gráfica, ao fazer login, o usuário verá diretamente um **prompt de shell**, onde pode digitar comandos.
- **Janela de Terminal**: Em ambientes gráficos, pode-se abrir um terminal para usar o shell dentro da GUI.
- **Consoles Virtuais**: É possível alternar para consoles em modo texto pressionando `Ctrl + Alt + F1` a `F6` e retornar à interface gráfica com `Ctrl + Alt + F7` ou `F2` dependendo do sistema.

---

### **Escolhendo Seu Shell**
O shell mais comum no Linux é o **Bash (Bourne Again Shell)**, mas outros shells estão disponíveis:
- **C Shell (csh)** – Popular em sistemas BSD.
- **Korn Shell (ksh)** – Utilizado no UNIX System V.
- **Dash** – Shell padrão no Ubuntu para inicialização rápida.
- **Tcsh** e **Ash** – Alternativas leves e simplificadas.

Para verificar o shell padrão do usuário, pode-se usar:
```bash
echo $SHELL
```
Para listar e alterar o shell padrão:
```bash
chsh -s /bin/bash  # Exemplo para mudar para Bash
```

---

### **Executando Comandos**
Para executar comandos no shell, basta digitá-los e pressionar **Enter**. Exemplos:
```bash
date        # Mostra a data e hora atuais
whoami      # Exibe o nome do usuário logado
ls          # Lista arquivos no diretório atual
```
O shell distingue **comandos internos** (como `cd`, `echo`, `export`) e **comandos externos** (como `ls`, `grep`, `awk`).

#### **Entendendo a Sintaxe dos Comandos**
Os comandos seguem a estrutura:
```bash
comando [opções] [argumentos]
```
Por exemplo:
```bash
ls -l /home
```
Aqui, `ls` é o comando, `-l` é a opção que mostra detalhes dos arquivos, e `/home` é o argumento que especifica o diretório.

Para localizar um comando específico:
```bash
which comando      # Mostra o caminho de um comando
whereis comando    # Mostra a localização do executável e suas man pages
locate arquivo     # Busca rapidamente arquivos no sistema
find / -name nome  # Pesquisa arquivos no disco
```

---

### **Utilizando o Histórico de Comandos**
O shell mantém um histórico de comandos que podem ser reutilizados. Alguns comandos úteis:
```bash
history           # Lista os últimos comandos executados
!!               # Repete o último comando
!n               # Executa o comando de número 'n' no histórico
!texto           # Executa o último comando que começa com 'texto'
```
Para navegar pelo histórico:
- **Seta para cima (↑)** – Percorre comandos anteriores.
- **Ctrl + R** – Pesquisa um comando pelo nome.

---

### **Conectando e Expandindo Comandos**
O Linux permite combinar comandos para aumentar a eficiência:

1. **Encadeamento com Pipes (`|`)**:
   - Usa a saída de um comando como entrada de outro.
   ```bash
   ls -l | grep "txt"
   ```

2. **Execução Sequencial (`;`)**:
   - Executa comandos em sequência, independentemente do sucesso do anterior.
   ```bash
   date; uptime
   ```

3. **Execução Condicional (`&&` e `||`)**:
   - `&&` executa o segundo comando apenas se o primeiro for bem-sucedido.
   ```bash
   mkdir teste && cd teste
   ```
   - `||` executa o segundo comando apenas se o primeiro falhar.
   ```bash
   cd /diretorio_inexistente || echo "Erro ao acessar diretório"
   ```

4. **Execução em Background (`&`)**:
   - Permite executar processos em segundo plano.
   ```bash
   firefox &
   ```

5. **Expansões do Shell**:
   - **Expansão de variáveis**:
     ```bash
     echo "Usuário atual: $USER"
     ```
   - **Expansão aritmética**:
     ```bash
     echo $((5 + 3))
     ```

---

### **Trabalhando com Variáveis no Shell**
Variáveis armazenam informações e podem ser criadas dinamicamente:
```bash
MEU_NOME="Linux"
echo $MEU_NOME
```
Variáveis de ambiente podem ser exportadas para que fiquem disponíveis em subprocessos:
```bash
export PATH=$PATH:/novo/diretorio
```
Para listar todas as variáveis do ambiente:
```bash
env
```

#### **Criando e Usando Aliases**
Aliases são atalhos para comandos longos ou frequentemente usados:
```bash
alias ll="ls -l"
alias rm="rm -i"  # Protege contra exclusões acidentais
```
Para remover um alias:
```bash
unalias ll
```

---

### **Configurando o Ambiente do Shell**
Os arquivos de configuração do Bash incluem:
- `~/.bashrc` – Configuração de usuário para sessões interativas.
- `~/.bash_profile` – Executado ao iniciar uma sessão de login.
- `/etc/profile` – Configuração global do sistema.

Para personalizar o prompt do Bash:
```bash
export PS1="[\u@\h \W]\$ "
```
Isso exibe:
```
[usuario@hostname pasta]$
```

Para adicionar variáveis de ambiente permanentes, edite `~/.bashrc` ou `~/.bash_profile`:
```bash
export PATH=$PATH:/novo/caminho
```

---

### **Obtendo Informações sobre Comandos**
No Linux, há várias maneiras de obter ajuda sobre comandos:
- **Man Pages (`man`)**:
  ```bash
  man ls
  ```
- **Páginas de Ajuda (`--help`)**:
  ```bash
  ls --help
  ```
- **Comando `info`**:
  ```bash
  info ls
  ```
- **Apropos** (pesquisa por palavras-chave na documentação):
  ```bash
  apropos "disk"