
# TypeScript em 5 Minutos

## Introdução

TypeScript é uma linguagem de programação que se baseia no JavaScript, adicionando tipagem estática opcional. Isso permite detectar erros antes de executar o código, tornando o desenvolvimento mais eficiente e seguro.

## Primeiros Passos

1. **Instalação do TypeScript**
   ```bash
   npm install -g typescript
   ```
   Este comando instala o compilador TypeScript globalmente.

2. **Compilação de um Arquivo TypeScript**
   - Crie um arquivo chamado `hello.ts` com o seguinte conteúdo:
     ```typescript
     function greeter(person: string) {
       return "Hello, " + person;
     }

     let user = "Jane User";
     console.log(greeter(user));
     ```
   - Compile o arquivo TypeScript para JavaScript:
     ```bash
     tsc hello.ts
     ```
   - Isso gera um arquivo `hello.js` que pode ser executado com Node.js:
     ```bash
     node hello.js
     ```

## Tipagem Estática

TypeScript permite declarar tipos para variáveis, parâmetros de função e retornos de função, o que ajuda a capturar erros cedo. No exemplo acima, a função `greeter` espera um parâmetro do tipo `string`.

## Interfaces

Interfaces em TypeScript ajudam a definir a forma de objetos, garantindo que eles tenham as propriedades necessárias.

```typescript
interface Person {
  firstName: string;
  lastName: string;
}

function greeter(person: Person) {
  return "Hello, " + person.firstName + " " + person.lastName;
}

let user = { firstName: "Jane", lastName: "User" };
console.log(greeter(user));
```

## Classes

Classes em TypeScript são uma maneira comum de definir objetos e suas funcionalidades. Elas suportam herança, encapsulamento e polimorfismo.

```typescript
class Student {
  fullName: string;
  constructor(public firstName: string, public middleInitial: string, public lastName: string) {
    this.fullName = firstName + " " + middleInitial + " " + lastName;
  }
}

interface Person {
  firstName: string;
  lastName: string;
}

function greeter(person: Person) {
  return "Hello, " + person.firstName + " " + person.lastName;
}

let user = new Student("Jane", "M.", "User");
console.log(greeter(user));
```

## Configuração do Compilador

Crie um arquivo `tsconfig.json` para configurar o compilador TypeScript. Este arquivo define as opções de compilação e facilita o gerenciamento do projeto.

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "strict": true
  }
}
```

## Compilação e Execução

Para compilar todo o projeto, use:
```bash
tsc
```
Isso compilará todos os arquivos TypeScript de acordo com as configurações no `tsconfig.json`.

## Boas Práticas

- **Consistência na Tipagem**: Sempre defina tipos para variáveis e parâmetros de funções.
- **Uso de Interfaces**: Utilize interfaces para definir a forma de objetos e garantir que eles possuam as propriedades necessárias.
- **Configuração Adequada**: Mantenha o arquivo `tsconfig.json` bem configurado para facilitar o desenvolvimento e compilação do projeto.
- **Ferramentas de Desenvolvimento**: Utilize um editor de código com suporte para TypeScript, como o Visual Studio Code, para aproveitar funcionalidades como auto-completar e verificação de erros em tempo real.
