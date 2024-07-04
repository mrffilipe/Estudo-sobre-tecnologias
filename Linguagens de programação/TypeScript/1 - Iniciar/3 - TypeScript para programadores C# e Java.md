
# TypeScript em 5 Minutos com Programação Orientada a Objetos (POO)

## Introdução

TypeScript facilita a adoção de conceitos de Programação Orientada a Objetos (POO) no desenvolvimento JavaScript. Ele permite criar classes, interfaces, herança e outros conceitos POO, proporcionando um código mais estruturado e reutilizável.

## Primeiros Passos

1. **Instalação do TypeScript**
   ```bash
   npm install -g typescript
   ```
   Este comando instala o compilador TypeScript globalmente.

2. **Compilação de um Arquivo TypeScript**
   - Crie um arquivo chamado `greeter.ts` com o seguinte conteúdo:
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
   - Compile o arquivo TypeScript para JavaScript:
     ```bash
     tsc greeter.ts
     ```
   - Isso gera um arquivo `greeter.js` que pode ser executado com Node.js:
     ```bash
     node greeter.js
     ```

## Classes

TypeScript permite a criação de classes para definir objetos e suas funcionalidades. No exemplo acima, a classe `Student` possui um construtor e uma propriedade `fullName`.

## Interfaces

Interfaces definem a estrutura esperada para objetos, garantindo que eles possuam as propriedades necessárias. A interface `Person` define que um objeto deve ter as propriedades `firstName` e `lastName`.

## Herança

TypeScript suporta herança, permitindo que uma classe derive de outra. Isso facilita a reutilização de código e a criação de hierarquias de classes.

```typescript
class Animal {
  constructor(public name: string) {}
  move(distanceInMeters: number = 0) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}

class Dog extends Animal {
  bark() {
    console.log('Woof! Woof!');
  }
}

const dog = new Dog('Rex');
dog.bark();
dog.move(10);
```

## Modificadores de Acesso

TypeScript oferece modificadores de acesso para controlar a visibilidade das propriedades e métodos das classes. Os principais modificadores são:

- `public`: Propriedades e métodos são acessíveis de qualquer lugar.
- `private`: Propriedades e métodos são acessíveis apenas dentro da classe.
- `protected`: Propriedades e métodos são acessíveis dentro da classe e subclasses.

```typescript
class Animal {
  private name: string;
  constructor(theName: string) { this.name = theName; }
  move(distanceInMeters: number) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}
```

## Boas Práticas

- **Utilize Classes e Interfaces**: Aproveite as classes e interfaces para criar um código mais organizado e modular.
- **Modificadores de Acesso**: Use modificadores de acesso para encapsular dados e métodos, garantindo a integridade dos objetos.
- **Herança com Cuidado**: Utilize herança para reutilizar código, mas evite criar hierarquias muito profundas, pois podem dificultar a manutenção.
