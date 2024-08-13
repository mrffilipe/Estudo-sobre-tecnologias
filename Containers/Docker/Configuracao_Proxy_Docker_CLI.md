
# Configuração de Proxy no Docker CLI

## Visão Geral
O Docker CLI permite configurar proxies HTTP/HTTPS para que os containers e o Docker daemon possam acessar a internet em ambientes onde o acesso é restrito por um proxy. A configuração de proxy é essencial em ambientes corporativos ou redes que exigem o uso de um proxy para acessar recursos externos, como registros de imagens Docker.

## 1. Configurando Proxy para Containers

### Variáveis de Ambiente
- A configuração de proxy para containers é feita através de variáveis de ambiente que são passadas durante a execução de um container.
- As variáveis comuns incluem:
  - `HTTP_PROXY` ou `http_proxy`: Define o proxy HTTP.
  - `HTTPS_PROXY` ou `https_proxy`: Define o proxy HTTPS.
  - `NO_PROXY` ou `no_proxy`: Define uma lista de endereços ou domínios que não devem usar o proxy.

### Exemplo de Uso
- Para passar as variáveis de proxy ao executar um container:

```bash
docker run -e "HTTP_PROXY=http://proxy.example.com:8080" -e "HTTPS_PROXY=https://proxy.example.com:8080" -e "NO_PROXY=localhost,127.0.0.1" nginx
```

- Neste exemplo, o container `nginx` usará os proxies definidos para acessar recursos externos.

## 2. Configurando Proxy para o Docker Daemon

### Arquivo de Configuração do Docker Daemon
- O Docker daemon também pode ser configurado para usar um proxy. Isso é feito editando o arquivo de configuração `daemon.json`, geralmente localizado em `/etc/docker/` ou `/etc/docker/daemon.json`.

### Exemplo de Configuração
- Adicione as seguintes linhas ao arquivo `daemon.json` para configurar o proxy:

```json
{
  "proxies": {
    "default": {
      "httpProxy": "http://proxy.example.com:8080",
      "httpsProxy": "https://proxy.example.com:8080",
      "noProxy": "localhost,127.0.0.1"
    }
  }
}
```

- Após salvar as alterações, reinicie o Docker daemon para aplicar as novas configurações:

```bash
sudo systemctl restart docker
```

## 3. Configuração de Proxy Persistente

### Persistência de Variáveis de Ambiente
- Para garantir que as variáveis de ambiente de proxy sejam persistentes em todas as execuções de containers, você pode adicioná-las aos arquivos de configuração de shell, como `.bashrc`, `.bash_profile`, ou `.zshrc`.

### Exemplo para Bash
- Adicione as seguintes linhas ao arquivo `.bashrc` ou `.bash_profile`:

```bash
export HTTP_PROXY="http://proxy.example.com:8080"
export HTTPS_PROXY="https://proxy.example.com:8080"
export NO_PROXY="localhost,127.0.0.1"
```

- Após salvar, recarregue o perfil:

```bash
source ~/.bashrc
```

## 4. Considerações de Segurança

### Proteção de Credenciais
- Se o proxy exigir autenticação, é importante proteger as credenciais. Evite armazenar senhas em texto plano nos arquivos de configuração. Use variáveis de ambiente ou arquivos de configuração seguros para gerenciar credenciais.

### Controle de Acesso
- Certifique-se de que o acesso ao proxy está devidamente controlado e monitorado para evitar o uso não autorizado ou a exposição de dados sensíveis.

## 5. Depuração e Testes

### Verificação de Conectividade
- Após configurar o proxy, é importante testar a conectividade para garantir que os containers e o Docker daemon conseguem acessar os recursos externos conforme esperado.

### Testando dentro de um Container
- Execute um container e teste a conexão com a internet:

```bash
docker run --rm -e "HTTP_PROXY=http://proxy.example.com:8080" curl -I http://www.google.com
```

- Isso permite verificar se o container está utilizando o proxy corretamente.

## Dicas de Boas Práticas
- Proteja as credenciais de proxy para evitar exposição acidental.
- Teste a configuração de proxy após a implementação para garantir que está funcionando corretamente.
- Mantenha o arquivo de configuração do Docker daemon atualizado e sob controle de versão para garantir consistência em todos os ambientes.

