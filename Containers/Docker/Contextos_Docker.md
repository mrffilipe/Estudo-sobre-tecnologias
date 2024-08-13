
# Contextos no Docker

## Visão Geral
Contextos no Docker permitem alternar entre diferentes configurações de ambiente de forma simples e eficiente. Eles são especialmente úteis para gerenciar múltiplos clusters, servidores Docker, ou ambientes de desenvolvimento e produção a partir de um único Docker CLI. Um contexto armazena informações de conexão, como o host Docker, certificado TLS, e opções de configuração, permitindo que você mude de ambiente com um único comando.

## 1. Criando um Novo Contexto

### Comando Básico
- Você pode criar um novo contexto usando o comando `docker context create`. Este comando requer informações sobre o host Docker ao qual você deseja se conectar.
- Exemplo de criação de um contexto chamado `my-context`:

```bash
docker context create my-context --docker "host=tcp://192.168.1.100:2376"
```

### Especificando Certificados TLS
- Se o Docker host requer certificados TLS, você pode especificá-los durante a criação do contexto:

```bash
docker context create my-context --docker "host=tcp://192.168.1.100:2376,ca=/path/to/ca.pem,cert=/path/to/cert.pem,key=/path/to/key.pem"
```

## 2. Listando e Selecionando Contextos

### Listando Contextos
- Para ver todos os contextos disponíveis, use o comando:

```bash
docker context ls
```

- O contexto atualmente ativo será indicado por um asterisco `*`.

### Alternando Entre Contextos
- Para alternar para um contexto diferente, use o comando `docker context use` seguido do nome do contexto:

```bash
docker context use my-context
```

## 3. Gerenciando Contextos

### Removendo um Contexto
- Para remover um contexto que não é mais necessário, use o comando:

```bash
docker context rm my-context
```

### Inspecionando um Contexto
- Para ver os detalhes de um contexto específico, incluindo as configurações de conexão, use:

```bash
docker context inspect my-context
```

### Atualizando um Contexto
- Se precisar alterar as configurações de um contexto existente, você pode usar o comando `docker context update`. No entanto, na maioria dos casos, é mais simples remover e recriar o contexto com as novas configurações.

## 4. Usos Comuns para Contextos

### Desenvolvimento e Produção
- Contextos são extremamente úteis para alternar entre ambientes de desenvolvimento, teste e produção sem precisar reconfigurar manualmente o Docker CLI cada vez.

### Gerenciamento de Múltiplos Clusters
- Quando se trabalha com múltiplos clusters Docker Swarm ou Kubernetes, contextos facilitam a alternância entre os clusters para gerenciamento e implantação.

### Trabalho Remoto e Local
- Desenvolvedores que precisam alternar entre um ambiente de trabalho local e um servidor remoto podem usar contextos para gerenciar facilmente as conexões e as configurações de cada ambiente.

## 5. Considerações de Boas Práticas

### Nomes Descritivos para Contextos
- Use nomes descritivos para contextos, como `dev`, `prod`, ou `staging`, para facilitar a identificação rápida do ambiente ao qual você está conectado.

### Documentação e Consistência
- Documente os contextos utilizados em projetos para garantir que toda a equipe saiba como alternar entre diferentes ambientes de forma consistente.

### Segurança
- Mantenha os certificados e as chaves privadas usados nos contextos em locais seguros e com permissões adequadas para evitar o acesso não autorizado.

## Dicas de Boas Práticas
- Utilize nomes claros e descritivos para contextos, facilitando a alternância entre diferentes ambientes.
- Documente e compartilhe as configurações de contexto com a equipe para garantir consistência nos projetos.
- Proteja as credenciais e certificados utilizados nos contextos para garantir a segurança dos ambientes Docker.

