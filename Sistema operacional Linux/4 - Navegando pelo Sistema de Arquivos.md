## **Capítulo 4: Navegando pelo Sistema de Arquivos**

### **Usando Comandos Básicos do Sistema de Arquivos**
O sistema de arquivos do Linux é baseado em uma estrutura hierárquica, com o diretório raiz `/` no topo. Para navegar nele, utilizamos comandos essenciais:

- **`cd [diretório]`** – Muda para um diretório específico.
  ```bash
  cd /usr/share
  ```
- **`pwd`** – Exibe o diretório atual.
  ```bash
  pwd
  ```
- **`mkdir [nome]`** – Cria um novo diretório.
  ```bash
  mkdir novo_diretorio
  ```
- **`rmdir [nome]`** – Remove um diretório vazio.
- **`ls [opções]`** – Lista os arquivos e diretórios.
  ```bash
  ls -l  # Exibe detalhes dos arquivos
  ls -a  # Mostra arquivos ocultos
  ```
  
---

### **Usando Metacaracteres e Operadores**
Metacaracteres são símbolos especiais usados para facilitar a manipulação de arquivos e diretórios:

- `*` – Corresponde a qualquer número de caracteres.
  ```bash
  ls a*
  ```
  Lista todos os arquivos que começam com "a".

- `?` – Corresponde a um único caractere.
  ```bash
  ls file?
  ```
  Lista arquivos como `file1`, `file2`, mas não `file10`.

- `[ ]` – Define um conjunto de caracteres.
  ```bash
  ls [abc]*
  ```
  Lista arquivos que começam com "a", "b" ou "c".

- `{ }` – Expande padrões de nomes.
  ```bash
  touch {arquivo1,arquivo2,arquivo3}
  ```

Além disso, há operadores de **redirecionamento**:
- `>` – Redireciona a saída para um arquivo (sobrescrevendo-o).
  ```bash
  ls > lista_arquivos.txt
  ```
- `>>` – Acrescenta saída a um arquivo.
  ```bash
  echo "Nova linha" >> lista_arquivos.txt
  ```
- `<` – Usa um arquivo como entrada para um comando.
  ```bash
  sort < lista_arquivos.txt
  ```

---

### **Listando Arquivos e Diretórios**
O comando **`ls`** pode ser combinado com várias opções para exibir arquivos de diferentes maneiras:

- **Listagem simples:**
  ```bash
  ls
  ```
- **Listagem detalhada:**
  ```bash
  ls -l
  ```
  Exibe permissões, dono, grupo, tamanho e data de modificação.

- **Listagem de arquivos ocultos:**
  ```bash
  ls -a
  ```
  Mostra arquivos iniciados com `.` (exemplo: `.bashrc`).

- **Listagem ordenada por tamanho:**
  ```bash
  ls -lhS
  ```
  Exibe arquivos do maior para o menor.

---

### **Entendendo Permissões e Propriedade de Arquivos**
No Linux, cada arquivo tem permissões e donos. O comando **`ls -l`** exibe essas informações:

```bash
-rw-r--r--  1 user grupo  1234 Mar  1 12:00 arquivo.txt
```

A estrutura da permissão é dividida em:
- **Dono** (`user`) – Pode ser o criador do arquivo.
- **Grupo** (`grupo`) – Grupo de usuários que podem acessar o arquivo.
- **Outros** – Qualquer outro usuário do sistema.

#### **Mudando Permissões com `chmod`**
1. **Usando números:**
   - `4` = leitura (`r`), `2` = escrita (`w`), `1` = execução (`x`).
   - Para dar permissão total ao dono, leitura e execução para grupo e outros:
     ```bash
     chmod 755 arquivo.txt
     ```

2. **Usando letras:**
   ```bash
   chmod u+rwx,g+rx,o+r arquivo.txt
   ```
   - `u` = usuário (dono)
   - `g` = grupo
   - `o` = outros
   - `r` = leitura, `w` = escrita, `x` = execução

#### **Mudando Propriedade de Arquivos**
- **Mudar dono do arquivo:**
  ```bash
  sudo chown novo_dono arquivo.txt
  ```
- **Mudar dono e grupo:**
  ```bash
  sudo chown novo_dono:novo_grupo arquivo.txt
  ```

#### **Definindo Permissões Padrão com `umask`**
O comando `umask` define permissões padrão para novos arquivos:
```bash
umask 022
```
Isso resulta em arquivos com permissões **644** (`rw-r--r--`) e diretórios com **755** (`rwxr-xr-x`).

---

### **Movendo, Copiando e Removendo Arquivos**
1. **Movendo arquivos (`mv`)**:
   ```bash
   mv origem destino
   mv arquivo.txt /home/user/
   ```
   Também pode ser usado para renomear arquivos:
   ```bash
   mv arquivo.txt novo_nome.txt
   ```

2. **Copiando arquivos (`cp`)**:
   ```bash
   cp arquivo.txt copia.txt
   ```
   Para copiar diretórios inteiros:
   ```bash
   cp -r pasta_origem pasta_destino
   ```

3. **Removendo arquivos e diretórios (`rm`)**:
   ```bash
   rm arquivo.txt
   ```
   Para remover diretórios:
   ```bash
   rm -r pasta/
   ```
   Para evitar confirmação:
   ```bash
   rm -rf pasta/
   ```