
# Narrowing no TypeScript

Narrowing (afunilamento) é o processo de refinamento dos tipos de variáveis no TypeScript. Através de diferentes técnicas, o TypeScript pode inferir tipos mais específicos, melhorando a segurança e a precisão do código.

## Técnicas de Narrowing

1. **Verificações de Tipo (Type Guards)**
   - Usando operadores `typeof` e `instanceof`, é possível afunilar tipos em blocos condicionais.
   ```typescript
   function padLeft(value: string, padding: string | number) {
     if (typeof padding === "number") {
       return Array(padding + 1).join(" ") + value;
     }
     if (typeof padding === "string") {
       return padding + value;
     }
     throw new Error(`Expected string or number, got '${padding}'.`);
   }
   ```

2. **Verificação de Igualdade**
   - Comparações diretas podem ajudar a afunilar tipos.
   ```typescript
   function example(x: string | number, y: string | boolean) {
     if (x === y) {
       // x e y são do tipo string
       x.toUpperCase();
       y.toUpperCase();
     } else {
       console.log(x);
       console.log(y);
     }
   }
   ```

3. **Verificações de `in`**
   - Verificar a existência de uma propriedade específica pode ajudar a determinar tipos.
   ```typescript
   interface Bird {
     fly(): void;
     layEggs(): void;
   }

   interface Fish {
     swim(): void;
     layEggs(): void;
   }

   function getAnimal(animal: Bird | Fish) {
     if ("fly" in animal) {
       animal.fly();
     } else {
       animal.swim();
     }
   }
   ```

4. **Verificação de `instanceof`**
   - Determinar se um objeto é instância de uma classe.
   ```typescript
   function logValue(x: Date | string) {
     if (x instanceof Date) {
       console.log(x.toUTCString());
     } else {
       console.log(x.toUpperCase());
     }
   }
   ```

5. **Verificação de Tipos Personalizados**
   - Usando predicados de tipo (type predicates) para criar guardas de tipos customizados.
   ```typescript
   interface Cat {
     meow(): void;
   }

   interface Dog {
     bark(): void;
   }

   function isCat(animal: Cat | Dog): animal is Cat {
     return (animal as Cat).meow !== undefined;
   }

   function makeSound(animal: Cat | Dog) {
     if (isCat(animal)) {
       animal.meow();
     } else {
       animal.bark();
     }
   }
   ```

## Verificações de Discriminadores

- Usar propriedades comuns para distinguir entre tipos dentro de uma união.
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

interface Circle {
  kind: "circle";
  radius: number;
}

type Shape = Square | Rectangle | Circle;

function area(shape: Shape) {
  switch (shape.kind) {
    case "square":
      return shape.size * shape.size;
    case "rectangle":
      return shape.width * shape.height;
    case "circle":
      return Math.PI * shape.radius ** 2;
  }
}
```

## Afunilamento por Exceções

- Usar blocos try/catch para afunilar tipos com base em possíveis erros.
```typescript
function getStringValue(x: number | string): string {
  try {
    if (typeof x === "string") {
      return x;
    }
    throw new Error("Not a string");
  } catch (e) {
    return "Error";
  }
}
```

## Dicas de Boas Práticas

1. **Use Guardas de Tipo Sempre que Possível**: Aplicar verificações de tipo melhora a robustez e a clareza do código.
2. **Prefira Verificações de Discriminadores**: Quando trabalhar com tipos de união, utilize propriedades comuns para afunilar tipos.
3. **Aproveite Predicados de Tipo**: Crie guardas de tipos personalizadas para melhorar a legibilidade e segurança do código.
4. **Combine Técnicas para Máxima Precisão**: Utilize uma combinação de técnicas de narrowing para garantir que seu código lide corretamente com todos os casos possíveis.
