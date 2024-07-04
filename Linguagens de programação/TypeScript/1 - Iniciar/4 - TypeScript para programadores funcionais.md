
# TypeScript em 5 Minutos com Funções

## Introdução

TypeScript permite a utilização de funções de forma mais segura e robusta, fornecendo tipagem estática e outras funcionalidades avançadas que ajudam a evitar erros comuns no desenvolvimento com JavaScript.

## Primeiros Passos

1. **Instalação do TypeScript**
   ```bash
   npm install -g typescript
   ```
   Este comando instala o compilador TypeScript globalmente.

2. **Compilação de um Arquivo TypeScript**
   - Crie um arquivo chamado `functions.ts` com o seguinte conteúdo:
     ```typescript
     function add(x: number, y: number): number {
       return x + y;
     }

     let result = add(2, 3);
     console.log(result);
     ```
   - Compile o arquivo TypeScript para JavaScript:
     ```bash
     tsc functions.ts
     ```
   - Isso gera um arquivo `functions.js` que pode ser executado com Node.js:
     ```bash
     node functions.js
     ```

## Funções com Tipos

TypeScript permite definir tipos para os parâmetros e para o retorno das funções. Isso ajuda a garantir que as funções sejam usadas corretamente.

```typescript
function greet(name: string): string {
  return `Hello, ${name}!`;
}

let greeting = greet("World");
console.log(greeting);
```

## Parâmetros Opcionais e Padrão

É possível definir parâmetros opcionais e padrões em funções TypeScript.

- **Parâmetros Opcionais**: Use `?` para marcar um parâmetro como opcional.
  ```typescript
  function buildName(firstName: string, lastName?: string): string {
    if (lastName) {
      return `${firstName} ${lastName}`;
    } else {
      return firstName;
    }
  }

  let result1 = buildName("Bob");
  let result2 = buildName("Bob", "Adams");
  ```

- **Parâmetros Padrão**: Defina um valor padrão para o parâmetro.
  ```typescript
  function buildNameWithDefault(firstName: string, lastName = "Smith"): string {
    return `${firstName} ${lastName}`;
  }

  let result1 = buildNameWithDefault("Bob");
  let result2 = buildNameWithDefault("Bob", "Adams");
  ```

## Parâmetros Rest

Funções em TypeScript podem usar parâmetros rest para aceitar um número variável de argumentos.

```typescript
function buildNameWithRest(firstName: string, ...restOfName: string[]): string {
  return `${firstName} ${restOfName.join(" ")}`;
}

let employeeName = buildNameWithRest("Joseph", "Samuel", "Lucas", "MacKinzie");
console.log(employeeName);
```

## Sobrecarga de Funções

TypeScript suporta sobrecarga de funções, permitindo definir múltiplas assinaturas para uma função.

```typescript
function pickCard(x: { suit: string; card: number }[]): number;
function pickCard(x: number): { suit: string; card: number };
function pickCard(x: any): any {
  if (typeof x == "object") {
    return Math.floor(Math.random() * x.length);
  } else if (typeof x == "number") {
    let suits = ["hearts", "spades", "clubs", "diamonds"];
    let pickedSuit = Math.floor(x / 13);
    return { suit: suits[pickedSuit], card: x % 13 };
  }
}

let myDeck = [
  { suit: "diamonds", card: 2 },
  { suit: "spades", card: 10 },
  { suit: "hearts", card: 4 },
];
let pickedCard1 = myDeck[pickCard(myDeck)];
let pickedCard2 = pickCard(15);

console.log(`card: ${pickedCard1.card} of ${pickedCard1.suit}`);
console.log(`card: ${pickedCard2.card} of ${pickedCard2.suit}`);
```

## Boas Práticas

- **Tipagem Consistente**: Sempre defina tipos para os parâmetros e retorno das funções.
- **Utilize Parâmetros Opcionais e Padrão**: Facilita o uso das funções e evita erros.
- **Parâmetros Rest**: Use parâmetros rest para funções que aceitam um número variável de argumentos.
- **Sobrecarga de Funções**: Defina sobrecargas para funções que têm múltiplas assinaturas, tornando-as mais flexíveis e seguras.
