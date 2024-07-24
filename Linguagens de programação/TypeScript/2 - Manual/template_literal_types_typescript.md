
# Tipos de Template Literals no TypeScript

Tipos de template literals no TypeScript permitem criar novos tipos combinando tipos literais com strings. Eles são úteis para criar tipos dinâmicos e flexíveis, especialmente ao trabalhar com strings.

## Definindo Tipos de Template Literals

1. **Sintaxe Básica**
   - A sintaxe é similar à dos template literals em JavaScript, mas usada em tipos.
   ```typescript
   type Greeting = `Hello, ${string}`;
   ```

2. **Exemplo Prático**
   ```typescript
   type Direction = "left" | "right";
   type Movement = `move-${Direction}`;  // "move-left" | "move-right"
   ```

## Usando Tipos de Template Literals com Tipos Literais

1. **Combinação com Tipos Literais**
   - Combine tipos literais para criar novos tipos.
   ```typescript
   type Color = "red" | "green" | "blue";
   type ColorMessage = `You selected ${Color}`;  // "You selected red" | "You selected green" | "You selected blue"
   ```

2. **Exemplo Prático**
   ```typescript
   type Animal = "cat" | "dog";
   type AnimalSound = `${Animal}-sound`;  // "cat-sound" | "dog-sound"
   ```

## Uso de Tipos de Template Literals com Tipos Genéricos

1. **Combinação com Tipos Genéricos**
   - Crie tipos dinâmicos usando tipos genéricos.
   ```typescript
   type EntityId<Entity extends string> = `${Entity}-id`;

   type UserId = EntityId<"user">;  // "user-id"
   type OrderId = EntityId<"order">;  // "order-id"
   ```

2. **Exemplo Prático**
   ```typescript
   type ApiEndpoint<Method extends string, Resource extends string> = `${Method} /api/${Resource}`;

   type GetUserEndpoint = ApiEndpoint<"GET", "users">;  // "GET /api/users"
   type CreateOrderEndpoint = ApiEndpoint<"POST", "orders">;  // "POST /api/orders"
   ```

## Manipulação de Strings com Tipos de Template Literals

1. **Interseção e União de Tipos**
   - Combine tipos de template literals com interseções e uniões.
   ```typescript
   type Position = "top" | "bottom";
   type Size = "small" | "large";
   type Style = `${Position}-${Size}`;  // "top-small" | "top-large" | "bottom-small" | "bottom-large"
   ```

2. **Exemplo Prático**
   ```typescript
   type Prefix = "pre" | "post";
   type Suffix = "fix" | "script";
   type Combined = `${Prefix}${Suffix}`;  // "prefix" | "prescript" | "postfix" | "postscript"
   ```

## Casos de Uso Avançados

1. **Verificação de Padrões em Strings**
   - Crie tipos para verificar se strings seguem certos padrões.
   ```typescript
   type HexColor = `#${string}`;
   type CssProperty = `${string}: ${string};`;
   ```

2. **Exemplo Prático**
   ```typescript
   type QueryParam = `${string}=${string}`;
   type QueryString = `?${QueryParam}&${QueryParam}`;
   ```

## Dicas de Boas Práticas

1. **Use Tipos de Template Literals para Padrões de Strings**: Ideal para validar e manipular strings que seguem padrões específicos.
2. **Combine com Tipos Genéricos para Flexibilidade**: Crie tipos dinâmicos e reutilizáveis usando template literals com tipos genéricos.
3. **Documente Tipos de Template Literals Complexos**: Facilita o entendimento e a manutenção do código.
4. **Teste e Valide Strings com Tipos de Template Literals**: Garantem que as strings sigam os formatos esperados.
