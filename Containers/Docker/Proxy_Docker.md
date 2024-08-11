
# Proxy no Docker

## Visão Geral
O Docker permite configurar proxies HTTP/HTTPS para containers e para o daemon do Docker. Isso é útil em ambientes corporativos ou em redes onde o acesso à internet é restrito ou filtrado por proxies. Configurar um proxy garante que os containers e o daemon possam acessar recursos externos, como registros de imagens e serviços web, através da rede restrita.

## Configurando um Proxy para Containers

### Definição de Variáveis de Ambiente
- Para que os containers utilizem um proxy, você pode definir as variáveis de ambiente `HTTP_PROXY`, `HTTPS_PROXY` e `NO_PROXY` ao executar um container.
- Exemplo:

```bash
docker run -e "HTTP_PROXY=http://proxy.example.com:8080" -e "HTTPS_PROXY=https://proxy.example.com:8080" -e "NO_PROXY=localhost,127.0.0.1" nginx
```

### Definição no Dockerfile
- As variáveis de proxy também podem ser definidas diretamente no `Dockerfile`, o que garante que todos os containers criados a partir dessa imagem utilizem o proxy configurado.
- Exemplo:

```Dockerfile
ENV HTTP_PROXY=http://proxy.example.com:8080
ENV HTTPS_PROXY=https://proxy.example.com:8080
ENV NO_PROXY=localhost,127.0.0.1
```

## Configurando um Proxy para o Docker Daemon

### Arquivo de Configuração do Daemon
- Você pode configurar o Docker daemon para utilizar um proxy ao acessar a internet. Isso é feito editando o arquivo de configuração do daemon, geralmente localizado em `/etc/systemd/system/docker.service.d/` ou `/etc/docker/daemon.json`.
- Exemplo para `/etc/systemd/system/docker.service.d/http-proxy.conf`:

```ini
[Service]
Environment="HTTP_PROXY=http://proxy.example.com:8080/"
Environment="HTTPS_PROXY=https://proxy.example.com:8080/"
Environment="NO_PROXY=localhost,127.0.0.1"
```

### Configuração via JSON
- Também é possível configurar o proxy no arquivo `daemon.json`.
- Exemplo:

```json
{
  "proxies":
  {
    "default":
    {
      "httpProxy": "http://proxy.example.com:8080",
      "httpsProxy": "https://proxy.example.com:8080",
      "noProxy": "localhost,127.0.0.1"
    }
  }
}
```

### Reiniciando o Docker Daemon
- Após configurar o proxy, é necessário reiniciar o daemon para que as mudanças entrem em vigor:

```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## Configuração de Proxy para Builds

### Passando Variáveis de Proxy para o Build
- Quando você executa `docker build`, as variáveis de proxy podem ser passadas usando a flag `--build-arg`.
- Exemplo:

```bash
docker build --build-arg HTTP_PROXY=http://proxy.example.com:8080 --build-arg HTTPS_PROXY=https://proxy.example.com:8080 -t minha-imagem .
```

### Persistência de Proxy no Dockerfile
- Você também pode definir variáveis de proxy no Dockerfile para que cada etapa do build utilize o proxy configurado.
- Exemplo:

```Dockerfile
ARG HTTP_PROXY
ARG HTTPS_PROXY
ENV http_proxy=$HTTP_PROXY
ENV https_proxy=$HTTPS_PROXY
```

## Considerações de Segurança

### Proteção de Credenciais
- Se o proxy exige autenticação, as credenciais devem ser protegidas. Evite colocar credenciais diretamente no Dockerfile ou no código-fonte.
- Utilize variáveis de ambiente ou arquivos de configuração seguros para gerenciar credenciais de proxy.

### Controle de Acesso
- Certifique-se de que o acesso ao proxy está devidamente restrito e monitorado para evitar o uso não autorizado ou a exposição de dados sensíveis.

## Depuração e Teste

### Verificando Conectividade
- Após configurar o proxy, teste a conectividade de um container ou do daemon Docker para garantir que o proxy esteja funcionando corretamente.
- Exemplo para testar dentro de um container:

```bash
docker run --rm -e "HTTP_PROXY=http://proxy.example.com:8080" curl -I http://www.google.com
```

### Logs e Diagnósticos
- Verifique os logs do Docker daemon e dos containers para diagnosticar possíveis problemas relacionados à configuração do proxy.

## Casos de Uso Comuns

### Ambientes Corporativos
- Configuração de proxies é essencial em ambientes onde o acesso à internet é controlado por políticas corporativas.

### Desenvolvimento Local com Restrição de Rede
- Desenvolvedores que trabalham em redes restritas podem configurar proxies para garantir que os containers e builds Docker tenham acesso a recursos externos.

## Dicas de Boas Práticas
- Mantenha as credenciais de proxy seguras e utilize variáveis de ambiente para evitar exposições acidentais.
- Sempre teste a conectividade após configurar um proxy para garantir que os containers possam acessar os recursos necessários.
- Revise regularmente as configurações de proxy para garantir que estejam atualizadas e seguras.
