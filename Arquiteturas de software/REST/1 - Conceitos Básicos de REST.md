# 4.1 Conceitos Básicos de REST

## O que é REST

REST (Representational State Transfer) é um estilo arquitetural para sistemas distribuídos, especialmente para a construção de serviços web. Foi introduzido por Roy Fielding em sua tese de doutorado em 2000. REST é baseado em um conjunto de princípios e restrições que, quando seguidos, permitem a criação de serviços escaláveis, eficientes e modulares.

## Princípios do REST

Os princípios fundamentais do REST incluem:

1. **Interface Uniforme**: Define a interface entre os componentes do sistema de forma uniforme, facilitando a comunicação e a interação entre eles.
   - **Identificação de Recursos**: Recursos são identificados por URIs (Uniform Resource Identifiers).
   - **Manipulação de Recursos através de Representações**: As operações nos recursos são realizadas através de suas representações, que são transferidas entre cliente e servidor.
   - **Mensagens Autodescritivas**: Cada mensagem contém informações suficientes para descrever como processar a mensagem.
   - **Hipermídia como Motor do Estado da Aplicação (HATEOAS)**: Os clientes interagem com a aplicação inteiramente através de hipermídia fornecida dinamicamente pelos servidores.

2. **Sem Estado**: Cada requisição do cliente para o servidor deve conter todas as informações necessárias para entender e processar a requisição. O servidor não armazena o estado do cliente entre as requisições.

3. **Cacheabilidade**: As respostas devem ser explicitamente marcadas como cacheáveis ou não-cacheáveis. Quando cacheáveis, as respostas podem ser armazenadas e reutilizadas para melhorar a performance e reduzir a carga no servidor.

4. **Cliente-Servidor**: A arquitetura cliente-servidor separa as responsabilidades, permitindo que os clientes e servidores evoluam de forma independente. O cliente é responsável pela interface do usuário e a lógica de interação, enquanto o servidor gerencia os dados e a lógica de negócio.

5. **Camadas**: A arquitetura pode ser composta por camadas hierárquicas, onde cada camada só interage com a camada imediatamente adjacente. Isso permite a escalabilidade e a modularidade do sistema.

6. **Código Sob Demanda (Opcional)**: Servidores podem fornecer código executável para clientes, aumentando a funcionalidade do cliente sob demanda (por exemplo, JavaScript).

## Recursos e URIs

No contexto de REST, um recurso é qualquer informação que pode ser nomeada e referenciada. Recursos são os elementos principais manipulados pelas operações do serviço REST.

- **Recursos**: Podem ser documentos, imagens, serviços temporais (como "hoje" em um calendário), coleções de outros recursos, objetos do mundo real, e assim por diante. Um recurso é uma entidade ou um objeto de interesse que pode ser representado em diferentes formatos, como JSON, XML, HTML, etc.

- **URIs (Uniform Resource Identifiers)**: São identificadores que fornecem uma maneira única de identificar e acessar recursos. A URI de um recurso RESTful deve ser intuitiva e fácil de entender. A estrutura da URI geralmente segue um padrão hierárquico que facilita a navegação e a manipulação dos recursos.
  - Exemplo de URI: `http://api.exemplo.com/usuarios/123`
  - Aqui, `usuarios` é o recurso e `123` é o identificador específico do recurso usuário.