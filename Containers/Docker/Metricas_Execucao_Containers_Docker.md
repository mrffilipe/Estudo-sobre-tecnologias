
# Métricas de Execução de Containers no Docker

## Visão Geral
O monitoramento das métricas de execução dos containers é essencial para garantir o desempenho e a estabilidade dos serviços executados em containers Docker. O Docker fornece várias ferramentas e comandos para visualizar e analisar essas métricas em tempo real, permitindo uma melhor gestão dos recursos do sistema.

## 1. Comando `docker stats`

### Descrição
- O comando `docker stats` exibe métricas em tempo real para os containers em execução. Essas métricas incluem uso de CPU, memória, I/O de bloco, e rede.

### Sintaxe
- O comando básico é:

```bash
docker stats [OPTIONS] [CONTAINER...]
```

- Se nenhum container for especificado, o comando mostrará as métricas para todos os containers em execução.

### Exemplo de Uso
- Para visualizar métricas de um container específico:

```bash
docker stats meu-container
```

- Para visualizar métricas de todos os containers:

```bash
docker stats
```

### Principais Métricas
- **CPU %**: Porcentagem de uso da CPU pelo container.
- **MEM USAGE / LIMIT**: Uso de memória pelo container em relação ao limite configurado.
- **MEM %**: Porcentagem de memória utilizada pelo container.
- **NET I/O**: Quantidade de dados enviados e recebidos pelo container.
- **BLOCK I/O**: Quantidade de dados lidos e escritos no disco pelo container.
- **PIDS**: Número de processos ou threads em execução no container.

## 2. Monitoramento de Métricas com APIs e Ferramentas de Terceiros

### APIs do Docker
- As métricas dos containers também podem ser acessadas programaticamente usando a API do Docker. As APIs permitem que desenvolvedores e administradores integrem o monitoramento de métricas com sistemas externos de monitoramento.

### Ferramentas de Terceiros
- Existem várias ferramentas de monitoramento de terceiros que se integram com o Docker, como Prometheus, Grafana, e Datadog. Essas ferramentas oferecem visualizações avançadas e alertas para ajudar a monitorar a saúde e o desempenho dos containers.

## 3. Coleta de Métricas com Prometheus

### Exportador de Métricas para Docker
- O `cAdvisor` (Container Advisor) é uma ferramenta amplamente utilizada para coletar métricas de containers e exportá-las para o Prometheus. Ele coleta informações sobre uso de CPU, memória, I/O de bloco, e rede, e as disponibiliza em um formato que o Prometheus pode consumir.

### Exemplo de Configuração
- Para configurar o `cAdvisor` em um container:

```bash
docker run   --volume=/:/rootfs:ro   --volume=/var/run:/var/run:ro   --volume=/sys:/sys:ro   --volume=/var/lib/docker/:/var/lib/docker:ro   --publish=8080:8080   --detach=true   --name=cadvisor   google/cadvisor:latest
```

- Em seguida, configure o Prometheus para raspar as métricas do `cAdvisor`.

## 4. Considerações de Boas Práticas

### Monitoramento Contínuo
- É crucial monitorar continuamente as métricas de execução dos containers para identificar gargalos de desempenho e problemas antes que afetem o ambiente de produção.

### Ajustes Dinâmicos
- Utilize as métricas coletadas para ajustar dinamicamente os limites de recursos dos containers e otimizar o desempenho.

### Alertas e Notificações
- Configure alertas baseados em limites críticos de métricas (como uso excessivo de CPU ou memória) para notificar administradores e permitir uma resposta rápida a problemas emergentes.

## 5. Casos de Uso Comuns

### Detecção de Gargalos de Desempenho
- Identificar containers que estão consumindo mais recursos do que o esperado, permitindo ajustes proativos.

### Otimização de Recursos
- Monitorar e ajustar o uso de recursos para maximizar a eficiência do sistema e reduzir custos de infraestrutura.

### Garantia de SLA
- Usar métricas para garantir que os containers estejam operando dentro dos níveis de serviço acordados (SLAs), evitando violações e penalidades.

## Dicas de Boas Práticas
- Utilize ferramentas como Prometheus e Grafana para um monitoramento mais avançado e visualização das métricas.
- Monitore constantemente o uso de recursos e ajuste as configurações conforme necessário.
- Estabeleça alertas para detectar anomalias no uso de recursos e agir rapidamente para evitar problemas maiores.

