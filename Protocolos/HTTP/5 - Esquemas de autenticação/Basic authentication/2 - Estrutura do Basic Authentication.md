# 2. Estrutura do Basic Authentication

## Uso de nome de usuário e senha

No Basic Authentication, a autenticação é realizada através do uso de um par de credenciais composto por um nome de usuário e uma senha. Essas credenciais são utilizadas para verificar a identidade do usuário e garantir que ele tenha permissão para acessar os recursos protegidos.

- **Nome de usuário**: Identifica o usuário que está tentando acessar o recurso.
- **Senha**: Verifica a identidade do usuário, garantindo que ele seja quem diz ser.

## Codificação Base64

As credenciais (nome de usuário e senha) são combinadas em uma única string, separadas por dois pontos (":"), e então codificadas usando Base64. A codificação Base64 é uma forma de representar dados binários em um formato ASCII, o que facilita a transmissão dessas credenciais através dos cabeçalhos HTTP.

- **Combinação de credenciais**: `nome_de_usuário:senha`
  - Exemplo: `marcos:senha123`
- **Codificação Base64**: A string combinada é então convertida para Base64.
  - Exemplo: `marcos:senha123` se torna `bWFyY29zOnNlbmhhMTIz`

## Cabeçalho HTTP Authorization

As credenciais codificadas são enviadas no cabeçalho HTTP `Authorization` em cada solicitação que o cliente faz para acessar um recurso protegido. O cabeçalho `Authorization` segue o formato:

- `Authorization: Basic <credenciais codificadas>`

Esse cabeçalho é incluído em todas as solicitações subsequentes que o cliente faz ao servidor, garantindo que o servidor possa verificar as credenciais e conceder ou negar acesso ao recurso solicitado.

### Exemplo de uma solicitação com Basic Authentication

1. **Combinação e codificação das credenciais**:
   - Nome de usuário: `marcos`
   - Senha: `senha123`
   - String combinada: `marcos:senha123`
   - String codificada em Base64: `bWFyY29zOnNlbmhhMTIz`

2. **Cabeçalho HTTP Authorization**:
   - `Authorization: Basic bWFyY29zOnNlbmhhMTIz`

## Fluxo do Basic Authentication

1. **Cliente**: Faz uma solicitação para um recurso protegido sem incluir credenciais.
2. **Servidor**: Responde com `401 Unauthorized` e inclui o cabeçalho `WWW-Authenticate` indicando que a autenticação é necessária.
3. **Cliente**: Reenvia a solicitação, desta vez incluindo o cabeçalho `Authorization` com as credenciais codificadas em Base64.
4. **Servidor**: Decodifica as credenciais, verifica a autenticidade do nome de usuário e senha, e concede ou nega acesso ao recurso.