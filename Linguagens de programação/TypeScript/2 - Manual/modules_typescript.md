
# Módulos no TypeScript

Os módulos no TypeScript permitem organizar e encapsular código em diferentes arquivos e namespaces, facilitando a reutilização e manutenção do código.

## Importação e Exportação

1. **Exportando Declarations**
   - Você pode exportar qualquer declaração (classe, função, variável, etc.) usando a palavra-chave `export`.
   ```typescript
   // math.ts
   export function add(x: number, y: number): number {
     return x + y;
   }
   ```

2. **Importando Declarations**
   - Use a palavra-chave `import` para trazer declarações de outros módulos.
   ```typescript
   // main.ts
   import { add } from "./math";
   console.log(add(2, 3));  // 5
   ```

## Exportações Nomeadas e Padrão

1. **Exportações Nomeadas**
   - Você pode ter várias exportações nomeadas em um módulo.
   ```typescript
   // math.ts
   export const pi = 3.14;
   export function multiply(x: number, y: number): number {
     return x * y;
   }
   ```

2. **Exportação Padrão**
   - Cada módulo pode ter uma exportação padrão que é importada sem chaves.
   ```typescript
   // person.ts
   export default class Person {
     constructor(public name: string) {}
   }

   // main.ts
   import Person from "./person";
   const person = new Person("Alice");
   console.log(person.name);  // "Alice"
   ```

## Reexportação

1. **Reexportando Módulos**
   - Você pode reexportar de outro módulo para criar um ponto central de exportação.
   ```typescript
   // shapes.ts
   export * from "./circle";
   export * from "./square";
   ```

2. **Reexportando com Alias**
   - Use `as` para renomear durante a reexportação.
   ```typescript
   // geometry.ts
   export { Circle as MyCircle } from "./circle";
   ```

## Módulos e Namespaces

1. **Diferença entre Módulos e Namespaces**
   - Módulos são o principal meio de organizar código e dependências, enquanto namespaces são usados para agrupar lógicamente código dentro de um módulo.

2. **Namespace Interno**
   - Dentro de um módulo, você pode usar namespaces para organizar código.
   ```typescript
   // shapes.ts
   export namespace Shapes {
     export class Circle {
       constructor(public radius: number) {}
     }
     export class Square {
       constructor(public sideLength: number) {}
     }
   }
   ```

3. **Acessando Namespaces**
   - Importe o módulo e acesse os membros do namespace.
   ```typescript
   // main.ts
   import { Shapes } from "./shapes";
   let circle = new Shapes.Circle(5);
   let square = new Shapes.Square(10);
   ```

## Carregamento de Módulos

1. **Configuração do `moduleResolution` no tsconfig.json**
   - Configure a resolução de módulos usando `moduleResolution`.
   ```json
   {
     "compilerOptions": {
       "module": "commonjs",
       "moduleResolution": "node"
     }
   }
   ```

2. **Carregadores de Módulos**
   - TypeScript suporta vários sistemas de módulos, incluindo `CommonJS`, `AMD`, `SystemJS` e ES6 módulos.
   ```typescript
   // CommonJS
   const math = require("./math");
   console.log(math.add(2, 3));  // 5
   ```

## Dicas de Boas Práticas

1. **Prefira Exportações Padrão para Módulos Únicos**: Facilita a importação e manutenção do código.
2. **Use Exportações Nomeadas para Várias Declarations**: Torna claro o que está sendo exportado e importado.
3. **Reexporte para Ponto Único de Acesso**: Centralize exportações para facilitar o gerenciamento de dependências.
4. **Organize Código com Namespaces Quando Necessário**: Use namespaces para agrupar lógicamente código relacionado dentro de um módulo.
