
# TypeScript em 5 Minutos

TypeScript é uma linguagem de programação que adiciona tipagem estática ao JavaScript. Ele ajuda a evitar muitos erros comuns e melhora a qualidade do código.

## Começando com TypeScript

1. **Instalando TypeScript**
   - Instale o compilador TypeScript usando npm.
   ```sh
   npm install -g typescript
   ```

2. **Escrevendo um Arquivo TypeScript**
   - Crie um arquivo `greeter.ts` com o seguinte conteúdo:
   ```typescript
   function greeter(person: string) {
     return `Hello, ${person}`;
   }

   let user = "Jane User";

   console.log(greeter(user));
   ```

3. **Compilando o Arquivo TypeScript**
   - Compile o arquivo TypeScript para JavaScript.
   ```sh
   tsc greeter.ts
   ```

4. **Executando o Arquivo JavaScript**
   - Execute o arquivo JavaScript gerado.
   ```sh
   node greeter.js
   ```

## Tipagem Básica

1. **Adicionando Tipos**
   - Adicione tipos às variáveis e parâmetros para melhorar a segurança do código.
   ```typescript
   function greeter(person: string) {
     return `Hello, ${person}`;
   }

   let user: string = "Jane User";

   console.log(greeter(user));
   ```

2. **Definindo Interfaces**
   - Use interfaces para definir a estrutura de objetos.
   ```typescript
   interface Person {
     firstName: string;
     lastName: string;
   }

   function greeter(person: Person) {
     return `Hello, ${person.firstName} ${person.lastName}`;
   }

   let user = { firstName: "Jane", lastName: "User" };

   console.log(greeter(user));
   ```

## Classes

1. **Criando uma Classe**
   - Defina uma classe com propriedades e métodos.
   ```typescript
   class Student {
     fullName: string;

     constructor(public firstName: string, public middleInitial: string, public lastName: string) {
       this.fullName = `${firstName} ${middleInitial} ${lastName}`;
     }
   }

   interface Person {
     firstName: string;
     lastName: string;
   }

   function greeter(person: Person) {
     return `Hello, ${person.firstName} ${person.lastName}`;
   }

   let user = new Student("Jane", "M.", "User");

   console.log(greeter(user));
   ```

2. **Herança**
   - Use a palavra-chave `extends` para criar subclasses e reutilizar código.
   ```typescript
   class Animal {
     move(distance: number = 0) {
       console.log(`Animal moved ${distance}m.`);
     }
   }

   class Dog extends Animal {
     bark() {
       console.log("Woof! Woof!");
     }
   }

   const dog = new Dog();
   dog.bark();  // "Woof! Woof!"
   dog.move(10);  // "Animal moved 10m."
   ```

## Compilação

1. **Compilando Múltiplos Arquivos**
   - Compile vários arquivos TypeScript ao mesmo tempo.
   ```sh
   tsc file1.ts file2.ts
   ```

2. **Usando tsconfig.json**
   - Crie um arquivo `tsconfig.json` para definir as configurações do compilador.
   ```json
   {
     "compilerOptions": {
       "target": "es5",
       "module": "commonjs",
       "strict": true,
       "esModuleInterop": true
     }
   }
   ```

## Dicas de Boas Práticas

1. **Adicione Tipos Explicitamente**: Declare tipos explícitos para variáveis e parâmetros para melhorar a clareza e a segurança do código.
2. **Use Interfaces para Estruturas de Objetos**: Defina interfaces para padronizar a estrutura de objetos e facilitar a manutenção.
3. **Aproveite Classes e Herança**: Use classes para criar componentes reutilizáveis e aplique herança para compartilhar funcionalidades comuns.
4. **Configure Adequadamente o tsconfig.json**: Utilize o arquivo de configuração para ajustar o compilador às necessidades do seu projeto.
