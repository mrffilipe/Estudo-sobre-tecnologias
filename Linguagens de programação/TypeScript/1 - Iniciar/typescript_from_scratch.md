
# TypeScript do Zero

TypeScript é uma linguagem de programação desenvolvida pela Microsoft que adiciona tipagem estática ao JavaScript. Ele melhora a segurança e a robustez do código, fornecendo ferramentas que ajudam a detectar erros em tempo de compilação.

## Instalando o TypeScript

1. **Instalação com npm**
   - Para instalar o TypeScript globalmente, use o npm.
   ```sh
   npm install -g typescript
   ```

2. **Verificando a Instalação**
   - Após a instalação, verifique a versão instalada.
   ```sh
   tsc --version
   ```

## Compilando Código TypeScript

1. **Escrevendo um Arquivo TypeScript**
   - Crie um arquivo `hello.ts` com o seguinte conteúdo:
   ```typescript
   function greet(name: string) {
     return `Hello, ${name}!`;
   }

   let user = "World";
   console.log(greet(user));
   ```

2. **Compilando o Arquivo**
   - Use o comando `tsc` para compilar o arquivo TypeScript em JavaScript.
   ```sh
   tsc hello.ts
   ```

3. **Executando o Arquivo Compilado**
   - Execute o arquivo JavaScript gerado.
   ```sh
   node hello.js
   ```

## Configurando o TypeScript

1. **Arquivo tsconfig.json**
   - O `tsconfig.json` é o arquivo de configuração do TypeScript. Crie um arquivo `tsconfig.json` com o seguinte conteúdo:
   ```json
   {
     "compilerOptions": {
       "target": "ES5",
       "module": "commonjs",
       "strict": true,
       "esModuleInterop": true
     },
     "include": ["src"]
   }
   ```

2. **Compilando com tsconfig.json**
   - Com o `tsconfig.json` configurado, você pode simplesmente executar `tsc` para compilar todos os arquivos incluídos.
   ```sh
   tsc
   ```

## Tipagem Básica

1. **Tipos Primitivos**
   - TypeScript fornece tipos primitivos como `number`, `string`, `boolean`.
   ```typescript
   let isDone: boolean = false;
   let age: number = 30;
   let firstName: string = "John";
   ```

2. **Arrays**
   - Declare arrays de tipos específicos.
   ```typescript
   let list: number[] = [1, 2, 3];
   let list: Array<number> = [1, 2, 3];
   ```

3. **Tuplas**
   - Declare arrays com tipos específicos em cada posição.
   ```typescript
   let x: [string, number];
   x = ["hello", 10];  // OK
   ```

## Interfaces

1. **Definindo Interfaces**
   - Use interfaces para definir a estrutura de objetos.
   ```typescript
   interface Person {
     firstName: string;
     lastName: string;
   }

   function greeter(person: Person) {
     return `Hello, ${person.firstName} ${person.lastName}`;
   }

   let user = { firstName: "Jane", lastName: "Doe" };
   console.log(greeter(user));
   ```

## Classes

1. **Definindo Classes**
   - Classes em TypeScript são semelhantes às classes em outras linguagens orientadas a objetos.
   ```typescript
   class Animal {
     name: string;

     constructor(name: string) {
       this.name = name;
     }

     move(distance: number = 0) {
       console.log(`${this.name} moved ${distance}m.`);
     }
   }

   let dog = new Animal("Dog");
   dog.move(10);
   ```

2. **Herança**
   - Use a palavra-chave `extends` para criar subclasses.
   ```typescript
   class Dog extends Animal {
     bark() {
       console.log("Woof! Woof!");
     }
   }

   let dog = new Dog("Rex");
   dog.bark();  // "Woof! Woof!"
   dog.move(10);  // "Rex moved 10m."
   ```

## Módulos

1. **Exportando e Importando Módulos**
   - Organize o código em módulos e use `export` e `import`.
   ```typescript
   // math.ts
   export function add(x: number, y: number): number {
     return x + y;
   }

   // main.ts
   import { add } from "./math";
   console.log(add(2, 3));  // 5
   ```

## Dicas de Boas Práticas

1. **Use Tipos Explícitos**: Declare tipos explicitamente para melhorar a clareza e segurança do código.
2. **Aproveite a Inferência de Tipos**: Deixe o TypeScript inferir tipos quando possível, mas sempre que for necessário, declare explicitamente.
3. **Divida o Código em Módulos**: Organize o código em módulos para melhorar a reutilização e manutenção.
4. **Configure o `tsconfig.json` Adequadamente**: Use o arquivo de configuração para ajustar o compilador às necessidades do seu projeto.
