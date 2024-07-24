
# Objetos no TypeScript

Objetos são fundamentais em TypeScript, permitindo a criação de estruturas complexas e reutilizáveis. O TypeScript oferece diversas funcionalidades e tipos para trabalhar eficientemente com objetos.

## Tipos de Objetos

1. **Objetos Literais**
   - Criados diretamente com chaves `{}`.
   ```typescript
   let obj: { name: string; age: number } = {
     name: "John",
     age: 30
   };
   ```

2. **Tipos Opcionais**
   - Propriedades que podem ou não estar presentes.
   ```typescript
   let obj: { name: string; age?: number } = { name: "Alice" };
   ```

3. **Índice de Assinaturas**
   - Define tipos para propriedades dinâmicas.
   ```typescript
   let obj: { [key: string]: number } = {};
   obj["key1"] = 1;
   obj["key2"] = 2;
   ```

## Alias de Tipo

- Definindo alias de tipos para objetos complexos.
  ```typescript
  type User = {
    name: string;
    age: number;
  };

  let user: User = {
    name: "John",
    age: 25
  };
  ```

## Interseção de Tipos

- Combina múltiplos tipos em um só.
  ```typescript
  type CanDrive = {
    drive(): void;
  };

  type CanFly = {
    fly(): void;
  };

  type DriverPilot = CanDrive & CanFly;

  let person: DriverPilot = {
    drive() { console.log("Driving"); },
    fly() { console.log("Flying"); }
  };
  ```

## Funções em Objetos

- Funções como propriedades de objetos.
  ```typescript
  let person: { name: string; greet: () => void } = {
    name: "Jane",
    greet() { console.log("Hello, " + this.name); }
  };

  person.greet(); // "Hello, Jane"
  ```

## Herança de Tipos

- Usando interfaces e tipos para herdar propriedades.
  ```typescript
  interface Animal {
    name: string;
  }

  interface Dog extends Animal {
    breed: string;
  }

  let myDog: Dog = {
    name: "Buddy",
    breed: "Golden Retriever"
  };
  ```

## União Discriminada

- Técnica que usa propriedades comuns para distinguir entre tipos.
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

## Index Signatures

- Definindo tipos para propriedades dinâmicas com índices.
  ```typescript
  interface StringArray {
    [index: number]: string;
  }

  let myArray: StringArray = ["Bob", "Fred"];

  let myStr: string = myArray[0];
  ```

## Readonly Properties

- Propriedades que não podem ser modificadas após inicialização.
  ```typescript
  interface Point {
    readonly x: number;
    readonly y: number;
  }

  let p1: Point = { x: 10, y: 20 };
  p1.x = 5; // Error: Cannot assign to 'x' because it is a read-only property.
  ```

## `this` em Objetos

- Garantir o contexto correto de `this`.
  ```typescript
  let person = {
    name: "John",
    sayHello: function() {
      console.log("Hello, " + this.name);
    }
  };

  person.sayHello(); // Hello, John
  ```

## Dicas de Boas Práticas

1. **Use Tipos e Interfaces para Definir Objetos**: Facilita a manutenção e aumenta a clareza do código.
2. **Prefira Propriedades Readonly quando Apropriado**: Protege dados que não devem ser alterados.
3. **Utilize União Discriminada para Tipos Complexos**: Ajuda a criar tipos seguros e fáceis de entender.
4. **Combine Interseção de Tipos para Funcionalidades Múltiplas**: Permite a criação de objetos multifuncionais.
