
# Docker Engine

## Visão Geral
O Docker Engine é o principal componente da plataforma Docker. Ele é responsável por criar, executar e gerenciar containers em um ambiente isolado. O Docker Engine é composto por três partes principais: **Docker Daemon**, **REST API** e **Docker CLI**.

## Docker Daemon
O Docker Daemon é o serviço principal que gerencia os containers no sistema.

- Ele ouve as requisições da Docker API e gerencia objetos Docker como containers, imagens, volumes e redes.
- Normalmente é executado como um processo de segundo plano e pode ser configurado para iniciar automaticamente com o sistema.

## Docker REST API
A REST API do Docker é a interface utilizada para interagir com o Docker Daemon programaticamente.

- É possível gerenciar os containers, imagens, volumes e redes através de chamadas HTTP para a API.
- A API suporta diferentes versões e, ao fazer uma chamada, é possível especificar a versão desejada para compatibilidade.

## Docker CLI
A Docker CLI (Command Line Interface) é a ferramenta de linha de comando que permite interagir diretamente com o Docker.

- Comandos básicos incluem:
  - `docker run`: Executa um container a partir de uma imagem.
  - `docker build`: Constrói uma imagem a partir de um Dockerfile.
  - `docker pull`: Baixa uma imagem do Docker Hub ou de outro registro.
  - `docker push`: Envia uma imagem para um registro.

## Imagens Docker
**Imagens Docker** são templates de leitura que contêm tudo o que é necessário para rodar um container.

- As imagens são construídas a partir de um **Dockerfile**, que descreve as instruções para criar a imagem.
- As imagens podem ser armazenadas localmente ou em um registro como o Docker Hub.

## Containers Docker
Containers são instâncias em execução de imagens Docker.

- Eles compartilham o kernel do sistema host e outros recursos, mas são isolados no nível de processo e rede.
- Containers são leves e iniciam rapidamente, o que os torna ideais para ambientes de produção e desenvolvimento.

## Volumes Docker
Volumes são o mecanismo preferido para persistir dados gerados e utilizados por containers.

- Eles são gerenciados pelo Docker e podem ser montados em containers para compartilhar dados entre eles ou com o host.
- Volumes oferecem uma maneira de manter os dados fora do ciclo de vida dos containers, garantindo que os dados persistam mesmo que o container seja removido.

## Redes Docker
Docker oferece várias opções de rede para containers, incluindo redes bridge, host, none, e redes definidas pelo usuário.

- Cada rede permite diferentes níveis de isolamento e conectividade entre containers, e entre containers e o host.
- É possível criar redes customizadas para organizar a comunicação entre múltiplos containers.

## Registros Docker
Registros são locais onde as imagens Docker são armazenadas e distribuídas.

- O Docker Hub é o registro público padrão, mas é possível configurar registros privados para uso interno.
- Registros permitem versionamento das imagens e facilitam a distribuição em ambientes de produção.

## Segurança no Docker
Docker oferece várias camadas de segurança para proteger containers e o ambiente host.

- Recomenda-se o uso de **userspaces** para containers, o isolamento de processos com cgroups e namespaces, e a assinatura de imagens para garantir a integridade.
- Docker também suporta a criação de **policies** e **profiles** de segurança para controle mais granular sobre o comportamento dos containers.

## Monitoramento e Logs
Docker oferece ferramentas para monitorar a performance dos containers e coletar logs.

- Logs podem ser acessados através da CLI ou enviados para sistemas de logging externos.
- Monitoramento de recursos como CPU, memória e rede é possível através de comandos ou ferramentas como o Docker Stats.

## Dicas de Boas Práticas
- Mantenha o Docker Engine sempre atualizado para garantir a segurança e eficiência do sistema.
- Utilize volumes para persistência de dados de maneira eficiente e segura.
- Configure redes personalizadas para ambientes de múltiplos containers, garantindo segurança e isolamento adequado.
