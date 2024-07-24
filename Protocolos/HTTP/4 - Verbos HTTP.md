# 1.4 Verbos HTTP

## GET
O método GET é utilizado para solicitar a representação de um recurso específico. As solicitações GET não devem ser usadas para operações que causam efeitos colaterais (por exemplo, modificar um recurso). Elas são idempotentes e seguras.
- **Uso comum**: Recuperar dados de um servidor.
- **Exemplo**: Solicitar uma página web.

## POST
O método POST é utilizado para enviar dados a um servidor para criar ou atualizar um recurso. Os dados são incluídos no corpo da solicitação. O POST não é idempotente, ou seja, múltiplas solicitações podem resultar em diferentes efeitos.
- **Uso comum**: Submissão de formulários, upload de arquivos.
- **Exemplo**: Enviar dados de cadastro de usuário.

## PUT
O método PUT é utilizado para atualizar um recurso existente ou criar um novo recurso se ele não existir. Ele é idempotente, o que significa que múltiplas solicitações terão o mesmo efeito que uma única solicitação.
- **Uso comum**: Atualizar um recurso completo.
- **Exemplo**: Atualizar as informações de um usuário.

## DELETE
O método DELETE é utilizado para remover um recurso específico. Ele é idempotente.
- **Uso comum**: Remover recursos de um servidor.
- **Exemplo**: Excluir um usuário do sistema.

## PATCH
O método PATCH é utilizado para aplicar modificações parciais a um recurso. Ao contrário do PUT, que substitui o recurso inteiro, o PATCH aplica apenas as alterações especificadas.
- **Uso comum**: Atualizar parcialmente um recurso.
- **Exemplo**: Atualizar apenas o endereço de um usuário.

## HEAD
O método HEAD é semelhante ao GET, mas solicita apenas os cabeçalhos da resposta, sem o corpo. Ele é usado para obter metadados sobre o recurso sem transferir o conteúdo completo.
- **Uso comum**: Verificar se um recurso existe, obter informações sobre ele.
- **Exemplo**: Verificar a última modificação de uma página web.

## OPTIONS
O método OPTIONS é utilizado para descrever as opções de comunicação para o recurso de destino. Ele retorna os métodos HTTP suportados pelo servidor para um recurso específico.
- **Uso comum**: Determinar as capacidades do servidor.
- **Exemplo**: Verificar os métodos permitidos em um endpoint.

## TRACE
O método TRACE é utilizado para realizar um teste de loopback de solicitação, retornando o que foi recebido no servidor, sem modificações. Ele é útil para depuração.
- **Uso comum**: Diagnóstico e depuração de solicitações HTTP.
- **Exemplo**: Verificar o caminho que uma solicitação percorre até o servidor.