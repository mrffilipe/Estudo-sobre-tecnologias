
# Limpeza de Recursos no Docker

## Visão Geral
A limpeza de recursos no Docker é uma prática essencial para manter o sistema otimizado e evitar o acúmulo de dados não utilizados, como containers parados, imagens não referenciadas, volumes e redes não utilizados. O Docker CLI oferece comandos específicos para realizar essa limpeza de forma segura e eficiente.

## 1. Comando `docker system prune`

### Descrição
- O comando `docker system prune` é utilizado para remover todos os objetos não utilizados no sistema Docker, incluindo containers parados, imagens não referenciadas, volumes e redes não utilizados.

### Sintaxe Básica
- Para realizar uma limpeza completa:

```bash
docker system prune
```

- O comando solicitará confirmação antes de proceder com a limpeza.

### Remoção Forçada
- Para executar o comando sem solicitar confirmação:

```bash
docker system prune -f
```

### Incluir Volumes
- Por padrão, os volumes não utilizados não são removidos. Para incluí-los na limpeza:

```bash
docker system prune --volumes
```

## 2. Comandos Específicos para Limpeza

### Limpeza de Containers Parados
- Para remover todos os containers que não estão em execução:

```bash
docker container prune
```

### Limpeza de Imagens Não Referenciadas
- Para remover todas as imagens que não estão sendo utilizadas por nenhum container:

```bash
docker image prune
```

- Para remover todas as imagens não utilizadas, incluindo as intermediárias:

```bash
docker image prune -a
```

### Limpeza de Volumes Não Utilizados
- Para remover todos os volumes que não estão sendo utilizados por nenhum container:

```bash
docker volume prune
```

### Limpeza de Redes Não Utilizadas
- Para remover todas as redes que não estão sendo utilizadas por nenhum container:

```bash
docker network prune
```

## 3. Considerações de Segurança e Precauções

### Verificação Antes da Limpeza
- Sempre verifique quais recursos serão removidos antes de executar os comandos de limpeza, especialmente em ambientes de produção.

### Evitar Perda de Dados
- Ao remover volumes ou imagens, certifique-se de que não há dados ou dependências importantes sendo removidas inadvertidamente.

### Uso de Opções Específicas
- Utilize as opções específicas de cada comando (`--volumes`, `-a`, etc.) para personalizar a limpeza de acordo com as necessidades do sistema.

## 4. Casos de Uso Comuns

### Manutenção de Servidores de Desenvolvimento
- Realizar limpezas regulares em servidores de desenvolvimento para liberar espaço em disco e evitar o acúmulo de recursos obsoletos.

### Otimização de Ambientes de Produção
- Em ambientes de produção, use `docker system prune` com cautela para garantir que apenas recursos verdadeiramente obsoletos sejam removidos.

### Preparação para Backups
- Antes de realizar backups, execute uma limpeza para garantir que apenas dados relevantes e em uso sejam incluídos no processo.

## Dicas de Boas Práticas
- Execute `docker system prune` regularmente em ambientes de desenvolvimento para manter o sistema limpo e eficiente.
- Em ambientes de produção, verifique sempre os recursos que serão removidos para evitar a exclusão de dados importantes.
- Utilize comandos específicos como `docker volume prune` e `docker image prune -a` para realizar limpezas mais direcionadas e seguras.

