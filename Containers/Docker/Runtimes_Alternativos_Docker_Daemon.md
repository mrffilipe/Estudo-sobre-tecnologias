
# Runtimes Alternativos no Docker Daemon

## Visão Geral
O Docker suporta o uso de runtimes alternativos além do padrão `runc`, que é usado para criar e executar containers. Runtimes alternativos podem ser utilizados para atender a requisitos específicos de segurança, desempenho, ou compatibilidade, como usar `Kata Containers` para maior isolamento ou `gVisor` para maior segurança.

## 1. O Que São Runtimes Alternativos?

### `runc`
- É o runtime padrão usado pelo Docker para criar e executar containers. É leve e amplamente utilizado, sendo responsável pela maioria dos workloads Docker.

### Outros Runtimes
- **Kata Containers**: Oferece maior isolamento ao rodar containers em máquinas virtuais leves.
- **gVisor**: Focado em segurança, roda containers em um ambiente isolado que intercepta as chamadas do sistema.
- **cri-o**: Um runtime leve para Kubernetes, criado para gerenciar containers com maior eficiência.

## 2. Configurando um Runtime Alternativo

### Editando o Arquivo `daemon.json`
- Para configurar um runtime alternativo, você precisa modificar o arquivo `daemon.json` e adicionar as configurações necessárias.

- Exemplo de configuração para adicionar `kata-runtime` como um runtime adicional:

```json
{
  "runtimes": {
    "kata-runtime": {
      "path": "/usr/bin/kata-runtime"
    }
  }
}
```

### Definindo o Runtime Padrão
- Se você deseja que o runtime alternativo seja o padrão para todos os containers, adicione a configuração `default-runtime` ao `daemon.json`:

```json
{
  "default-runtime": "kata-runtime",
  "runtimes": {
    "kata-runtime": {
      "path": "/usr/bin/kata-runtime"
    }
  }
}
```

## 3. Usando Runtimes Alternativos com Containers

### Especificando o Runtime ao Criar um Container
- Para usar um runtime específico ao criar um container, utilize a flag `--runtime`:

```bash
docker run --runtime kata-runtime alpine
```

### Verificando o Runtime de um Container
- Para verificar qual runtime está sendo usado por um container em execução:

```bash
docker inspect --format '{{.HostConfig.Runtime}}' <container_id>
```

## 4. Considerações de Segurança e Desempenho

### Segurança
- Runtimes como `gVisor` e `Kata Containers` oferecem maior segurança ao isolar containers de maneira mais eficaz que `runc`. Escolha o runtime com base nas necessidades de segurança do seu ambiente.

### Desempenho
- Alguns runtimes podem introduzir overhead adicional devido ao maior isolamento (como o uso de VMs em Kata Containers). Avalie o impacto no desempenho antes de adotar um runtime alternativo em produção.

## 5. Casos de Uso Comuns

### Ambientes de Alta Segurança
- Em ambientes onde a segurança é crítica, como infraestruturas financeiras ou governamentais, o uso de runtimes como `gVisor` ou `Kata Containers` pode ajudar a atender a requisitos rigorosos de segurança.

### Isolamento Rigoroso
- Para workloads que exigem isolamento rigoroso, como multi-tenant environments, o uso de runtimes que oferecem maior separação, como `Kata Containers`, pode ser vantajoso.

### Kubernetes e Runtimes Leves
- Em clusters Kubernetes, runtimes como `cri-o` podem ser utilizados para melhorar a eficiência na criação e gerenciamento de containers, integrando-se diretamente com o Kubernetes.

## Dicas de Boas Práticas
- Avalie o impacto de desempenho ao utilizar runtimes alternativos em ambientes de produção.
- Use runtimes como `gVisor` ou `Kata Containers` para aumentar a segurança em ambientes que exigem maior isolamento.
- Considere as necessidades específicas de segurança e isolamento do seu ambiente ao escolher um runtime alternativo.

