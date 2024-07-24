
# Generics no TypeScript

Generics são uma poderosa ferramenta em TypeScript que permite criar componentes reutilizáveis que funcionam com diferentes tipos. Eles fornecem uma maneira de criar funções, classes e interfaces que podem trabalhar com qualquer tipo, mantendo a tipagem segura.

## Funções Genéricas

1. **Função Genérica Básica**
   ```typescript
   function identity<T>(arg: T): T {
     return arg;
   }

   let output = identity<string>("myString");  // output: "myString"
   let output2 = identity<number>(42);  // output2: 42
   ```

2. **Inferência de Tipo**
   - TypeScript pode inferir o tipo genérico com base no argumento passado.
   ```typescript
   let output = identity("myString");  // Tipo inferido como string
   ```

## Arrays Genéricos

1. **Usando Genéricos com Arrays**
   ```typescript
   function loggingIdentity<T>(arg: T[]): T[] {
     console.log(arg.length);  // Array tem uma propriedade 'length', então isso está ok
     return arg;
   }
   ```

## Tipos Genéricos em Interfaces e Tipos

1. **Interface Genérica**
   ```typescript
   interface GenericIdentityFn<T> {
     (arg: T): T;
   }

   function identity<T>(arg: T): T {
     return arg;
   }

   let myIdentity: GenericIdentityFn<number> = identity;
   ```

2. **Tipo Genérico**
   ```typescript
   type GenericIdentityFn<T> = (arg: T) => T;

   function identity<T>(arg: T): T {
     return arg;
   }

   let myIdentity: GenericIdentityFn<number> = identity;
   ```

## Classes Genéricas

1. **Classe Genérica Básica**
   ```typescript
   class GenericNumber<T> {
     zeroValue: T;
     add: (x: T, y: T) => T;
   }

   let myGenericNumber = new GenericNumber<number>();
   myGenericNumber.zeroValue = 0;
   myGenericNumber.add = function(x, y) { return x + y; };
   ```

## Restrições Genéricas

1. **Usando Restrições em Genéricos**
   - Adicionando restrições para garantir que um tipo genérico tenha certas propriedades.
   ```typescript
   interface Lengthwise {
     length: number;
   }

   function loggingIdentity<T extends Lengthwise>(arg: T): T {
     console.log(arg.length);  // Agora sabemos que 'arg' tem uma propriedade 'length'
     return arg;
   }

   loggingIdentity({length: 10, value: 3});  // Ok
   ```

## Parâmetros de Tipo em Parâmetros de Tipo

1. **Usando Múltiplos Parâmetros de Tipo**
   ```typescript
   function getProperty<T, K extends keyof T>(obj: T, key: K) {
     return obj[key];
   }

   let x = { a: 1, b: 2, c: 3, d: 4 };

   getProperty(x, "a"); // Ok
   getProperty(x, "m"); // Erro: Argument of type '"m"' isn't assignable to parameter of type '"a" | "b" | "c" | "d"'.
   ```

## Classes Genéricas com Restrições

1. **Classe com Restrições Genéricas**
   ```typescript
   class BeeKeeper {
     hasMask: boolean;
   }

   class ZooKeeper {
     nametag: string;
   }

   class Animal {
     numLegs: number;
   }

   class Bee extends Animal {
     keeper: BeeKeeper;
   }

   class Lion extends Animal {
     keeper: ZooKeeper;
   }

   function createInstance<A extends Animal>(c: new () => A): A {
     return new c();
   }

   createInstance(Lion).keeper.nametag;  // Ok
   createInstance(Bee).keeper.hasMask;   // Ok
   ```

## Dicas de Boas Práticas

1. **Use Genéricos para Reutilização de Código**: Genéricos permitem criar componentes altamente reutilizáveis.
2. **Adicione Restrições Apenas Quando Necessário**: Restrições em genéricos devem ser usadas para garantir que os tipos atendam a certos requisitos.
3. **Aproveite a Inferência de Tipos do TypeScript**: Deixe o TypeScript inferir tipos genéricos quando possível para simplificar o código.
4. **Documente Suas Funções e Classes Genéricas**: Facilita o entendimento do propósito e uso correto dos genéricos.
