## **Capítulo 11: Gerenciando Contas de Usuário**

### **Criando Contas de Usuário**
As contas de usuário são fundamentais no Linux, pois garantem a separação de permissões entre diferentes usuários e processos. Existem diversas formas de criar usuários no sistema:

#### **Criando usuários com `useradd`**
O comando `useradd` é a forma mais comum de adicionar um novo usuário via terminal:
```bash
sudo useradd -m -s /bin/bash -c "Nome Completo" usuario
sudo passwd usuario
```
Explicação:
- `-m` cria o diretório home.
- `-s /bin/bash` define o shell padrão.
- `-c "Nome Completo"` adiciona um comentário com o nome do usuário.
- `passwd usuario` define a senha.

#### **Definindo Padrões de Usuário**
Podemos definir padrões para novos usuários com:
```bash
sudo useradd -D
```
Para alterar um valor padrão, como o shell padrão:
```bash
sudo useradd -D -s /bin/zsh
```
Isso define o **Zsh** como shell padrão para novos usuários.

#### **Modificando Usuários com `usermod`**
Para alterar informações de um usuário existente:
```bash
sudo usermod -c "Novo Nome" usuario
sudo usermod -s /bin/zsh usuario
```
Isso altera o nome e o shell do usuário.

#### **Removendo Usuários com `userdel`**
O comando `userdel` exclui usuários do sistema:
```bash
sudo userdel -r usuario
```
O parâmetro `-r` remove também o diretório **home**.

---

### **Compreendendo Contas de Grupo**
Os **grupos** são usados para gerenciar permissões compartilhadas entre usuários.

#### **Criando Grupos**
Para criar um grupo:
```bash
sudo groupadd desenvolvedores
```
Para listar grupos existentes:
```bash
cat /etc/group
```
Para adicionar um usuário a um grupo:
```bash
sudo usermod -aG desenvolvedores usuario
```
O parâmetro `-aG` adiciona o usuário sem remover os grupos anteriores.

---

### **Gerenciando Usuários em Ambientes Empresariais**
Em empresas, é comum utilizar **servidores centralizados** para autenticação de usuários, como:
- **LDAP (Lightweight Directory Access Protocol)**
- **NIS (Network Information Service)**
- **Microsoft Active Directory**

Isso evita a necessidade de criar contas manualmente em cada máquina.

---

### **Definindo Permissões com Listas de Controle de Acesso (ACL)**
As ACLs permitem definir permissões mais flexíveis para usuários e grupos além do modelo tradicional do Linux.

#### **Configurando ACLs**
Para adicionar permissões de leitura e escrita a um usuário específico:
```bash
sudo setfacl -m u:usuario:rwx arquivo
```
Para visualizar ACLs de um arquivo:
```bash
getfacl arquivo
```
Para remover ACLs:
```bash
sudo setfacl -x u:usuario arquivo
```
As ACLs são úteis para diretórios compartilhados, onde usuários precisam de diferentes níveis de acesso.

---

### **Diretórios de Colaboração**
Em ambientes colaborativos, pode ser necessário configurar diretórios que permitem a modificação de arquivos por múltiplos usuários.

#### **Usando o "Sticky Bit"**
O **sticky bit** impede que usuários removam arquivos de outros dentro de um diretório compartilhado:
```bash
sudo chmod +t /diretorio
```
Isso é comum em diretórios como `/tmp`, onde múltiplos usuários têm acesso.

#### **Usando o "Set GID"**
O **set GID** garante que arquivos criados dentro de um diretório pertençam ao grupo correto:
```bash
sudo chmod g+s /diretorio
```
Isso mantém a estrutura de permissões consistente.

---

### **Centralizando Contas de Usuário**
Empresas costumam centralizar a autenticação de usuários em **servidores LDAP ou Active Directory**. No Linux, é possível integrar autenticação centralizada com:

1. **LDAP (Lightweight Directory Access Protocol)**
   - Servidor de diretório usado para autenticação em redes Linux e Windows.

2. **NIS (Network Information Service)**
   - Usado em redes Unix para compartilhar informações de usuários.

3. **Winbind**
   - Integração com **Active Directory** do Windows.

Exemplo de configuração de autenticação com LDAP:
```bash
sudo authconfig --enableldap --ldapserver=ldap://servidor --ldapbasedn="dc=empresa,dc=com" --update
```
Isso permite que usuários sejam autenticados sem precisar de uma conta local em cada máquina.