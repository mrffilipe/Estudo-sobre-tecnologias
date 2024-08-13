
# Restrições de Recursos em Containers Docker

## Visão Geral
Ao executar containers, é essencial controlar o uso de recursos como CPU, memória, e I/O para garantir que nenhum container monopolize os recursos do host, o que pode comprometer a estabilidade e o desempenho geral do sistema. O Docker oferece várias opções para aplicar restrições de recursos aos containers, ajudando a gerenciar a alocação de recursos de forma eficiente.

## 1. Limitação de CPU

### --cpus
- Define a quantidade de CPU que o container pode usar.
- Exemplo:

```bash
docker run --cpus="1.5" nginx
```

- Esse comando limita o container a usar 1.5 CPUs.

### --cpu-shares
- Define a prioridade relativa do uso da CPU entre os containers.
- Exemplo:

```bash
docker run --cpu-shares=512 nginx
```

- Containers com valores de `cpu-shares` mais altos terão maior prioridade na alocação de CPU.

### --cpuset-cpus
- Especifica quais núcleos de CPU o container pode usar.
- Exemplo:

```bash
docker run --cpuset-cpus="0,1" nginx
```

- O container só usará os núcleos de CPU 0 e 1.

## 2. Limitação de Memória

### -m, --memory
- Define o limite máximo de memória que o container pode usar.
- Exemplo:

```bash
docker run -m 512m nginx
```

- O container é limitado a 512 MB de memória.

### --memory-swap
- Define a quantidade total de memória (física + swap) que o container pode usar.
- Exemplo:

```bash
docker run -m 512m --memory-swap=1g nginx
```

- O container pode usar 512 MB de memória física e até 1 GB incluindo swap.

### --memory-reservation
- Define a quantidade mínima de memória garantida para o container.
- Exemplo:

```bash
docker run -m 512m --memory-reservation=256m nginx
```

- O container tem 256 MB garantidos, mas pode usar até 512 MB se houver memória disponível.

## 3. Limitação de I/O de Disco

### --blkio-weight
- Define a prioridade relativa de I/O de disco para o container (valor entre 10 e 1000).
- Exemplo:

```bash
docker run --blkio-weight=300 nginx
```

- Containers com maior peso têm prioridade no uso de I/O de disco.

### --device-read-bps e --device-write-bps
- Limita a taxa de leitura/escrita em dispositivos específicos.
- Exemplo:

```bash
docker run --device-read-bps /dev/sda:1mb nginx
```

- Limita a leitura no dispositivo `/dev/sda` a 1 MB/s.

## 4. Limitação de PIDs (Processos)

### --pids-limit
- Limita o número máximo de processos que um container pode criar.
- Exemplo:

```bash
docker run --pids-limit=100 nginx
```

- O container pode criar no máximo 100 processos.

## 5. Limitação de Rede

### --network
- Define a rede à qual o container será conectado. Embora não seja uma limitação direta de recursos, configurar redes separadas pode ajudar a controlar e isolar o tráfego de rede entre containers.
- Exemplo:

```bash
docker run --network minha-rede nginx
```

## 6. Considerações de Segurança

### OOME (Out Of Memory Error)
- Containers que excedem os limites de memória podem ser finalizados pelo sistema para evitar um OOME no host. É importante monitorar os recursos e ajustar as configurações conforme necessário.

### Isolamento de Recursos
- Limitar recursos ajuda a isolar containers e impedir que um container afete negativamente outros containers ou o host.

## 7. Monitoramento e Ajustes

### docker stats
- Use o comando `docker stats` para monitorar o uso de recursos em tempo real.
- Exemplo:

```bash
docker stats meu-container
```

### Ajustes Dinâmicos
- Alguns parâmetros, como limites de CPU e memória, podem ser ajustados em containers em execução usando comandos como `docker update`.

## 8. Casos de Uso Comuns

### Containers de Produção
- Limitar CPU e memória em containers de produção para garantir desempenho estável e evitar sobrecarga do host.

### Ambientes Multi-tenant
- Aplicar limites de recursos em ambientes onde vários containers pertencentes a diferentes clientes compartilham o mesmo host, garantindo equidade na alocação de recursos.

### Testes e Desenvolvimento
- Limitar recursos em ambientes de teste para simular condições de produção ou verificar como a aplicação se comporta sob restrições de recursos.

## Dicas de Boas Práticas
- Monitore constantemente o uso de recursos para ajustar as limitações conforme necessário.
- Use limites de recursos para evitar que um container impacte negativamente outros serviços no host.
- Considere as necessidades específicas de cada aplicação ao definir as restrições de recursos.

