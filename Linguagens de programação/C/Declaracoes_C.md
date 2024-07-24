
# Declarações na Linguagem C

## Visão Geral
Declarações são as instruções executáveis em um programa C. Elas definem as ações que o programa deve realizar, como controle de fluxo, operações aritméticas, chamadas de funções e outras operações. As declarações são componentes fundamentais para a lógica de um programa.

## Tipos de Declarações

### Declarações de Expressão
- Executam expressões, incluindo chamadas de função, operações aritméticas e atribuições.
- Exemplo:
  ```c
  a = 5;
  b = a + 2;
  printf("Hello, World!
");
  ```

### Declarações Compostas
- Agrupam várias declarações em um bloco delimitado por `{}`.
- Exemplo:
  ```c
  {
      int a = 10;
      int b = 20;
      printf("%d
", a + b);
  }
  ```

### Declarações de Seleção
- Controlam o fluxo de execução com base em condições.
- `if`, `else`, `switch`
- Exemplo:
  ```c
  if (a > b) {
      printf("A é maior que B
");
  } else {
      printf("A não é maior que B
");
  }

  switch (a) {
      case 1:
          printf("A é 1
");
          break;
      default:
          printf("A não é 1
");
  }
  ```

### Declarações de Iteração
- Executam um bloco de código várias vezes.
- `while`, `do-while`, `for`
- Exemplo:
  ```c
  while (a < 10) {
      printf("%d
", a);
      a++;
  }

  do {
      printf("%d
", b);
      b--;
  } while (b > 0);

  for (int i = 0; i < 5; i++) {
      printf("%d
", i);
  }
  ```

### Declarações de Salto
- Alteram o fluxo de execução, geralmente de forma não linear.
- `break`, `continue`, `return`, `goto`
- Exemplo:
  ```c
  for (int i = 0; i < 10; i++) {
      if (i == 5) {
          break;
      }
      printf("%d
", i);
  }

  for (int j = 0; j < 10; j++) {
      if (j % 2 == 0) {
          continue;
      }
      printf("%d
", j);
  }

  int func() {
      return 0;
  }

  goto label;
  label:
  printf("Usando goto
");
  ```

### Declarações de Labeled
- Usadas com `goto` para indicar o destino do salto.
- Exemplo:
  ```c
  label:
  printf("Este é um rótulo
");
  ```

## Dicas de Boas Práticas
- **Estruture o Código Claramente:** Utilize indentação e espaçamento consistentes para melhorar a legibilidade.
- **Evite `goto`:** O uso de `goto` pode tornar o código difícil de seguir e manter.
- **Inicialize Variáveis:** Sempre inicialize variáveis antes de usá-las para evitar comportamento indefinido.
- **Documente Blocos Complexos:** Adicione comentários explicativos para blocos de código complexos ou não triviais.
