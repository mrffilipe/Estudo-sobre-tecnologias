
# Tipos Mapeados no TypeScript

Tipos mapeados no TypeScript permitem criar novos tipos transformando cada propriedade de um tipo existente. Eles são extremamente úteis para criar tipos dinâmicos e reutilizáveis.

## Definindo Tipos Mapeados

1. **Sintaxe Básica de Tipos Mapeados**
   - Use colchetes e a palavra-chave `in` para iterar sobre as propriedades de um tipo.
   ```typescript
   type OptionsFlags<Type> = {
     [Property in keyof Type]: boolean;
   };

   type FeatureFlags = {
     darkMode: () => void;
     newUserProfile: () => void;
   };

   type FeatureOptions = OptionsFlags<FeatureFlags>;
   // { darkMode: boolean; newUserProfile: boolean }
   ```

2. **Tipos Mapeados com Modificadores**
   - Você pode adicionar modificadores como `readonly` ou `?` para tornar as propriedades somente leitura ou opcionais.
   ```typescript
   type Mutable<Type> = {
     -readonly [Property in keyof Type]: Type[Property];
   };

   type Optional<Type> = {
     [Property in keyof Type]?: Type[Property];
   };
   ```

## Tipos Mapeados e Tipos Condicionais

1. **Combinando Tipos Mapeados com Tipos Condicionais**
   - Crie tipos que mudam com base em uma condição.
   ```typescript
   type ExtractStringKeys<T> = {
     [K in keyof T]: T[K] extends string ? K : never
   }[keyof T];

   type Person = {
     name: string;
     age: number;
     location: string;
   };

   type StringKeysOfPerson = ExtractStringKeys<Person>;
   // "name" | "location"
   ```

## Exemplos Comuns de Tipos Mapeados

1. **`Partial`**
   - Torna todas as propriedades de um tipo opcionais.
   ```typescript
   type Partial<Type> = {
     [Property in keyof Type]?: Type[Property];
   };

   type Person = {
     name: string;
     age: number;
   };

   type PartialPerson = Partial<Person>;
   // { name?: string; age?: number }
   ```

2. **`Required`**
   - Torna todas as propriedades de um tipo obrigatórias.
   ```typescript
   type Required<Type> = {
     [Property in keyof Type]-?: Type[Property];
   };

   type PartialPerson = {
     name?: string;
     age?: number;
   };

   type RequiredPerson = Required<PartialPerson>;
   // { name: string; age: number }
   ```

3. **`Readonly`**
   - Torna todas as propriedades de um tipo somente leitura.
   ```typescript
   type Readonly<Type> = {
     readonly [Property in keyof Type]: Type[Property];
   };

   type Person = {
     name: string;
     age: number;
   };

   type ReadonlyPerson = Readonly<Person>;
   // { readonly name: string; readonly age: number }
   ```

4. **`Pick`**
   - Seleciona um conjunto de propriedades de um tipo.
   ```typescript
   type Pick<Type, Keys extends keyof Type> = {
     [Property in Keys]: Type[Property];
   };

   type Person = {
     name: string;
     age: number;
     location: string;
   };

   type PersonNameAndAge = Pick<Person, "name" | "age">;
   // { name: string; age: number }
   ```

5. **`Record`**
   - Cria um tipo de objeto com um conjunto específico de chaves e valores.
   ```typescript
   type Record<Keys extends keyof any, Type> = {
     [Property in Keys]: Type;
   };

   type ThreeStringProps = Record<"prop1" | "prop2" | "prop3", string>;
   // { prop1: string; prop2: string; prop3: string }
   ```

## Dicas de Boas Práticas

1. **Use Tipos Mapeados para Transformações Comuns**: Utilitários como `Partial`, `Readonly`, `Required`, `Pick` e `Record` são extremamente úteis.
2. **Combine Tipos Mapeados com Tipos Condicionais**: Crie tipos mais flexíveis e dinâmicos.
3. **Documente Seus Tipos Mapeados**: Facilita o entendimento e a manutenção do código.
4. **Aproveite Modificadores em Tipos Mapeados**: Use modificadores `readonly` e `?` para controlar a mutabilidade e opcionalidade das propriedades.
