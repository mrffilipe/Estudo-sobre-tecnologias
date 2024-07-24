
# TypeScript em 5 Minutos - POO (Programação Orientada a Objetos)

TypeScript permite usar a programação orientada a objetos (POO) para organizar e estruturar seu código de forma eficiente, aproveitando os conceitos de classes, herança, interfaces e muito mais.

## Definindo uma Classe

1. **Classe Básica**
   - Defina uma classe com propriedades e métodos.
   ```typescript
   class Student {
     fullName: string;
     constructor(public firstName: string, public middleInitial: string, public lastName: string) {
       this.fullName = \`\${firstName} \${middleInitial} \${lastName}\`;
     }
   }

   interface Person {
     firstName: string;
     lastName: string;
   }

   function greeter(person: Person) {
     return \`Hello, \${person.firstName} \${person.lastName}\`;
   }

   let user = new Student("Jane", "M.", "User");

   console.log(greeter(user));
   ```

## Herança

1. **Criando uma Subclasse**
   - Use a palavra-chave `extends` para criar subclasses.
   ```typescript
   class Animal {
     move(distance: number = 0) {
       console.log(\`Animal moved \${distance}m.\`);
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

2. **Sobrescrevendo Métodos**
   - Subclasses podem sobrescrever métodos da classe base.
   ```typescript
   class Bird extends Animal {
     move(distance: number = 5) {
       console.log("Flying...");
       super.move(distance);
     }
   }

   const bird = new Bird();
   bird.move();  // "Flying... Animal moved 5m."
   ```

## Membros Públicos, Privados e Protegidos

1. **Membros Públicos**
   - Por padrão, todos os membros de uma classe são públicos.
   ```typescript
   class Animal {
     public name: string;
     public constructor(name: string) {
       this.name = name;
     }
     public move(distance: number) {
       console.log(\`\${this.name} moved \${distance}m.\`);
     }
   }
   ```

2. **Membros Privados**
   - Membros privados só podem ser acessados dentro da classe que os define.
   ```typescript
   class Animal {
     private name: string;
     constructor(name: string) {
       this.name = name;
     }
     move(distance: number) {
       console.log(\`\${this.name} moved \${distance}m.\`);
     }
   }
   ```

3. **Membros Protegidos**
   - Membros protegidos podem ser acessados por subclasses.
   ```typescript
   class Animal {
     protected name: string;
     constructor(name: string) {
       this.name = name;
     }
     move(distance: number) {
       console.log(\`\${this.name} moved \${distance}m.\`);
     }
   }

   class Dog extends Animal {
     bark() {
       console.log("Woof! Woof!");
     }
   }

   const dog = new Dog("Buddy");
   dog.bark();  // "Woof! Woof!"
   // dog.name; // Error: Property 'name' is protected and only accessible within class 'Animal' and its subclasses.
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
     return \`Hello, \${person.firstName} \${person.lastName}\`;
   }

   let user = { firstName: "Jane", lastName: "User" };

   console.log(greeter(user));
   ```

2. **Implementando Interfaces**
   - Classes podem implementar interfaces para garantir que elas seguem uma determinada estrutura.
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

## Parâmetros de Propriedades

1. **Declaração de Propriedades no Construtor**
   - Propriedades podem ser declaradas diretamente no construtor.
   ```typescript
   class Animal {
     constructor(public name: string) {}
     move(distance: number) {
       console.log(\`\${this.name} moved \${distance}m.\`);
     }
   }

   const cat = new Animal("Kitty");
   cat.move(10);  // "Kitty moved 10m."
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

## Dicas de Boas Práticas

1. **Use Tipos Explícitos**: Declare tipos explicitamente para melhorar a clareza e segurança do código.
2. **Aproveite Interfaces para Estruturas de Objetos**: Defina interfaces para padronizar a estrutura de objetos e facilitar a manutenção.
3. **Aproveite Herança e Polimorfismo**: Use classes e herança para criar componentes reutilizáveis e compartilhar funcionalidades comuns.
4. **Documente Métodos e Propriedades**: Melhora a legibilidade e manutenção do código.
