
# Tipos `typeof` no TypeScript

O operador `typeof` no TypeScript é usado para obter o tipo de uma variável ou expressão em tempo de execução. Isso permite criar tipos dinamicamente baseados no valor de outra variável.

## Usando `typeof` para Criar Tipos

1. **Definindo Tipos Baseados em Valores**
   - O operador `typeof` pode capturar o tipo de uma variável ou expressão.
   ```typescript
   let s = "hello";
   let n: typeof s;  // string
   ```

2. **Usando `typeof` em Funções**
   - Captura o tipo de retorno de uma função.
   ```typescript
   function f() {
     return { x: 10, y: 3 };
   }
   type P = ReturnType<typeof f>;  // { x: number; y: number }
   ```

## Combinando `typeof` com `keyof`

1. **Criando Tipos de Chaves Dinâmicas**
   - Usando `keyof` e `typeof` juntos para criar tipos dinamicamente.
   ```typescript
   const person = {
     name: "Alice",
     age: 25
   };

   type PersonKeys = keyof typeof person;  // "name" | "age"
   ```

## Usando `typeof` em Declarações de Função

1. **Capturando o Tipo de uma Função**
   - Você pode capturar a assinatura de tipo de uma função usando `typeof`.
   ```typescript
   function add(a: number, b: number): number {
     return a + b;
   }

   type AddType = typeof add;  // (a: number, b: number) => number
   ```

## `typeof` e Inferência de Tipo

1. **Inferência de Tipos com `typeof`**
   - `typeof` pode ser usado para inferir tipos em declarações de variáveis.
   ```typescript
   let x = { a: 1, b: 2 };
   type X = typeof x;  // { a: number; b: number }
   ```

## Exemplo de Uso com Objetos

1. **Definindo Tipos a Partir de Objetos**
   - Use `typeof` para criar tipos baseados em objetos.
   ```typescript
   const obj = {
     name: "Alice",
     age: 25,
     isStudent: true
   };

   type ObjType = typeof obj;
   // { name: string; age: number; isStudent: boolean }
   ```

## Usando `typeof` em Tipos Genéricos

1. **Combinando `typeof` com Genéricos**
   - Crie funções genéricas que utilizam `typeof` para inferir tipos.
   ```typescript
   function getValue<T, K extends keyof T>(obj: T, key: K): T[K] {
     return obj[key];
   }

   let person = { name: "Alice", age: 25 };
   let personName = getValue(person, "name");  // string
   ```

## Tipos de Variáveis com `typeof`

1. **Capturando o Tipo de Variáveis**
   - `typeof` pode capturar o tipo de variáveis em diferentes contextos.
   ```typescript
   let str = "hello";
   let num = 42;

   type StrType = typeof str;  // string
   type NumType = typeof num;  // number
   ```

## Tipos de Funções e `typeof`

1. **Usando `typeof` para Capturar Tipos de Funções**
   - Captura a assinatura de tipo de funções.
   ```typescript
   function greet(name: string): string {
     return `Hello, ${name}`;
   }

   type GreetType = typeof greet;  // (name: string) => string
   ```

## Dicas de Boas Práticas

1. **Use `typeof` para Manter Tipos Sincronizados**: Facilita a manutenção de tipos baseados em variáveis e expressões existentes.
2. **Combine `typeof` com `keyof` para Tipos Dinâmicos**: Crie tipos mais flexíveis e seguros usando `keyof` junto com `typeof`.
3. **Aproveite `typeof` em Funções Genéricas**: Melhore a inferência de tipos em funções genéricas usando `typeof`.
4. **Documente o Uso de `typeof`**: Facilita o entendimento de como os tipos foram derivados.
