
# TypeScript em 5 Minutos - Programação Funcional

TypeScript suporta programação funcional (PF), permitindo que você escreva código de forma mais declarativa e imutável. Este guia rápido mostra como começar com programação funcional em TypeScript.

## Funções como Cidadãos de Primeira Classe

1. **Definindo Funções**
   - Funções em TypeScript podem ser atribuídas a variáveis, passadas como argumentos e retornadas de outras funções.
   ```typescript
   function greeter(person: string): string {
     return \`Hello, \${person}\`;
   }

   let greetFunction: (person: string) => string;
   greetFunction = greeter;
   console.log(greetFunction("World"));  // "Hello, World"
   ```

## Funções Anônimas e Arrow Functions

1. **Funções Anônimas**
   - Defina funções sem nome, frequentemente usadas como argumentos.
   ```typescript
   let add = function(x: number, y: number): number {
     return x + y;
   };
   console.log(add(2, 3));  // 5
   ```

2. **Arrow Functions**
   - Sintaxe concisa para definir funções, com o contexto `this` léxico.
   ```typescript
   let subtract = (x: number, y: number): number => x - y;
   console.log(subtract(5, 3));  // 2
   ```

## Funções de Ordem Superior

1. **Definindo Funções de Ordem Superior**
   - Funções que recebem outras funções como argumentos ou retornam funções.
   ```typescript
   function applyOperation(x: number, y: number, operation: (a: number, b: number) => number): number {
     return operation(x, y);
   }

   let multiply = (x: number, y: number): number => x * y;
   console.log(applyOperation(2, 3, multiply));  // 6
   ```

## Imutabilidade

1. **Constantes**
   - Use `const` para garantir que variáveis não sejam reassinadas.
   ```typescript
   const pi = 3.14;
   // pi = 3.1415; // Error: Assignment to constant variable.
   ```

2. **Objetos Imutáveis**
   - Evite modificar objetos diretamente. Use métodos que retornam novos objetos.
   ```typescript
   const person = { name: "Alice", age: 25 };
   const updatedPerson = { ...person, age: 26 };
   console.log(updatedPerson);  // { name: "Alice", age: 26 }
   ```

## Funções Puras

1. **Definindo Funções Puras**
   - Funções que não têm efeitos colaterais e sempre retornam o mesmo resultado para os mesmos argumentos.
   ```typescript
   function pureFunction(x: number, y: number): number {
     return x + y;
   }

   console.log(pureFunction(2, 3));  // 5
   ```

## Composição de Funções

1. **Compor Funções**
   - Combine funções menores para criar funções mais complexas.
   ```typescript
   const add = (a: number) => (b: number) => a + b;
   const multiply = (a: number) => (b: number) => a * b;

   const addAndMultiply = (a: number, b: number, c: number) => multiply(a + b)(c);

   console.log(addAndMultiply(1, 2, 3));  // 9
   ```

## Currying

1. **Funções Curried**
   - Transforme uma função com múltiplos argumentos em uma cadeia de funções que aceitam um único argumento.
   ```typescript
   function add(x: number): (y: number) => number {
     return function(y: number): number {
       return x + y;
     };
   }

   const addFive = add(5);
   console.log(addFive(3));  // 8
   ```

## Dicas de Boas Práticas

1. **Prefira Funções Puras**: Elas são mais previsíveis e fáceis de testar.
2. **Evite Efeitos Colaterais**: Minimize a mutação de estado dentro das funções.
3. **Use Imutabilidade**: Trabalhe com dados imutáveis para evitar estados imprevisíveis.
4. **Aproveite Funções de Ordem Superior**: Elas permitem criar abstrações poderosas e reutilizáveis.
