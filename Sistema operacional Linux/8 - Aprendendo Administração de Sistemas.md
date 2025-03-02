## **Capítulo 8: Aprendendo Administração de Sistemas**

### **Compreendendo a Administração de Sistemas**
A administração de sistemas Linux envolve a configuração, gerenciamento e manutenção de recursos essenciais para garantir a estabilidade, segurança e eficiência do sistema. O administrador de sistemas é responsável por:
- Gerenciar usuários e permissões.
- Configurar redes e serviços.
- Monitorar e otimizar desempenho.
- Aplicar medidas de segurança e backup.

Mesmo em sistemas de um único usuário, a administração é essencial para garantir um ambiente seguro e bem configurado.

---

### **Usando Ferramentas Gráficas de Administração**
Embora a administração do Linux tradicionalmente ocorra via **linha de comando**, ferramentas gráficas facilitam tarefas administrativas.

1. **Cockpit** – Interface web para gerenciar:
   - Monitoramento do sistema.
   - Configuração de rede e serviços.
   - Gerenciamento de armazenamento.
   ```bash
   sudo systemctl enable --now cockpit.socket
   ```
   Acesse via navegador em `https://localhost:9090`.

2. **Ferramentas `system-config-*`** – Disponíveis em Fedora/RHEL:
   - **`system-config-users`** – Gerenciamento de usuários.
   - **`system-config-network`** – Configuração de rede.
   - **`system-config-firewall`** – Configuração do firewall.

3. **Outras Ferramentas Web**:
   - **Webmin** – Interface abrangente para administração remota.
   - **phpMyAdmin** – Gerenciamento de bancos de dados MySQL via web.

---

### **Usando a Conta de Root**
O **usuário root** tem acesso completo ao sistema. Para evitar riscos, recomenda-se usar privilégios administrativos apenas quando necessário.

#### **Alternando para Root via Terminal**
1. **Usando `su`**:
   ```bash
   su -
   ```
   Isso abre um shell como root.

2. **Usando `sudo`**:
   ```bash
   sudo comando
   ```
   No Ubuntu e em algumas distribuições, `sudo` é usado em vez de `su`.

3. **Adicionando um usuário ao grupo `sudo`**:
   ```bash
   sudo usermod -aG sudo usuario
   ```

4. **Permitindo acesso sem senha** (editar `/etc/sudoers` com `visudo`):
   ```bash
   usuario ALL=(ALL) NOPASSWD: ALL
   ```

O **root** pode acessar qualquer arquivo, modificar permissões e instalar pacotes. No entanto, o uso indevido pode causar danos ao sistema.

---

### **Explorando Comandos Administrativos, Arquivos de Configuração e Logs**
A administração do sistema requer conhecimento sobre:
- **Comandos administrativos** – Normalmente armazenados em `/sbin` e `/usr/sbin`.
- **Arquivos de configuração** – Localizados em `/etc`.
- **Logs do sistema** – Guardados em `/var/log`.

#### **Principais Comandos Administrativos**
1. **Gerenciamento de usuários**:
   ```bash
   useradd novo_usuario
   passwd novo_usuario
   usermod -aG sudo novo_usuario
   ```

2. **Gerenciamento de serviços (`systemd`)**:
   ```bash
   systemctl status sshd
   systemctl restart apache2
   ```

3. **Monitoramento de processos**:
   ```bash
   top
   ps aux | grep apache
   ```

4. **Verificando logs com `journalctl`**:
   ```bash
   journalctl -u sshd --since "1 hour ago"
   ```

5. **Filtrando logs por prioridade**:
   ```bash
   journalctl PRIORITY=3
   ```

6. **Gerenciamento de logs com `rsyslog`**:
   - Configurado no arquivo `/etc/rsyslog.conf`.
   - Logs comuns:
     - `/var/log/messages` – Logs gerais do sistema.
     - `/var/log/secure` – Registros de login e autenticação.

---

### **Usando Outras Contas Administrativas**
Além do root, alguns serviços Linux rodam com usuários específicos para aumentar a segurança. Exemplos:
- **`apache`** – Para servidores web.
- **`postfix`** – Para servidores de e-mail.
- **`lp`** – Para serviços de impressão.

Essa segmentação evita que um serviço comprometido comprometa todo o sistema.

---

### **Verificando e Configurando Hardware**
A administração do sistema também envolve a detecção e gerenciamento de hardware.

1. **Verificando informações do sistema**:
   ```bash
   lscpu        # Exibe detalhes da CPU
   lsblk        # Lista dispositivos de armazenamento
   lspci        # Mostra informações sobre dispositivos PCI
   lsusb        # Exibe dispositivos USB conectados
   ```

2. **Gerenciando hardware removível**:
   - Montar manualmente:
     ```bash
     mount /dev/sdb1 /mnt/usb
     ```
   - Desmontar:
     ```bash
     umount /mnt/usb
     ```

3. **Trabalhando com módulos do kernel**:
   - **Listar módulos carregados**:
     ```bash
     lsmod
     ```
   - **Carregar um módulo manualmente**:
     ```bash
     sudo modprobe nome_do_modulo
     ```
   - **Remover um módulo**:
     ```bash
     sudo rmmod nome_do_modulo
     ```
   - **Listar informações de um módulo específico**:
     ```bash
     modinfo nome_do_modulo
     ```

Isso é útil para depurar problemas de hardware.