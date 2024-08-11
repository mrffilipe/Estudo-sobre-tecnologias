
# Instalação do Docker Engine

## Visão Geral
O Docker Engine pode ser instalado em várias distribuições Linux, assim como em sistemas Windows e macOS. A instalação pode ser realizada utilizando repositórios oficiais do Docker, e é recomendável seguir os passos específicos para cada sistema operacional para garantir uma instalação correta e atualizada.

## Instalação no Linux
O Docker Engine está disponível para as seguintes distribuições Linux: Ubuntu, Debian, Fedora, CentOS, RHEL e SUSE.

### Passos Gerais de Instalação:
1. **Atualização do Sistema**:
   - Antes de instalar o Docker, atualize seu sistema com os comandos adequados, como `sudo apt-get update` para sistemas baseados em Debian/Ubuntu.
   
2. **Instalação de Pacotes de Pré-requisitos**:
   - Instale pacotes como `apt-transport-https`, `ca-certificates`, `curl`, `gnupg`, e `lsb-release`.

3. **Adição do Repositório Docker**:
   - Adicione a chave GPG oficial do Docker e o repositório usando comandos como `curl` e `add-apt-repository`.

4. **Instalação do Docker Engine**:
   - Instale o Docker Engine, Docker CLI, e Containerd com o comando `sudo apt-get install docker-ce docker-ce-cli containerd.io`.

5. **Iniciar e Configurar Docker**:
   - Inicie o serviço do Docker com `sudo systemctl start docker`.
   - Opcionalmente, configure o Docker para iniciar automaticamente no boot com `sudo systemctl enable docker`.

6. **Verificação da Instalação**:
   - Verifique se o Docker foi instalado corretamente executando `docker --version` e rodando um container de teste com `sudo docker run hello-world`.

## Instalação no Windows e macOS
Para instalar o Docker Engine no **Windows** e **macOS**, utiliza-se o Docker Desktop, que já inclui o Docker Engine.

### Passos:
1. Baixe o Docker Desktop do site oficial.
2. Siga as instruções do instalador.
3. Após a instalação, você pode verificar o Docker Engine com os mesmos comandos que no Linux (`docker --version` e `docker run hello-world`).

## Instalação Usando Scripts Automáticos
O Docker fornece scripts que podem ser usados para instalar o Docker Engine automaticamente.

- Para Linux, o comando `curl -fsSL https://get.docker.com -o get-docker.sh` seguido de `sh get-docker.sh` instala o Docker automaticamente.

## Atualização do Docker Engine
Para manter o Docker atualizado, use os comandos de atualização da sua distribuição Linux (como `sudo apt-get update` seguido de `sudo apt-get upgrade` em sistemas Debian/Ubuntu).

- No Windows e macOS, o Docker Desktop notifica automaticamente quando há atualizações disponíveis.

## Desinstalação
Para desinstalar o Docker, remova os pacotes Docker e qualquer configuração residual.

- No Linux, você pode usar `sudo apt-get purge docker-ce docker-ce-cli containerd.io` para remoção completa.
- Em Windows e macOS, utilize as opções de desinstalação padrão do sistema operacional.

## Dicas de Boas Práticas
- Verifique sempre as notas de versão antes de atualizar o Docker Engine.
- Mantenha seu sistema operacional e pacotes de pré-requisitos atualizados para garantir a compatibilidade.
- Após a instalação, crie e teste um container com `hello-world` para garantir que tudo esteja funcionando corretamente.
