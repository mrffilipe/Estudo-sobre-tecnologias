
# Filtros no Docker CLI

## Visão Geral
O Docker CLI oferece suporte a filtros para refinar os resultados de comandos que listam objetos, como containers, imagens, volumes, e redes. Os filtros permitem que você selecione objetos específicos com base em critérios como status, nome, rótulos, e outros atributos, tornando a gestão de recursos Docker mais eficiente.

## 1. Comandos que Suportam Filtros

### Comandos Comuns
- `docker ps`: Lista os containers em execução ou parados.
- `docker images`: Lista as imagens Docker.
- `docker volume ls`: Lista volumes Docker.
- `docker network ls`: Lista redes Docker.

### Uso do Parâmetro `--filter`
- O parâmetro `--filter` pode ser adicionado a esses comandos para aplicar filtros aos resultados listados.
- Sintaxe básica:

```bash
docker <command> --filter <filter=value>
```

## 2. Exemplos de Filtros Comuns

### Filtrando Containers por Status
- Para listar apenas containers em execução:

```bash
docker ps --filter "status=running"
```

- Para listar apenas containers parados:

```bash
docker ps --filter "status=exited"
```

### Filtrando Containers por Nome
- Para listar containers cujo nome contém uma string específica:

```bash
docker ps --filter "name=myapp"
```

### Filtrando Containers por Rótulos (Labels)
- Para listar containers com um rótulo específico:

```bash
docker ps --filter "label=com.example.version=1.0"
```

### Filtrando Imagens por Dangling (Imagens Não Referenciadas)
- Para listar apenas imagens que não estão sendo referenciadas por nenhum container:

```bash
docker images --filter "dangling=true"
```

### Filtrando Volumes por Uso
- Para listar volumes que não estão em uso por nenhum container:

```bash
docker volume ls --filter "dangling=true"
```

## 3. Combinação de Múltiplos Filtros

### Uso de Múltiplos Filtros Simultâneos
- Você pode combinar vários filtros em um único comando para refinar ainda mais os resultados.
- Exemplo:

```bash
docker ps --filter "status=running" --filter "label=com.example.env=production"
```

- Esse comando lista containers que estão em execução e têm o rótulo `com.example.env=production`.

## 4. Casos de Uso Comuns

### Gerenciamento de Containers em Produção
- Use filtros para localizar rapidamente containers críticos com base em status, nome, ou rótulos, facilitando a administração em ambientes de produção.

### Limpeza de Imagens e Volumes
- Filtros como `dangling=true` são úteis para identificar e remover imagens ou volumes que não estão mais em uso, liberando espaço em disco.

### Auditoria e Monitoramento
- Aplique filtros para auditar o estado atual dos recursos Docker, garantindo conformidade com políticas de infraestrutura.

## 5. Considerações de Boas Práticas

### Uso Regular de Filtros
- Habitue-se a usar filtros regularmente para refinar os resultados e tornar a administração de recursos Docker mais eficiente.

### Combinação de Filtros
- Aproveite a possibilidade de combinar múltiplos filtros para obter resultados altamente específicos.

### Automatização
- Integre filtros em scripts automatizados para gerenciar recursos Docker de maneira eficaz, especialmente em ambientes grandes ou complexos.

## Dicas de Boas Práticas
- Utilize filtros para otimizar o gerenciamento de recursos Docker e evitar sobrecarga de informações.
- Combine múltiplos filtros para obter resultados precisos e específicos, facilitando a administração em larga escala.
- Automatize processos que envolvam o uso de filtros para garantir consistência e eficiência na gestão de containers, imagens, volumes e redes.

