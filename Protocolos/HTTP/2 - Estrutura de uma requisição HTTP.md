# 1.2 Estrutura de uma Requisição HTTP

## Método de requisição (Verbos HTTP)
Os métodos de requisição, também conhecidos como verbos HTTP, indicam a ação a ser executada para um determinado recurso. Os principais verbos são:
- **GET**: Solicita a representação de um recurso específico. Utilizado principalmente para recuperar dados.
- **POST**: Envia dados para serem processados a um recurso específico. Utilizado para criar novos recursos.
- **PUT**: Substitui todas as atuais representações do recurso de destino pelos dados da requisição.
- **DELETE**: Remove um recurso específico.
- **HEAD**: Solicita uma resposta idêntica a uma requisição GET, mas sem o corpo da resposta.
- **PATCH**: Aplica modificações parciais a um recurso.

## URL (Uniform Resource Locator)
A URL é o endereço completo utilizado para identificar um recurso na Web. Ela é composta por várias partes:
- **Esquema**: Indica o protocolo a ser usado (e.g., http, https).
- **Host**: Nome do servidor ou endereço IP onde o recurso está localizado.
- **Porta**: (Opcional) Porta do servidor a ser conectada.
- **Caminho**: Especifica a localização exata do recurso no servidor.
- **Query String**: (Opcional) Parâmetros adicionais para especificar o recurso ou modificar a requisição.
- **Fragmento**: (Opcional) Referência a uma parte específica do recurso.

## Cabeçalhos de requisição
Os cabeçalhos de requisição HTTP contêm informações adicionais sobre a requisição ou sobre o cliente que está enviando a requisição. Alguns cabeçalhos comuns incluem:
- **Host**: Especifica o domínio da URL.
- **User-Agent**: Identifica o cliente que está fazendo a requisição (navegador, software, etc.).
- **Accept**: Indica os tipos de mídia que o cliente pode processar.
- **Content-Type**: Define o tipo de mídia do corpo da requisição.
- **Authorization**: Contém credenciais para autenticação.
- **Cookie**: Envia cookies armazenados no cliente para o servidor.

## Corpo da requisição
O corpo da requisição (body) contém os dados a serem enviados ao servidor. É opcional e geralmente utilizado em métodos como POST e PUT. O formato do corpo da requisição pode variar:
- **JSON**: Formato comum para envio de dados estruturados.
- **XML**: Outro formato para envio de dados estruturados.
- **Form Data**: Utilizado para envio de formulários (application/x-www-form-urlencoded ou multipart/form-data).
- **Texto**: Dados simples em formato de texto.