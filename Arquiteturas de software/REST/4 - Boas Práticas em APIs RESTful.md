# 5.2 Boas Práticas em APIs RESTful

## Versionamento de APIs

O versionamento de APIs é essencial para garantir a continuidade dos serviços enquanto novas funcionalidades são adicionadas ou alterações são feitas. Algumas práticas comuns de versionamento incluem:

- **No caminho da URL**: Adicionar a versão da API na URL.
  - Exemplo: `/v1/usuarios`, `/v2/usuarios`
- **Em cabeçalhos**: Usar cabeçalhos HTTP para especificar a versão da API.
  - Exemplo: `Accept: application/vnd.api.v1+json`
- **Parâmetros de consulta**: Usar parâmetros de consulta para especificar a versão da API.
  - Exemplo: `/usuarios?version=1`

## Documentação de APIs (OpenAPI/Swagger)

A documentação de APIs é crucial para a utilização e adoção por desenvolvedores. Ferramentas como OpenAPI e Swagger são amplamente utilizadas para criar e manter documentações claras e interativas.

- **OpenAPI**: Um padrão para especificação de APIs RESTful, que permite descrever os endpoints, operações, parâmetros e respostas da API.
  - **Exemplo**: Arquivo YAML ou JSON que descreve a API.
- **Swagger**: Uma coleção de ferramentas baseadas na especificação OpenAPI para documentação, geração de código e testes de APIs.
  - **Swagger UI**: Permite a visualização interativa da documentação da API e a execução de testes diretamente na interface.
  - **Swagger Editor**: Ferramenta para escrever a especificação OpenAPI em um ambiente amigável.

Benefícios da documentação de APIs:
- Facilita a compreensão e o uso da API pelos desenvolvedores.
- Ajuda na manutenção e evolução da API.
- Permite a geração automática de clientes e servidores para a API.

## Autenticação e Autorização (OAuth, JWT)

A autenticação e a autorização são essenciais para garantir a segurança das APIs. Duas abordagens comuns são OAuth e JWT (JSON Web Token).

- **OAuth**: Um protocolo de autorização que permite que aplicativos obtenham acesso limitado a recursos em um servidor HTTP em nome do proprietário do recurso.
  - **OAuth 2.0**: A versão mais recente do protocolo, amplamente utilizada para autenticação e autorização em APIs RESTful.
  - **Fluxo de autorização**: Envolve a obtenção de um token de acesso que é usado para acessar os recursos protegidos.

- **JWT (JSON Web Token)**: Um padrão aberto que define uma maneira compacta e autossuficiente de transmitir informações de forma segura entre partes como um objeto JSON.
  - **Estrutura**: Composto por três partes (header, payload, signature) que são codificadas em Base64 e separadas por pontos.
  - **Uso**: Utilizado para autenticação e troca segura de informações entre cliente e servidor.
  - **Benefícios**: Fácil de usar, seguro, e permite a verificação da integridade e autenticidade dos dados.

Exemplos de práticas de segurança:
- **Autenticação com OAuth 2.0**: Permite que usuários autorizem aplicativos a agir em seu nome sem compartilhar suas credenciais.
- **Autorização com JWT**: Utiliza tokens assinados que são enviados com cada requisição para verificar a identidade e permissões do usuário.