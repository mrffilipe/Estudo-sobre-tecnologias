## **Capítulo 7: Escrevendo Scripts Simples de Shell**

### **Entendendo os Shell Scripts**
Os scripts de shell são arquivos de texto que contêm uma sequência de comandos que podem ser executados no terminal do Linux. Eles permitem a automação de tarefas repetitivas e podem ser usados para configurações do sistema, backups e até mesmo processos complexos.

Os scripts de shell são comparáveis aos **arquivos batch** do Windows e podem incluir:
- **Comandos do shell**.
- **Estruturas de controle de fluxo** (loops, condicionais).
- **Variáveis e funções**.
- **Expressões aritméticas e manipulação de texto**.

Os sistemas Linux utilizam amplamente **scripts de inicialização** para configurar serviços e recursos durante a inicialização do sistema.

---

### **Executando e Depurando Shell Scripts**
Os scripts podem ser executados de duas maneiras:
1. **Chamando diretamente o shell**:
   ```bash
   bash meu_script.sh
   ```
   Nesse caso, o arquivo **não precisa** ser executável.

2. **Tornando o script executável**:
   ```bash
   chmod +x meu_script.sh
   ./meu_script.sh
   ```
   O primeiro comando concede permissão de execução e o segundo executa o script.

3. **Depuração de scripts**:
   Para ver os comandos enquanto são executados:
   ```bash
   bash -x meu_script.sh
   ```
   Para depuração avançada, pode-se adicionar `set -x` no início do script.

---

### **Compreendendo Variáveis no Shell**
As variáveis são usadas para armazenar valores e reutilizá-los em diferentes partes do script.

#### **Declaração de variáveis**
```bash
NOME="Linux"
echo "Bem-vindo ao $NOME!"
```
- Não deve haver espaços ao redor do `=` ao definir variáveis.
- Para exibir o valor, usa-se `$VARIAVEL`.

#### **Expansão de Parâmetros**
O Bash permite manipular strings usando variáveis:
```bash
ARQUIVO="/home/user/documento.txt"
echo "Nome do arquivo: ${ARQUIVO##*/}"  # Exibe apenas "documento.txt"
echo "Extensão: ${ARQUIVO##*.}"         # Exibe "txt"
echo "Caminho: ${ARQUIVO%/*}"           # Exibe "/home/user"
```
Isso ajuda a separar partes de nomes de arquivos de maneira eficiente.

---

### **Realizando Operações Aritméticas**
Diferente de linguagens fortemente tipadas, o Bash trata variáveis como **strings por padrão** e converte-as para números quando necessário.

1. **Usando `let`**:
   ```bash
   let RESULTADO=10+5
   echo $RESULTADO
   ```

2. **Usando `expr`**:
   ```bash
   RESULTADO=$(expr 10 + 5)
   echo $RESULTADO
   ```

3. **Usando `bc` para cálculos mais avançados**:
   ```bash
   echo "10.5 * 3" | bc
   ```

4. **Incremento e decremento**:
   ```bash
   I=0
   echo $((++I))  # Incrementa antes de exibir
   echo $((I++))  # Exibe e depois incrementa
   ```

Essas operações são úteis para contadores em loops.

---

### **Usando Estruturas de Controle em Shell Scripts**
O Bash permite o uso de estruturas condicionais e loops.

#### **Condicionais `if...then`**
O `if` avalia expressões e executa comandos se a condição for verdadeira:
```bash
VAR=10
if [ $VAR -eq 10 ]; then
   echo "A variável é 10"
else
   echo "A variável não é 10"
fi
```
Outros operadores:
- `-eq` – Igual a
- `-ne` – Diferente de
- `-gt` – Maior que
- `-lt` – Menor que
- `-ge` – Maior ou igual a
- `-le` – Menor ou igual a

#### **Comando `case`**
Permite avaliar múltiplas opções:
```bash
read -p "Digite um número: " NUM
case $NUM in
   1) echo "Um";;
   2) echo "Dois";;
   *) echo "Outro número";;
esac
```

#### **Loops `for`, `while` e `until`**
O `for` itera sobre uma lista de itens:
```bash
for i in {1..5}; do
   echo "Número: $i"
done
```

O `while` executa enquanto a condição for verdadeira:
```bash
VAR=5
while [ $VAR -gt 0 ]; do
   echo "Contagem: $VAR"
   VAR=$((VAR-1))
done
```

O `until` executa até que a condição seja verdadeira:
```bash
VAR=0
until [ $VAR -eq 5 ]; do
   echo "Valor: $VAR"
   VAR=$((VAR+1))
done
```

Essas estruturas são essenciais para scripts dinâmicos.

---

### **Programas Úteis para Manipulação de Texto**
Shell scripts frequentemente usam comandos para processar arquivos de texto:

1. **Expressões regulares (`grep`)**:
   ```bash
   grep "erro" /var/log/syslog
   ```
   Filtra linhas contendo "erro".

2. **Cortar seções de linhas (`cut`)**:
   ```bash
   echo "usuario:senha:uid:gid" | cut -d':' -f1
   ```
   Retorna `usuario`, extraindo o primeiro campo separado por `:`.

3. **Traduzir ou remover caracteres (`tr`)**:
   ```bash
   echo "teste" | tr 't' 'T'
   ```
   Transforma `t` em `T`.

4. **Editor de fluxo (`sed`)**:
   ```bash
   sed 's/Linux/Unix/g' arquivo.txt
   ```
   Substitui "Linux" por "Unix" em todo o arquivo.

---

### **Exemplos de Shell Scripts**
#### **Lista Telefônica**
Criação de um script para armazenar números de telefone:
```bash
#!/bin/bash
echo "Nome:"
read NOME
echo "Telefone:"
read TELEFONE
echo "$NOME : $TELEFONE" >> contatos.txt
echo "Contato salvo!"
```

#### **Script de Backup**
Um script para fazer backup de arquivos:
```bash
#!/bin/bash
DIR_ORIGEM="/home/user/documentos"
DIR_BACKUP="/backup"
ARQUIVO_BACKUP="backup_$(date +%Y%m%d).tar.gz"

tar -czf $DIR_BACKUP/$ARQUIVO_BACKUP $DIR_ORIGEM
echo "Backup concluído: $DIR_BACKUP/$ARQUIVO_BACKUP"
```

Scripts como esses facilitam tarefas administrativas.