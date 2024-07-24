
# Tipos Básicos no TypeScript

O TypeScript oferece um sistema de tipos que adiciona segurança e legibilidade ao código JavaScript. A seguir, estão os principais tipos básicos suportados pelo TypeScript:

## Tipos Primitivos

1. **Boolean**
   ```typescript
   let isDone: boolean = false;
   ```

2. **Number**
   ```typescript
   let decimal: number = 6;
   let hex: number = 0xf00d;
   let binary: number = 0b1010;
   let octal: number = 0o744;
   ```

3. **String**
   ```typescript
   let color: string = "blue";
   color = 'red';
   ```

4. **Array**
   - Usando tipo de elemento seguido por `[]`
     ```typescript
     let list: number[] = [1, 2, 3];
     ```
   - Usando `Array<tipo>`
     ```typescript
     let list: Array<number> = [1, 2, 3];
     ```

5. **Tuple**
   ```typescript
   let x: [string, number];
   x = ["hello", 10]; // OK
   ```

6. **Enum**
   ```typescript
   enum Color {Red, Green, Blue}
   let c: Color = Color.Green;
   ```

7. **Any**
   - Útil para quando você não conhece o tipo exato no momento da escrita do código.
     ```typescript
     let notSure: any = 4;
     notSure = "maybe a string instead";
     notSure = false; // okay, definitely a boolean
     ```

8. **Void**
   - Usado em funções que não retornam valor.
     ```typescript
     function warnUser(): void {
       console.log("This is my warning message");
     }
     ```
   - Pode ser usado em variáveis, mas apenas com `undefined` ou `null`.
     ```typescript
     let unusable: void = undefined;
     ```

9. **Null e Undefined**
   ```typescript
   let u: undefined = undefined;
   let n: null = null;
   ```

10. **Never**
    - Representa o tipo de valores que nunca ocorrem.
    ```typescript
    function error(message: string): never {
      throw new Error(message);
    }
    ```

11. **Object**
    - Tipo não primitivo que representa qualquer valor que não seja `number`, `string`, `boolean`, `symbol`, `null` ou `undefined`.
    ```typescript
    declare function create(o: object | null): void;
    create({ prop: 0 }); // OK
    create(null); // OK
    ```

## Tipagem por Inferência

TypeScript pode inferir o tipo de uma variável baseado no valor inicial atribuído a ela.
```typescript
let someValue = "this is a string";
```

## Tipo União

Permite que uma variável tenha mais de um tipo.
```typescript
let value: string | number;
value = "hello"; // OK
value = 10; // OK
```

## Alias de Tipo

Definem novos nomes para tipos existentes.
```typescript
type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
function getName(n: NameOrResolver): Name {
  if (typeof n === "string") {
    return n;
  } else {
    return n();
  }
}
```

## Interface

Definem a estrutura de um objeto.
```typescript
interface User {
  name: string;
  age: number;
}
let user: User = {
  name: "John",
  age: 30
};
```

## Dicas de Boas Práticas

1. **Utilize Tipos Sempre que Possível**: Definir tipos ajuda a prevenir erros e torna o código mais legível.
2. **Prefira Tipagem Estrita**: Evite usar `any` a menos que seja absolutamente necessário.
3. **Use Interfaces e Tipos Customizados para Estruturas Complexas**: Isso melhora a clareza e a manutenção do código.
4. **Aproveite a Inferência de Tipo do TypeScript**: Deixe o TypeScript inferir tipos quando apropriado para reduzir a verbosidade do código.
