
# TypeScript do Zero

## Introdução

TypeScript é um superset do JavaScript que adiciona tipos estáticos opcionais ao código. Ele ajuda a detectar erros durante o desenvolvimento e torna o código mais robusto e fácil de entender.

## Configuração do Ambiente

1. **Instalação do Node.js**: Primeiro, instale o Node.js, que inclui o npm (gerenciador de pacotes do Node).
2. **Instalação do TypeScript**: Use o npm para instalar o TypeScript globalmente:
   ```bash
   npm install -g typescript
   ```
3. **Inicialização do Projeto**: Crie uma nova pasta para o projeto e inicialize o npm:
   ```bash
   mkdir my-project
   cd my-project
   npm init -y
   ```

## Primeiros Passos

1. **Arquivo TypeScript**: Crie um arquivo `index.ts`.
2. **Escrevendo Código**: Escreva um código básico em TypeScript, por exemplo:
   ```typescript
   function greeter(person: string) {
     return "Hello, " + person;
   }

   let user = "Jane User";
   console.log(greeter(user));
   ```
3. **Compilação**: Compile o código TypeScript para JavaScript:
   ```bash
   tsc index.ts
   ```
   Isso gerará um arquivo `index.js`.

## Tipos Básicos

TypeScript fornece tipos básicos como `string`, `number`, `boolean`, `array`, `enum`, `any`, `void`, `null` e `undefined`. Definir tipos ajuda a evitar erros comuns e a tornar o código mais legível.

## Configuração do TypeScript

1. **Arquivo `tsconfig.json`**: Para configurar o compilador TypeScript, crie um arquivo `tsconfig.json`:
   ```json
   {
     "compilerOptions": {
       "target": "es6",
       "module": "commonjs",
       "strict": true,
       "esModuleInterop": true
     }
   }
   ```
   Esse arquivo define as opções de compilação, como o alvo ECMAScript, o sistema de módulos e regras de verificação de tipos.

## Executando o Código

1. **Node.js**: Use o Node.js para executar o arquivo compilado:
   ```bash
   node index.js
   ```
2. **Automatização**: Para evitar a necessidade de compilar manualmente a cada alteração, use ferramentas como `ts-node` ou `nodemon`.

## Boas Práticas

- **Utilize Tipos de Forma Consistente**: Sempre defina tipos para variáveis, parâmetros e retornos de funções para aproveitar ao máximo o TypeScript.
- **Mantenha o `tsconfig.json` Organizado**: Revise e ajuste as configurações conforme necessário para o seu projeto.
- **Integração com Editores**: Use um editor que suporte TypeScript, como Visual Studio Code, para aproveitar recursos como auto-completar e verificação de erros em tempo real.
