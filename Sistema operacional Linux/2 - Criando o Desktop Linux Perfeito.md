## **Capítulo 2: Criando o Desktop Linux Perfeito**

### **Entendendo a Tecnologia de Desktop no Linux**
Os ambientes gráficos em sistemas Linux são baseados no **X Window System**, desenvolvido pela **X.Org Foundation**. Ele fornece a estrutura necessária para diferentes tipos de interfaces gráficas (GUI), incluindo **GNOME, KDE, XFCE** e outras.

Recentemente, surgiu o **Wayland**, uma alternativa ao X.Org, que visa maior desempenho e segurança. **Fedora** já utiliza **Wayland** por padrão, mas a maioria dos sistemas ainda suporta X.Org.

A interface gráfica no Linux é composta por:
- **Gerenciador de janelas**: Controla a aparência e o comportamento das janelas.
- **Ambiente de desktop**: Inclui menus, painéis e aplicativos integrados.
- **Gerenciadores de arquivos**: Como o **Nautilus** no GNOME, que facilita a navegação e organização de arquivos.

---

### **Iniciando com a Imagem Live do Fedora GNOME Desktop**
Para experimentar o GNOME, é possível usar uma **imagem Live do Fedora**, que pode ser gravada em um DVD ou pendrive USB. Esse sistema permite testar o Linux sem precisar instalá-lo no disco rígido.

Passos para iniciar um sistema Live:
1. **Baixar a imagem** ISO do Fedora.
2. **Gravar** em um DVD ou criar um pendrive bootável.
3. **Reiniciar o computador** e selecionar o boot pelo DVD/USB.
4. **Escolher entre instalar o Fedora ou testar o ambiente Live**.

A vantagem da imagem Live é que permite explorar o GNOME sem modificar o sistema instalado.

---

### **Usando o Desktop GNOME 3**
O **GNOME 3** trouxe mudanças radicais comparado ao **GNOME 2**, tornando-se mais moderno e fluído, semelhante a interfaces móveis.

1. **Ao iniciar o sistema**:
   - Se estiver usando uma sessão Live, o login será feito automaticamente.
   - Se for um sistema instalado, será necessário escolher um usuário e inserir a senha.

2. **Navegação**:
   - **Com o mouse**: Mover o cursor para o canto superior esquerdo ativa a **Visão Geral** (Overview), exibindo as janelas ativas e lançadores de aplicativos.
   - **Com o teclado**: A tecla **Super (Windows)** alterna entre a área de trabalho e a Visão Geral.

3. **Configuração do GNOME 3**:
   - É possível personalizar o desktop usando a ferramenta **GNOME Tweaks**.
   - **Extensões GNOME Shell** permitem adicionar funcionalidades extras, como menus tradicionais e docks.

---

### **Expandindo o GNOME 3**
O GNOME pode ser ampliado de várias formas:
- **Extensões do GNOME Shell**: Adicionam funcionalidades ao ambiente gráfico.
- **GNOME Tweak Tool**: Permite ajustar temas, fontes e comportamentos do sistema.

---

### **Aplicações no Desktop**
O GNOME oferece aplicativos integrados para diversas funções:
- **Gerenciamento de arquivos**: O **Nautilus** permite acessar e organizar pastas.
- **Instalação de software**: Aplicações podem ser gerenciadas pela **GNOME Software**.
- **Mídia**: O **Rhythmbox** é o player de música padrão no GNOME.

---

### **Parando o GNOME 3**
Para encerrar a sessão no GNOME 3:
- Clicar na **seta para baixo** no canto superior direito e selecionar **Desligar ou Logout**.

---

### **O Desktop GNOME 2**
O **GNOME 2** era o ambiente padrão até o **RHEL 6** e versões antigas do Fedora e Ubuntu. Ele tem um layout mais tradicional, com:
- **Painéis superiores e inferiores** para atalhos e notificações.
- **Gerenciador de janelas Metacity**.
- **Sistema de menus clássico** (Aplicações, Locais e Sistema).

O GNOME 2 pode ser personalizado com:
- **Mudança de temas e ícones**.
- **Adição de applets e painéis extras**.

---

### **Adicionando Efeitos 3D com AIGLX**
O **AIGLX** é uma tecnologia que permite efeitos 3D no GNOME 2, usando o **Compiz** como gerenciador de janelas. Alguns efeitos incluem:
- Janelas gelatinosas.
- Alternância animada entre áreas de trabalho.
- Efeitos de transparência.