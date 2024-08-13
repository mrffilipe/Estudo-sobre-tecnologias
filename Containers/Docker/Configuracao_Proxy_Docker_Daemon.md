
# Configuração de Proxy no Docker Daemon

## Visão Geral
Configurar um proxy no Docker daemon é essencial em ambientes onde o acesso à internet é restrito e precisa passar por um proxy. Essa configuração garante que o Docker daemon possa baixar imagens, acessar registros e realizar outras operações que dependem da internet. O Docker permite configurar proxies HTTP, HTTPS e ignorar o proxy para determinados endereços.

## 1. Configuração do Proxy no Docker Daemon

### Configuração Através do Arquivo `daemon.json`
- Para configurar o proxy, você precisa editar o arquivo `daemon.json`, que geralmente está localizado em `/etc/docker/daemon.json`.

- Exemplo de configuração para adicionar um proxy:

```json
{
  "proxies": {
    "default": {
      "httpProxy": "http://proxy.example.com:80",
      "httpsProxy": "https://proxy.example.com:443",
      "noProxy": "localhost,127.0.0.1,.example.com"
    }
  }
}
```

### Variáveis de Ambiente
- Alternativamente, você pode configurar o proxy usando variáveis de ambiente. Essas variáveis devem ser exportadas no ambiente onde o Docker daemon será iniciado:

```bash
export HTTP_PROXY="http://proxy.example.com:80"
export HTTPS_PROXY="https://proxy.example.com:443"
export NO_PROXY="localhost,127.0.0.1,.example.com"
```

### Aplicando as Configurações
- Após configurar o proxy no `daemon.json`, você precisa reiniciar o Docker daemon para aplicar as mudanças:

```bash
sudo systemctl restart docker
```

## 2. Configuração do Proxy para Containers

### Propagação do Proxy para Containers
- Os proxies configurados no Docker daemon podem ser automaticamente propagados para os containers que ele gerencia. Isso é útil para garantir que todos os containers tenham acesso à internet através do proxy configurado.

- No `daemon.json`, você pode configurar a propagação do proxy com a seguinte sintaxe:

```json
{
  "proxies": {
    "default": {
      "httpProxy": "http://proxy.example.com:80",
      "httpsProxy": "https://proxy.example.com:443",
      "noProxy": "localhost,127.0.0.1,.example.com"
    }
  },
  "env": {
    "HTTP_PROXY": "http://proxy.example.com:80",
    "HTTPS_PROXY": "https://proxy.example.com:443",
    "NO_PROXY": "localhost,127.0.0.1,.example.com"
  }
}
```

## 3. Considerações de Segurança

### Autenticação no Proxy
- Se o proxy exigir autenticação, as credenciais devem ser fornecidas na URL do proxy:

```json
{
  "httpProxy": "http://username:password@proxy.example.com:80"
}
```

- Certifique-se de que as credenciais são armazenadas com segurança e que o arquivo `daemon.json` tem permissões restritas para evitar exposição acidental.

### Evitar Exposição de Credenciais
- Quando possível, evite armazenar credenciais em texto plano no `daemon.json`. Considere o uso de ferramentas de gerenciamento de segredos ou variáveis de ambiente para proteger as credenciais.

## 4. Solução de Problemas

### Verificando a Configuração
- Após configurar o proxy, você pode verificar se ele está sendo usado corretamente ao executar comandos como `docker pull` e monitorar se o tráfego está passando pelo proxy.

### Logs e Depuração
- Se o Docker daemon não conseguir acessar a internet através do proxy, verifique os logs para possíveis erros. Os logs podem ser acessados com:

```bash
journalctl -u docker.service
```

## 5. Casos de Uso Comuns

### Ambientes Corporativos
- Configurar um proxy é comum em ambientes corporativos onde o acesso direto à internet é restrito e deve ser canalizado através de um proxy.

### Desenvolvimento e Teste
- Em ambientes de desenvolvimento que simulam restrições de rede, configurar um proxy pode ajudar a testar como as aplicações se comportam em tais condições.

### Produção
- Garantir que o Docker daemon e os containers tenham acesso estável à internet através de um proxy configurado corretamente é crucial para a operação contínua em ambientes de produção.

## Dicas de Boas Práticas
- Certifique-se de que o proxy configurado está devidamente testado em ambientes de desenvolvimento antes de aplicar em produção.
- Proteja as credenciais de proxy utilizando variáveis de ambiente ou ferramentas de gerenciamento de segredos.
- Monitore a conectividade do Docker daemon e dos containers para garantir que o proxy esteja funcionando corretamente.

