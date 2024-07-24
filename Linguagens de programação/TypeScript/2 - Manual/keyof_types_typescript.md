
# Tipos `keyof` no TypeScript

O operador `keyof` no TypeScript é usado para criar um tipo que consiste nas chaves de um outro tipo. Isso é útil para criar tipos dinâmicos e melhorar a segurança do código.

## Usando o Operador `keyof`

1. **Definindo `keyof`**
   - O operador `keyof` retorna um tipo que é uma união de todas as chaves de um objeto.
   ```typescript
   interface Person {
     name: string;
     age: number;
   }

   type PersonKeys = keyof Person;  // "name" | "age"
   ```

2. **Acessando Tipos de Propriedade**
   - Usando `keyof` junto com tipos de índice para acessar tipos de propriedade.
   ```typescript
   function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
     return obj[key];
   }

   let person: Person = { name: "Alice", age: 25 };
   let personName = getProperty(person, "name");  // string
   let personAge = getProperty(person, "age");    // number
   ```

## Usando `keyof` com Classes

1. **`keyof` em Classes**
   - `keyof` pode ser usado para acessar chaves de propriedades de classes.
   ```typescript
   class Car {
     make: string;
     model: string;
     year: number;

     constructor(make: string, model: string, year: number) {
       this.make = make;
       this.model = model;
       this.year = year;
     }
   }

   type CarKeys = keyof Car;  // "make" | "model" | "year"
   ```

## Tipos Condicionais com `keyof`

1. **Filtrando Chaves com Tipos Condicionais**
   - Usar tipos condicionais para filtrar chaves específicas.
   ```typescript
   interface Person {
     name: string;
     age: number;
     location?: string;
   }

   type OptionalKeys<T> = {
     [K in keyof T]: undefined extends T[K] ? K : never
   }[keyof T];

   type PersonOptionalKeys = OptionalKeys<Person>;  // "location"
   ```

## `keyof` e Genéricos

1. **Genéricos com `keyof`**
   - Criando funções genéricas que utilizam `keyof`.
   ```typescript
   function pluck<T, K extends keyof T>(obj: T, keys: K[]): T[K][] {
     return keys.map(key => obj[key]);
   }

   let person: Person = { name: "Alice", age: 25, location: "Wonderland" };
   let personProps = pluck(person, ["name", "location"]);  // [string, string?]
   ```

## Mapeamento de Tipos com `keyof`

1. **Criando Mapeamentos**
   - Usando `keyof` para criar mapeamentos de tipos.
   ```typescript
   type MappedType<T> = {
     [K in keyof T]: T[K];
   };

   type PersonMapped = MappedType<Person>;
   ```

## `keyof` com `typeof`

1. **Usando `typeof` e `keyof` Juntos**
   - Combinar `typeof` e `keyof` para criar tipos dinamicamente baseados em objetos existentes.
   ```typescript
   const person = {
     name: "Alice",
     age: 25,
   };

   type PersonType = typeof person;
   type PersonKeys = keyof PersonType;  // "name" | "age"
   ```

## Dicas de Boas Práticas

1. **Use `keyof` para Melhorar a Segurança de Tipagem**: Utilize `keyof` para criar tipos dinâmicos e seguros.
2. **Combine `keyof` com Genéricos para Flexibilidade**: Crie funções e tipos mais reutilizáveis e flexíveis.
3. **Utilize Tipos Condicionais para Filtragem de Chaves**: Aplique tipos condicionais para criar tipos mais específicos baseados em chaves.
4. **Aproveite `typeof` e `keyof` Juntos**: Use `typeof` para capturar a estrutura de objetos e `keyof` para trabalhar dinamicamente com suas chaves.
