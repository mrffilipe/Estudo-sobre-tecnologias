
# Iniciando Containers Automaticamente no Docker

## Visão Geral
O Docker oferece funcionalidades que permitem que containers sejam iniciados automaticamente após uma reinicialização do Docker daemon ou do host. Isso é particularmente útil para garantir a disponibilidade contínua de serviços em containers, mesmo após falhas ou reinicializações planejadas.

## 1. Políticas de Reinício (Restart Policies)

### Tipos de Políticas de Reinício

#### no
- O container não será reiniciado automaticamente.
- Exemplo:

```bash
docker run --restart no nginx
```

#### on-failure
- O container será reiniciado apenas se falhar (se o código de saída for diferente de zero).
- Exemplo:

```bash
docker run --restart on-failure nginx
```

- Você pode especificar um número máximo de reinicializações:

```bash
docker run --restart on-failure:5 nginx
```

#### always
- O container sempre será reiniciado, independentemente do código de saída.
- Exemplo:

```bash
docker run --restart always nginx
```

#### unless-stopped
- Similar à política `always`, mas o container não será reiniciado se tiver sido parado manualmente.
- Exemplo:

```bash
docker run --restart unless-stopped nginx
```

## 2. Configurando Políticas de Reinício em Containers Existentes

### Atualizando um Container Existente
- Você pode atualizar a política de reinício de um container existente usando o comando `docker update`:

```bash
docker update --restart always meu-container
```

## 3. Considerações de Boas Práticas

### Escolha da Política de Reinício
- A escolha da política de reinício depende da criticidade do serviço rodando no container. Para serviços essenciais, `always` ou `unless-stopped` são boas escolhas para garantir alta disponibilidade.

### Monitoramento e Logs
- Mesmo com políticas de reinício, é importante monitorar containers para identificar falhas recorrentes e resolver as causas subjacentes. Utilize ferramentas de monitoramento e agregação de logs para este fim.

### Limites de Reinício
- Se optar por `on-failure`, defina um limite de reinicializações para evitar loops de falha e reinício, que podem sobrecarregar o sistema.

## 4. Casos de Uso Comuns

### Serviços Críticos em Produção
- Para garantir que serviços críticos estejam sempre disponíveis, configure containers com a política `always` ou `unless-stopped`.

### Ambientes de Desenvolvimento
- Em ambientes de desenvolvimento, `on-failure` pode ser útil para diagnosticar problemas sem reiniciar automaticamente em caso de paradas manuais.

### Tarefas em Background
- Para containers que executam tarefas periódicas ou em segundo plano, `unless-stopped` pode ser adequado para garantir que eles não sejam reiniciados desnecessariamente.

## Dicas de Boas Práticas
- Escolha a política de reinício adequada ao contexto do serviço.
- Monitore os containers mesmo com políticas de reinício configuradas para identificar problemas recorrentes.
- Defina limites para reinicializações em casos de falhas contínuas para evitar loops indesejados.

