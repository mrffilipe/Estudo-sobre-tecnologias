# 4.2 Operações RESTful usando HTTP

## Métodos HTTP em REST (CRUD)

Os métodos HTTP em REST são usados para executar operações CRUD (Create, Read, Update, Delete) em recursos. Cada método HTTP corresponde a uma operação específica:

- **POST (Create)**: Cria um novo recurso no servidor.
  - Exemplo: `POST /usuarios` cria um novo usuário.
  
- **GET (Read)**: Recupera representações de recursos do servidor.
  - Exemplo: `GET /usuarios/123` recupera os detalhes do usuário com ID 123.
  
- **PUT (Update)**: Atualiza um recurso existente ou cria um novo recurso se ele não existir.
  - Exemplo: `PUT /usuarios/123` atualiza os detalhes do usuário com ID 123.
  
- **DELETE (Delete)**: Remove um recurso existente do servidor.
  - Exemplo: `DELETE /usuarios/123` remove o usuário com ID 123.
  
- **PATCH (Update parcial)**: Aplica modificações parciais a um recurso existente.
  - Exemplo: `PATCH /usuarios/123` atualiza parcialmente os detalhes do usuário com ID 123.

## Statelessness (sem estado)

Em REST, cada requisição do cliente para o servidor deve conter todas as informações necessárias para entender e processar a requisição. O servidor não armazena o estado do cliente entre as requisições. Isso significa que cada requisição é independente e autossuficiente.

Benefícios do statelessness:
- **Escalabilidade**: Facilita a distribuição de requisições entre vários servidores.
- **Simples de gerenciar**: Reduz a complexidade no gerenciamento de estados no servidor.
- **Desempenho**: Melhor performance devido à ausência de overhead para manter estados.

## Cacheabilidade

Em REST, as respostas das requisições podem ser marcadas como cacheáveis ou não-cacheáveis. Quando cacheáveis, as respostas podem ser armazenadas pelo cliente ou por proxies intermediários e reutilizadas em requisições futuras.

Benefícios da cacheabilidade:
- **Redução da latência**: Melhora a performance reduzindo o tempo de resposta.
- **Redução da carga no servidor**: Diminui o número de requisições processadas pelo servidor.
- **Eficiência**: Aumenta a eficiência na utilização da largura de banda.

## Interface uniforme

A interface uniforme é um dos princípios fundamentais do REST. Ela simplifica e desassocia a arquitetura, permitindo que cada parte do sistema evolua de forma independente. Os quatro principais restrições da interface uniforme são:

1. **Identificação de Recursos**: Recursos são identificados por URIs.
2. **Manipulação de Recursos através de Representações**: Operações nos recursos são realizadas através de suas representações.
3. **Mensagens Autodescritivas**: Cada mensagem contém informações suficientes para descrever como processar a mensagem.
4. **Hipermídia como Motor do Estado da Aplicação (HATEOAS)**: Clientes interagem com a aplicação inteiramente através de hipermídia fornecida dinamicamente pelos servidores.