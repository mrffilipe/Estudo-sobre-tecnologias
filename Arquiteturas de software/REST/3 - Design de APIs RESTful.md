# 5.1 Design de APIs RESTful

## Definição de endpoints

Os endpoints em uma API RESTful são as URLs que expõem os recursos e permitem a interação com eles. A definição de endpoints deve seguir algumas boas práticas para garantir a clareza e a facilidade de uso:

- **Uso de substantivos**: Endpoints devem representar recursos usando substantivos, não verbos.
  - Exemplo: `/usuarios`, `/produtos`
- **Hierarquia e estrutura**: A estrutura das URLs deve refletir a hierarquia dos recursos.
  - Exemplo: `/usuarios/{usuarioId}/pedidos`
- **Pluralidade**: Use nomes no plural para indicar coleções de recursos.
  - Exemplo: `/usuarios`, `/pedidos`
- **Filtragem, paginação e ordenação**: Utilize query parameters para implementar filtros, paginação e ordenação.
  - Exemplo: `/usuarios?page=2&limit=10&sort=nome`

## Uso adequado de verbos HTTP

Os verbos HTTP devem ser usados de acordo com a operação a ser realizada no recurso:

- **GET**: Recupera representações de recursos.
  - Exemplo: `GET /usuarios` (retorna uma lista de usuários), `GET /usuarios/{usuarioId}` (retorna um usuário específico)
- **POST**: Cria um novo recurso.
  - Exemplo: `POST /usuarios` (cria um novo usuário)
- **PUT**: Atualiza um recurso existente ou cria um novo recurso se não existir.
  - Exemplo: `PUT /usuarios/{usuarioId}` (atualiza os detalhes do usuário com ID especificado)
- **DELETE**: Remove um recurso existente.
  - Exemplo: `DELETE /usuarios/{usuarioId}` (remove o usuário com ID especificado)
- **PATCH**: Aplica modificações parciais a um recurso existente.
  - Exemplo: `PATCH /usuarios/{usuarioId}` (atualiza parcialmente os detalhes do usuário com ID especificado)

## Tratamento de erros e códigos de status

O tratamento de erros e a utilização adequada de códigos de status HTTP são essenciais para a criação de APIs RESTful robustas e intuitivas:

### 2xx (Sucesso)
- **200 OK**: A requisição foi bem-sucedida.
- **201 Created**: Um novo recurso foi criado com sucesso.
- **204 No Content**: A requisição foi bem-sucedida, mas não há conteúdo a ser retornado.

### 4xx (Erro do Cliente)
- **400 Bad Request**: A requisição está malformada ou inválida.
- **401 Unauthorized**: Autenticação é necessária e falhou ou não foi fornecida.
- **403 Forbidden**: O servidor entende a requisição, mas se recusa a autorizá-la.
- **404 Not Found**: O recurso solicitado não foi encontrado.
- **409 Conflict**: Indica conflito com o estado atual do recurso.

### 5xx (Erro do Servidor)
- **500 Internal Server Error**: O servidor encontrou uma situação inesperada que o impediu de atender à requisição.
- **503 Service Unavailable**: O servidor não está disponível para atender à requisição no momento.

## Mensagens de erro detalhadas

Além dos códigos de status, forneça mensagens de erro detalhadas no corpo da resposta para ajudar os clientes a entender o que deu errado:
- Inclua informações como código de erro, mensagem de erro, detalhes adicionais e sugestões para resolução, se aplicável.