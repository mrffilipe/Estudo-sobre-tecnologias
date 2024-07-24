
# Tipos Condicionais no TypeScript

Os tipos condicionais no TypeScript permitem criar tipos que dependem de uma condição. Isso é útil para criar tipos dinâmicos e flexíveis que podem mudar com base em outros tipos.

## Sintaxe Básica de Tipos Condicionais

1. **Definindo um Tipo Condicional**
   - A sintaxe básica de um tipo condicional é `T extends U ? X : Y`.
   ```typescript
   type MessageOf<T> = T extends { message: unknown } ? T["message"] : never;
   ```

2. **Exemplo Prático**
   ```typescript
   interface Email {
     message: string;
   }

   interface Dog {
     bark(): void;
   }

   type EmailMessageContents = MessageOf<Email>;  // string
   type DogMessageContents = MessageOf<Dog>;      // never
   ```

## Tipos Condicionais com Inferência

1. **Usando `infer` para Inferir Tipos**
   - A palavra-chave `infer` permite capturar e reutilizar parte de um tipo em um tipo condicional.
   ```typescript
   type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
   ```

2. **Exemplo Prático**
   ```typescript
   type NumReturnType = GetReturnType<() => number>;  // number
   type StrReturnType = GetReturnType<(x: string) => string>;  // string
   ```

## Tipos Condicionais Distribuídos

1. **Distribuição em Uniões**
   - Tipos condicionais aplicam-se de forma distribuída em uniões.
   ```typescript
   type ToArray<T> = T extends any ? T[] : never;

   type StrArrOrNumArr = ToArray<string | number>;  // string[] | number[]
   ```

2. **Exemplo com Uniões**
   ```typescript
   type Exclude<T, U> = T extends U ? never : T;

   type T = Exclude<"a" | "b" | "c", "a" | "b">;  // "c"
   ```

## Tipos Condicionais Recursivos

1. **Definindo Tipos Recursivos**
   - Tipos condicionais podem ser usados recursivamente para criar tipos mais complexos.
   ```typescript
   type Flatten<T> = T extends Array<infer U> ? Flatten<U> : T;

   type Str = Flatten<string[]>;  // string
   type Num = Flatten<number[][][]>;  // number
   ```

## Combinação de Tipos Condicionais

1. **Combinando Vários Tipos Condicionais**
   - É possível combinar vários tipos condicionais para criar tipos mais refinados.
   ```typescript
   type TypeName<T> =
     T extends string ? "string" :
     T extends number ? "number" :
     T extends boolean ? "boolean" :
     T extends undefined ? "undefined" :
     T extends Function ? "function" :
     "object";
   ```

2. **Exemplo de Uso**
   ```typescript
   type T0 = TypeName<string>;  // "string"
   type T1 = TypeName<"a">;     // "string"
   type T2 = TypeName<true>;    // "boolean"
   type T3 = TypeName<() => void>;  // "function"
   ```

## Dicas de Boas Práticas

1. **Use Tipos Condicionais para Flexibilidade**: Permite criar tipos que se adaptam a diferentes cenários.
2. **Aproveite a Inferência de Tipos com `infer`**: Facilita a reutilização de partes de tipos em condicionais.
3. **Combine Tipos Condicionais para Maior Precisão**: Crie tipos mais específicos e refinados combinando múltiplos condicionais.
4. **Documente Tipos Condicionais Complexos**: Facilita o entendimento e a manutenção do código.
