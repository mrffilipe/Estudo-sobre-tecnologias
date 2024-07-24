
# Tipos Comuns no TypeScript

O TypeScript oferece vários tipos que são frequentemente utilizados em desenvolvimento de aplicações. Esses tipos ajudam a definir variáveis, funções, objetos e muito mais de maneira clara e segura. Aqui estão alguns dos tipos comuns e conceitos relacionados no TypeScript:

## Tipos de União e Interseção

1. **Tipo de União**
   - Permite que uma variável tenha mais de um tipo possível.
   ```typescript
   function printId(id: number | string) {
     console.log("Your ID is: " + id);
   }
   ```

2. **Tipo de Interseção**
   - Combina múltiplos tipos em um.
   ```typescript
   interface Colorful {
     color: string;
   }
   interface Circle {
     radius: number;
   }
   type ColorfulCircle = Colorful & Circle;
   ```

## Tipos Literais

1. **Literals de String**
   - Define um tipo exato, literal.
   ```typescript
   let myName: "Alice";
   myName = "Alice"; // OK
   myName = "Bob"; // Error
   ```

2. **Literals Numéricos e Booleanos**
   - Similar a literals de string, mas para números e booleanos.
   ```typescript
   let exactValue: 42;
   exactValue = 42; // OK
   exactValue = 43; // Error
   ```

3. **Combinação de Literais com União**
   ```typescript
   type Direction = "north" | "east" | "south" | "west";
   function move(direction: Direction) {
     console.log(`Moving ${direction}`);
   }
   ```

## Tipos de Alias

- Permite a criação de novos nomes para tipos existentes.
```typescript
type Point = {
  x: number;
  y: number;
};
let pt: Point = { x: 10, y: 20 };
```

## Tipos de Funções

1. **Assinaturas de Funções**
   ```typescript
   type Add = (a: number, b: number) => number;
   let add: Add;
   add = (a, b) => a + b;
   ```

2. **Parâmetros Opcionais**
   ```typescript
   function greet(name: string, greeting?: string) {
     console.log(`${greeting || "Hello"}, ${name}!`);
   }
   ```

3. **Parâmetros Padrão**
   ```typescript
   function greet(name: string, greeting: string = "Hello") {
     console.log(`${greeting}, ${name}!`);
   }
   ```

## Objetos e Tipagem Estrutural

- TypeScript é baseado em tipagem estrutural, o que significa que os tipos são compatíveis se suas estruturas são compatíveis.
```typescript
interface Person {
  name: string;
  age: number;
}

function greet(person: Person) {
  console.log(`Hello, ${person.name}`);
}

let user = { name: "John", age: 30 };
greet(user); // OK
```

## Interfaces

- Similar aos tipos, mas geralmente usadas para descrever a forma de um objeto.
```typescript
interface Point {
  x: number;
  y: number;
}
```

## Tipos de União Discriminada

- Uma técnica usada com tipos de união que contém uma propriedade comum (o discriminador) que pode ser usada para identificar a variante da união.
```typescript
interface Square {
  kind: "square";
  size: number;
}

interface Rectangle {
  kind: "rectangle";
  width: number;
  height: number;
}

type Shape = Square | Rectangle;

function area(shape: Shape) {
  switch (shape.kind) {
    case "square":
      return shape.size * shape.size;
    case "rectangle":
      return shape.width * shape.height;
  }
}
```

## Tipos de Interface Genéricos

- Permitem definir tipos de forma a serem reutilizados com diferentes tipos de dados.
```typescript
interface Box<T> {
  contents: T;
}

let stringBox: Box<string> = { contents: "hello" };
let numberBox: Box<number> = { contents: 100 };
```

## Dicas de Boas Práticas

1. **Use Tipos de União para Flexibilidade**: Utilize tipos de união quando uma variável ou função pode ter múltiplos tipos.
2. **Prefira Interfaces para Objetos**: Interfaces são mais apropriadas para descrever formas de objetos e permitem extensão.
3. **Aproveite Tipos Literais para Segurança**: Utilize literals para valores que não mudam, garantindo maior segurança.
4. **Utilize Tipos Genéricos para Reutilização**: Tipos genéricos permitem criar componentes mais reutilizáveis e flexíveis.
