
# Executando Containers com Docker

## Visão Geral
O comando `docker run` é o principal comando utilizado para criar e executar containers no Docker. Ele combina as funcionalidades de criação e inicialização de containers, possibilitando o uso de diversas opções para configurar a execução de containers de acordo com as necessidades específicas.

## Estrutura Básica do Comando
A sintaxe básica do comando `docker run` é:

```bash
docker run [OPÇÕES] IMAGEM [COMANDO] [ARGUMENTOS...]
```

- **IMAGEM**: A imagem Docker a partir da qual o container será criado.
- **COMANDO**: O comando que será executado dentro do container.
- **ARGUMENTOS**: Argumentos adicionais para o comando especificado.

## Opções Importantes para Executar Containers

### -d, --detach
- Executa o container em segundo plano (modo detached).
- Exemplo:

```bash
docker run -d nginx
```

### -p, --publish
- Mapeia uma porta do host para uma porta no container.
- Exemplo:

```bash
docker run -p 8080:80 nginx
```

### -e, --env
- Define variáveis de ambiente no container.
- Exemplo:

```bash
docker run -e "VARIAVEL=valor" nginx
```

### -v, --volume
- Monta um volume do host no container.
- Exemplo:

```bash
docker run -v /meu/diretorio:/diretorio/no/container nginx
```

### --network
- Conecta o container a uma rede Docker específica.
- Exemplo:

```bash
docker run --network minha-rede nginx
```

### --name
- Atribui um nome ao container, facilitando seu gerenciamento.
- Exemplo:

```bash
docker run --name meu-container nginx
```

### --rm
- Remove o container automaticamente após a finalização.
- Exemplo:

```bash
docker run --rm nginx
```

## Gerenciamento de Recursos

### -m, --memory
- Define o limite máximo de memória que o container pode utilizar.
- Exemplo:

```bash
docker run -m 512m nginx
```

### --cpus
- Limita o número de CPUs que o container pode usar.
- Exemplo:

```bash
docker run --cpus="2.0" nginx
```

## Políticas de Reinício (Restart Policies)

### --restart
- Define a política de reinício do container.
- Exemplo:

```bash
docker run --restart unless-stopped nginx
```

- Opções:
  - `no`: Não reinicia o container automaticamente.
  - `on-failure`: Reinicia o container se ele falhar.
  - `always`: Sempre reinicia o container se ele parar.
  - `unless-stopped`: Reinicia o container, exceto se ele for explicitamente parado.

## Comando e Argumentos

### Sobrescrevendo o Comando Padrão
- Você pode sobrescrever o comando padrão especificado no `Dockerfile` diretamente no comando `docker run`.
- Exemplo:

```bash
docker run nginx echo "Hello, World!"
```

### Argumentos Adicionais
- Você pode passar argumentos adicionais para o comando especificado.
- Exemplo:

```bash
docker run ubuntu ls -l /home
```

## Exemplo de Comando Completo

### Comando Completo

```bash
docker run -d -p 8080:80 --name meu-webserver --network minha-rede --rm nginx
```

### Explicação

- `-d`: Executa o container em segundo plano.
- `-p 8080:80`: Mapeia a porta 8080 do host para a porta 80 do container.
- `--name meu-webserver`: Nomeia o container como `meu-webserver`.
- `--network minha-rede`: Conecta o container à rede `minha-rede`.
- `--rm`: Remove o container após a finalização.
- `nginx`: Usa a imagem `nginx` para criar o container.

## Considerações e Boas Práticas

### Gestão de Nomes e Volumes
- Nomeie seus containers e volumes de forma consistente para facilitar a gestão e manutenção.

### Limitação de Recursos
- Sempre que possível, limite o uso de recursos (CPU e memória) para evitar que um único container afete o desempenho do host.

### Políticas de Reinício
- Use políticas de reinício para garantir a disponibilidade dos serviços em containers de produção.

