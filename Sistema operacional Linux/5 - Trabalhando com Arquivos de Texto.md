## **Capítulo 5: Trabalhando com Arquivos de Texto**

### **Editando Arquivos com `vim` e `vi`**
O editor de texto `vi` (e sua versão aprimorada `vim`) é essencial para administrar sistemas Linux, pois a maioria dos arquivos de configuração são textos simples.

#### **Iniciando o `vi`**
Para abrir um arquivo com `vi`:
```bash
vi nome_do_arquivo
```
Se o arquivo não existir, será criado.

Ao abrir o `vi`, ele entra no **modo de comando**. Para editar, é necessário alternar para o **modo de inserção**.

#### **Modos do `vi`**
- **Modo de comando**: Navegação e execução de ações.
- **Modo de inserção**: Permite digitar texto.

#### **Inserindo Texto**
Para entrar no **modo de inserção**, use um dos seguintes comandos:
- `i` – Insere antes do cursor.
- `a` – Insere após o cursor.
- `o` – Abre uma nova linha abaixo.
- `O` – Abre uma nova linha acima.

Após inserir o texto, pressione `ESC` para voltar ao modo de comando.

#### **Movimentação no Arquivo**
Use as teclas:
- `h` – Esquerda
- `l` – Direita
- `j` – Baixo
- `k` – Cima

Outros atalhos:
- `0` – Vai para o início da linha.
- `$` – Vai para o final da linha.
- `G` – Vai para o final do arquivo.
- `gg` – Vai para o início do arquivo.

#### **Deletando, Copiando e Alterando Texto**
- `x` – Apaga o caractere sob o cursor.
- `dd` – Deleta a linha atual.
- `yy` – Copia a linha atual.
- `p` – Cola após o cursor.
- `P` – Cola antes do cursor.

#### **Saindo do `vi`**
- `:q` – Sai (se nenhuma modificação foi feita).
- `:q!` – Sai sem salvar.
- `:wq` ou `ZZ` – Salva e sai.

---

### **Localizando e Buscando Arquivos**
O Linux oferece diversas maneiras de localizar arquivos no sistema.

#### **Localizando Arquivos com `locate`**
O comando `locate` pesquisa arquivos rapidamente em um banco de dados atualizado periodicamente.
```bash
locate arquivo.txt
```
Para atualizar o banco de dados:
```bash
sudo updatedb
```

#### **Buscando Arquivos com `find`**
O comando `find` permite pesquisar arquivos com critérios específicos.

1. **Buscar por nome**:
   ```bash
   find / -name "arquivo.txt"
   ```

2. **Buscar por tamanho**:
   ```bash
   find /usr/share -size +5M
   ```

3. **Buscar por usuário**:
   ```bash
   find /home -user usuario
   ```

4. **Buscar por permissão**:
   ```bash
   find /var/log -perm 644
   ```

5. **Buscar por data de modificação**:
   ```bash
   find /etc -mtime -5
   ```
   Encontra arquivos modificados nos últimos 5 dias.

6. **Executar comandos com `find`**:
   ```bash
   find /tmp -name "*.log" -exec rm {} \;
   ```
   Remove todos os arquivos `.log` em `/tmp`.

---

### **Pesquisando Conteúdo em Arquivos com `grep`**
O comando `grep` permite buscar palavras ou frases dentro de arquivos.

#### **Pesquisa Simples**
```bash
grep "palavra" arquivo.txt
```

#### **Pesquisa em Todos os Arquivos de um Diretório**
```bash
grep "erro" /var/log/*
```

#### **Pesquisa Recursiva**
```bash
grep -r "configuração" /etc/
```

#### **Opções Úteis**
- `-i` – Ignora maiúsculas e minúsculas.
- `-v` – Exclui linhas que contêm o termo.
- `-l` – Lista apenas os arquivos que contêm o termo.

Exemplo:
```bash
grep -i "servidor" /etc/*
```
Lista todas as ocorrências da palavra "servidor", ignorando diferenciação de maiúsculas/minúsculas.
