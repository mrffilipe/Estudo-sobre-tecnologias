
# Live Restore no Docker

## Visão Geral
A funcionalidade de live restore no Docker permite que containers continuem em execução mesmo que o Docker daemon seja interrompido ou reiniciado. Isso é especialmente útil em ambientes de produção, onde a continuidade do serviço é crítica e não pode ser interrompida por manutenções ou falhas no daemon.

## 1. Como Funciona o Live Restore

### Manutenção da Execução dos Containers
- Com o live restore ativado, os containers que já estão em execução continuam a funcionar mesmo que o Docker daemon seja reiniciado ou pare de funcionar.
- O daemon pode ser reiniciado sem afetar os containers em execução, minimizando o tempo de inatividade e o impacto nos serviços.

### Reconexão ao Daemon
- Quando o Docker daemon é reiniciado, ele se reconecta aos containers em execução sem a necessidade de reiniciá-los.

## 2. Habilitando o Live Restore

### Editando o Arquivo `daemon.json`
- Para habilitar o live restore, você precisa adicionar a seguinte configuração ao arquivo `daemon.json`, localizado em `/etc/docker/daemon.json`:

```json
{
  "live-restore": true
}
```

### Aplicando as Configurações
- Após adicionar a configuração, é necessário reiniciar o Docker daemon para que a mudança tenha efeito:

```bash
sudo systemctl restart docker
```

## 3. Considerações Importantes

### Limitações do Live Restore
- Enquanto o live restore mantém os containers em execução, operações de gerenciamento, como a criação de novos containers ou alteração de configurações, não podem ser realizadas enquanto o daemon está inativo.
- Além disso, certas operações, como a utilização de volumes montados e redes personalizadas, podem ser afetadas se o daemon estiver inativo por muito tempo.

### Recomendado para Ambientes de Produção
- A ativação do live restore é altamente recomendada em ambientes de produção, onde a alta disponibilidade é crítica.

### Monitoramento
- É importante monitorar o estado do Docker daemon e dos containers para garantir que eles continuem a operar corretamente durante e após a aplicação do live restore.

## 4. Casos de Uso Comuns

### Manutenção do Docker Daemon
- Live restore é útil durante atualizações ou manutenções do Docker daemon, permitindo que os containers continuem a operar sem interrupções.

### Recuperação de Falhas do Daemon
- Em casos onde o Docker daemon falha inesperadamente, o live restore garante que os containers em execução não sejam afetados até que o daemon seja restaurado.

### Ambientes de Alta Disponibilidade
- Em ambientes onde a alta disponibilidade é essencial, como servidores web ou sistemas de banco de dados, o live restore ajuda a minimizar o impacto de problemas relacionados ao daemon.

## Dicas de Boas Práticas
- Habilite o live restore em ambientes de produção para garantir a continuidade dos serviços durante manutenções do Docker daemon.
- Monitore o estado dos containers e do Docker daemon para garantir que tudo esteja operando corretamente após a ativação do live restore.
- Considere as limitações do live restore ao planejar manutenções e atualizações do Docker daemon.

