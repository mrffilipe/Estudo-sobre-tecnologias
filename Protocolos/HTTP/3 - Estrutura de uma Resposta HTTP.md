# 1.3 Estrutura de uma Resposta HTTP

## Código de status
Os códigos de status HTTP indicam o resultado da solicitação HTTP feita pelo cliente. Eles são divididos em cinco classes:
- **1xx (Informacional)**: Indica que a solicitação foi recebida e o processo continua.
  - Exemplo: 100 Continue
- **2xx (Sucesso)**: Indica que a solicitação foi recebida, compreendida e aceita com sucesso.
  - Exemplo: 200 OK
- **3xx (Redirecionamento)**: Indica que é necessário mais ação por parte do cliente para concluir a solicitação.
  - Exemplo: 301 Moved Permanently
- **4xx (Erro do cliente)**: Indica que houve um erro na solicitação enviada pelo cliente.
  - Exemplo: 404 Not Found
- **5xx (Erro do servidor)**: Indica que o servidor falhou ao cumprir uma solicitação válida.
  - Exemplo: 500 Internal Server Error

## Cabeçalhos de resposta
Os cabeçalhos de resposta HTTP contêm informações adicionais sobre a resposta, como metadados sobre os dados sendo transferidos ou sobre o próprio servidor. Alguns cabeçalhos comuns incluem:
- **Date**: Data e hora em que a mensagem de resposta foi gerada.
- **Server**: Informações sobre o software do servidor que está respondendo.
- **Content-Type**: Tipo de mídia do corpo da resposta.
- **Content-Length**: Tamanho do corpo da resposta em bytes.
- **Set-Cookie**: Define cookies que devem ser armazenados pelo cliente e enviados em futuras solicitações ao servidor.

## Corpo da resposta
O corpo da resposta contém os dados solicitados pelo cliente. O conteúdo do corpo da resposta varia conforme o tipo de solicitação e pode incluir:
- **HTML**: Conteúdo de páginas web.
- **JSON**: Dados estruturados em formato JSON.
- **XML**: Dados estruturados em formato XML.
- **Texto**: Dados simples em formato de texto.
- **Arquivos binários**: Imagens, vídeos, documentos, etc.