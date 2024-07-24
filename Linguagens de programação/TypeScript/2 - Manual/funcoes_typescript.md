
# Funções no TypeScript

Funções são um componente fundamental em qualquer linguagem de programação. No TypeScript, além dos conceitos básicos, há várias funcionalidades adicionais que melhoram a robustez e a clareza do código.

## Definindo Funções

1. **Sintaxe Básica**
   ```typescript
   function add(x: number, y: number): number {
     return x + y;
   }
   ```

2. **Expressões de Função**
   ```typescript
   let myAdd = function(x: number, y: number): number { return x + y; };
   ```

3. **Funções Anônimas**
   ```typescript
   let myAdd: (baseValue: number, increment: number) => number =
     function(x, y) { return x + y; };
   ```

## Tipos de Parâmetros e Retornos

1. **Parâmetros Opcionais e Padrão**
   ```typescript
   function buildName(firstName: string, lastName?: string) {
     return firstName + " " + (lastName || "");
   }

   function buildName(firstName: string, lastName = "Smith") {
     return firstName + " " + lastName;
   }
   ```

2. **Parâmetros Rest**
   ```typescript
   function buildName(firstName: string, ...restOfName: string[]) {
     return firstName + " " + restOfName.join(" ");
   }
   ```

## Funções como Tipos

1. **Definindo Tipos para Funções**
   ```typescript
   type Add = (a: number, b: number) => number;
   let add: Add = (x, y) => x + y;
   ```

2. **Inferência de Tipos**
   ```typescript
   let myAdd: (baseValue: number, increment: number) => number =
     function(x, y) { return x + y; };
   ```

## Sobrecarga de Funções

- Permite definir múltiplas assinaturas para uma função.
  ```typescript
  function pickCard(x: {suit: string; card: number; }[]): number;
  function pickCard(x: number): {suit: string; card: number; };
  function pickCard(x): any {
    if (typeof x == "object") {
      return Math.floor(Math.random() * x.length);
    } else if (typeof x == "number") {
      return { suit: "hearts", card: x % 13 };
    }
  }
  ```

## `this` em Funções

1. **Usando `this` em Funções**
   - Dentro de funções, o valor de `this` pode mudar dependendo de como a função é chamada.
   ```typescript
   let deck = {
     suits: ["hearts", "spades", "clubs", "diamonds"],
     cards: Array(52),
     createCardPicker: function() {
       return function() {
         let pickedCard = Math.floor(Math.random() * 52);
         let pickedSuit = Math.floor(pickedCard / 13);

         return {suit: this.suits[pickedSuit], card: pickedCard % 13};
       };
     }
   };

   let cardPicker = deck.createCardPicker();
   let pickedCard = cardPicker();

   alert("card: " + pickedCard.card + " of " + pickedCard.suit);
   ```

2. **Corrigindo o Valor de `this`**
   - Usando Arrow Functions para manter o valor de `this`.
   ```typescript
   let deck = {
     suits: ["hearts", "spades", "clubs", "diamonds"],
     cards: Array(52),
     createCardPicker: function() {
       return () => {
         let pickedCard = Math.floor(Math.random() * 52);
         let pickedSuit = Math.floor(pickedCard / 13);

         return {suit: this.suits[pickedSuit], card: pickedCard % 13};
       };
     }
   };

   let cardPicker = deck.createCardPicker();
   let pickedCard = cardPicker();

   alert("card: " + pickedCard.card + " of " + pickedCard.suit);
   ```

## Parâmetros `this`

- TypeScript permite adicionar um parâmetro explícito `this` em funções para melhorar a segurança de tipos.
  ```typescript
  interface Card {
    suit: string;
    card: number;
  }

  interface Deck {
    suits: string[];
    cards: number[];

    createCardPicker(this: Deck): () => Card;
  }

  let deck: Deck = {
    suits: ["hearts", "spades", "clubs", "diamonds"],
    cards: Array(52),
    createCardPicker: function(this: Deck) {
      return () => {
        let pickedCard = Math.floor(Math.random() * 52);
        let pickedSuit = Math.floor(pickedCard / 13);

        return {suit: this.suits[pickedSuit], card: pickedCard % 13};
      };
    }
  };

  let cardPicker = deck.createCardPicker();
  let pickedCard = cardPicker();

  alert("card: " + pickedCard.card + " of " + pickedCard.suit);
  ```

## Dicas de Boas Práticas

1. **Use Parâmetros Padrão e Opcionais para Flexibilidade**: Define valores padrão e marque parâmetros como opcionais para funções mais flexíveis.
2. **Aproveite Tipos para Funções**: Especificar tipos para funções melhora a clareza e previne erros.
3. **Utilize Arrow Functions para Manter o Contexto de `this`**: Arrow functions são úteis para garantir que o valor de `this` permanece consistente.
4. **Use Sobrecarga de Funções para Funções Complexas**: Definir múltiplas assinaturas pode tornar funções mais versáteis e compreensíveis.
