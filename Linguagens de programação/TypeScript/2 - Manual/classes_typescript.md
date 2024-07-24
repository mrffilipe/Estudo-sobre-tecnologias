
# Classes no TypeScript

Classes são uma maneira fundamental de definir objetos e suas interações em TypeScript. Elas oferecem uma maneira conveniente de definir propriedades e métodos, além de suportar conceitos de programação orientada a objetos como herança, encapsulamento e polimorfismo.

## Definindo Classes

1. **Classe Básica**
   ```typescript
   class Greeter {
     greeting: string;

     constructor(message: string) {
       this.greeting = message;
     }

     greet() {
       return `Hello, ${this.greeting}`;
     }
   }

   let greeter = new Greeter("world");
   ```

2. **Membros Públicos**
   - Por padrão, todos os membros de uma classe são públicos.
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
   ```

## Herança

1. **Herança Básica**
   - Uma classe pode estender outra classe.
   ```typescript
   class Dog extends Animal {
     bark() {
       console.log("Woof! Woof!");
     }
   }

   const dog = new Dog("Rex");
   dog.bark();  // "Woof! Woof!"
   dog.move(10);  // "Rex moved 10m."
   ```

2. **Sobrescrevendo Métodos**
   - Subclasses podem sobrescrever métodos da classe base.
   ```typescript
   class Bird extends Animal {
     move(distance: number = 5) {
       console.log("Flying...");
       super.move(distance);
     }
   }

   const bird = new Bird("Parrot");
   bird.move();  // "Flying... Parrot moved 5m."
   ```

## Membros Privados e Protegidos

1. **Membros Privados**
   - Membros privados só podem ser acessados dentro da classe que os define.
   ```typescript
   class Person {
     private name: string;

     constructor(name: string) {
       this.name = name;
     }

     getName() {
       return this.name;
     }
   }

   const person = new Person("Alice");
   // person.name; // Error: Property 'name' is private and only accessible within class 'Person'.
   console.log(person.getName());  // "Alice"
   ```

2. **Membros Protegidos**
   - Membros protegidos podem ser acessados por subclasses.
   ```typescript
   class Person {
     protected name: string;

     constructor(name: string) {
       this.name = name;
     }
   }

   class Employee extends Person {
     private department: string;

     constructor(name: string, department: string) {
       super(name);
       this.department = department;
     }

     getElevatorPitch() {
       return `Hello, my name is ${this.name} and I work in ${this.department}.`;
     }
   }

   const howard = new Employee("Howard", "Sales");
   console.log(howard.getElevatorPitch());  // "Hello, my name is Howard and I work in Sales."
   // console.log(howard.name); // Error: Property 'name' is protected and only accessible within class 'Person' and its subclasses.
   ```

## Membros Estáticos

1. **Definindo Membros Estáticos**
   - Membros estáticos são compartilhados por todas as instâncias da classe.
   ```typescript
   class Grid {
     static origin = { x: 0, y: 0 };

     calculateDistanceFromOrigin(point: { x: number; y: number; }) {
       let xDist = point.x - Grid.origin.x;
       let yDist = point.y - Grid.origin.y;
       return Math.sqrt(xDist * xDist + yDist * yDist);
     }
   }

   let grid1 = new Grid();
   console.log(Grid.origin);  // { x: 0, y: 0 }
   ```

## Classes Abstratas

1. **Definindo Classes Abstratas**
   - Classes abstratas não podem ser instanciadas diretamente e podem definir métodos abstratos.
   ```typescript
   abstract class Animal {
     abstract makeSound(): void;
     move(): void {
       console.log("Moving...");
     }
   }

   class Dog extends Animal {
     makeSound() {
       console.log("Bark!");
     }
   }

   const dog = new Dog();
   dog.makeSound();  // "Bark!"
   dog.move();  // "Moving..."
   ```

## Parâmetros de Propriedades

1. **Declaração de Propriedades no Construtor**
   - Propriedades podem ser declaradas diretamente no construtor.
   ```typescript
   class Person {
     constructor(private name: string, public age: number) {}

     getDetails() {
       return `Name: ${this.name}, Age: ${this.age}`;
     }
   }

   const person = new Person("Alice", 30);
   console.log(person.getDetails());  // "Name: Alice, Age: 30"
   ```

## Interfaces e Classes

1. **Implementando Interfaces**
   - Classes podem implementar interfaces.
   ```typescript
   interface ClockInterface {
     currentTime: Date;
     setTime(d: Date): void;
   }

   class Clock implements ClockInterface {
     currentTime: Date = new Date();

     setTime(d: Date) {
       this.currentTime = d;
     }

     constructor(h: number, m: number) {}
   }
   ```

## Dicas de Boas Práticas

1. **Use Membros Privados para Encapsulamento**: Protege dados internos e previne acesso externo não intencional.
2. **Aproveite Herança e Polimorfismo**: Facilita a reutilização e extensão de código.
3. **Prefira Interfaces para Definir Contratos**: Interfaces fornecem contratos claros e evitam dependências rígidas.
4. **Documente Métodos e Propriedades**: Melhora a legibilidade e manutenção do código.
