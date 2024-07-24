# 3. Funcionamento do Basic Authentication

## Envio de credenciais no cabeçalho

As credenciais de autenticação são enviadas no cabeçalho HTTP `Authorization` em cada solicitação que o cliente faz para acessar um recurso protegido. As credenciais são combinadas em uma única string, separadas por dois pontos (`:`), e então codificadas em Base64. Este cabeçalho é incluído em todas as requisições subsequentes.

- **Exemplo de cabeçalho**:
  - `Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=`
    - Aqui, `dXNlcm5hbWU6cGFzc3dvcmQ=` é a string `username:password` codificada em Base64.

## Decodificação no servidor

Quando o servidor recebe uma solicitação com o cabeçalho `Authorization`, ele decodifica as credenciais de Base64, separa o nome de usuário e a senha, e verifica a autenticidade dessas credenciais.

### Processo de decodificação Base64

1. **Recepção do cabeçalho**: O servidor recebe a solicitação com o cabeçalho `Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=`.
2. **Extração e decodificação**: O servidor extrai a parte codificada em Base64 (`dXNlcm5hbWU6cGFzc3dvcmQ=`) e a decodifica.
   - Decodificação Base64: `dXNlcm5hbWU6cGFzc3dvcmQ=` se torna `username:password`.

### Verificação das credenciais

1. **Separação das credenciais**: A string decodificada (`username:password`) é separada no nome de usuário (`username`) e na senha (`password`).
2. **Validação**: O servidor verifica se o nome de usuário e a senha correspondem a um usuário registrado e autorizado.
   - **Nome de usuário válido**: O servidor verifica se o nome de usuário existe.
   - **Senha válida**: O servidor verifica se a senha fornecida corresponde à senha armazenada para aquele usuário.

3. **Resposta do servidor**:
   - **Sucesso**: Se as credenciais forem válidas, o servidor processa a solicitação e retorna a resposta apropriada.
   - **Falha**: Se as credenciais forem inválidas, o servidor retorna um código de status `401 Unauthorized` indicando que a autenticação falhou.

## Exemplo de fluxo de Basic Authentication

1. **Solicitação inicial sem credenciais**:
   - Cliente: `GET /recurso-protegido`
   - Servidor: `401 Unauthorized` com cabeçalho `WWW-Authenticate: Basic realm="Exemplo"`

2. **Reenvio com credenciais**:
   - Cliente: `GET /recurso-protegido` com cabeçalho `Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=`
   - Servidor: Decodifica e verifica `username:password`
     - **Sucesso**: Retorna `200 OK` com o recurso solicitado.
     - **Falha**: Retorna `401 Unauthorized`.