
# Tipos Derivados no TypeScript

O TypeScript permite criar novos tipos baseados em tipos existentes usando uma variedade de operadores e utilitários. Isso aumenta a flexibilidade e a reutilização de tipos.

## Index Types (Tipos de Índice)

Os tipos de índice permitem acessar o tipo de uma propriedade de um objeto.

```typescript
type Person = { name: string; age: number };
type Name = Person["name"];  // string
```

## Chaves de Tipo

Você pode criar tipos baseados nas chaves de um objeto.

```typescript
type Person = { name: string; age: number };
type PersonKeys = keyof Person;  // "name" | "age"
```

## Tipos de Mapeamento

Os tipos de mapeamento permitem criar novos tipos transformando cada propriedade de um tipo existente.

```typescript
type Person = { name: string; age: number };
type ReadonlyPerson = { readonly [K in keyof Person]: Person[K] };
```

## Tipos Condicionais

Os tipos condicionais permitem criar tipos que mudam com base em uma condição.

```typescript
type MessageOf<T> = T extends { message: unknown } ? T["message"] : never;
```

## Inferência de Tipos Condicionais

Você pode usar a palavra-chave `infer` para capturar e reutilizar parte de um tipo.

```typescript
type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
```

## `Partial` e `Required`

- `Partial<T>` cria um tipo onde todas as propriedades são opcionais.
- `Required<T>` cria um tipo onde todas as propriedades são obrigatórias.

```typescript
interface Person {
  name: string;
  age?: number;
}

type PartialPerson = Partial<Person>;  // { name?: string; age?: number }
type RequiredPerson = Required<Person>;  // { name: string; age: number }
```

## `Readonly` e `Mutable`

- `Readonly<T>` cria um tipo onde todas as propriedades são somente leitura.
- `Mutable<T>` faz o inverso, tornando todas as propriedades mutáveis.

```typescript
interface Person {
  name: string;
  age: number;
}

type ReadonlyPerson = Readonly<Person>;  // { readonly name: string; readonly age: number }
type MutablePerson = { -readonly [K in keyof ReadonlyPerson]: ReadonlyPerson[K] };  // { name: string; age: number }
```

## `Pick` e `Omit`

- `Pick<T, K>` cria um tipo selecionando um conjunto de propriedades de `T`.
- `Omit<T, K>` cria um tipo omitindo um conjunto de propriedades de `T`.

```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

type NameAndAge = Pick<Person, "name" | "age">;  // { name: string; age: number }
type AddressOnly = Omit<Person, "name" | "age">;  // { address: string }
```

## `Extract` e `Exclude`

- `Extract<T, U>` cria um tipo extraindo de `T` apenas os tipos que são atribuíveis a `U`.
- `Exclude<T, U>` cria um tipo excluindo de `T` todos os tipos que são atribuíveis a `U`.

```typescript
type T = "a" | "b" | "c";
type U = "a" | "b";

type Extracted = Extract<T, U>;  // "a" | "b"
type Excluded = Exclude<T, U>;  // "c"
```

## `Record`

- `Record<K, T>` cria um tipo de objeto com as chaves de `K` e valores de `T`.

```typescript
type ThreeStringProps = Record<"prop1" | "prop2" | "prop3", string>;
// { prop1: string; prop2: string; prop3: string }
```

## `NonNullable`

- `NonNullable<T>` remove `null` e `undefined` de `T`.

```typescript
type T = string | number | null | undefined;
type NonNullableT = NonNullable<T>;  // string | number
```

## Dicas de Boas Práticas

1. **Use Tipos Derivados para Simplificar Tipos Complexos**: Facilita a manutenção e compreensão do código.
2. **Prefira `Partial`, `Readonly`, `Pick` e `Omit` para Transformações Comuns**: Utilitários embutidos são otimizados e bem compreendidos pela comunidade.
3. **Aproveite Tipos Condicionais para Flexibilidade Máxima**: Permite criar tipos dinâmicos baseados em condições.
4. **Utilize `Record` para Mapear Chaves Conhecidas**: Útil para criar objetos com chaves dinâmicas e tipos de valores consistentes.
