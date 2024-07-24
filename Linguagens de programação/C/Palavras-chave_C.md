
# Palavras-chave na Linguagem C

## Visão Geral
Palavras-chave são identificadores reservados na linguagem C que têm significados especiais. Elas não podem ser usadas como nomes de variáveis, funções ou identificadores. A linguagem C possui um conjunto específico de palavras-chave que são usadas para definir a estrutura do código, controlar fluxo, declarar tipos e outras funcionalidades essenciais.

## Lista de Palavras-chave

### Controle de Fluxo
- `if`, `else`: Estruturas condicionais.
  ```c
  if (a > b) {
      // código
  } else {
      // código
  }
  ```

- `switch`, `case`, `default`: Estruturas de seleção múltipla.
  ```c
  switch (a) {
      case 1: 
          // código
          break;
      default: 
          // código
  }
  ```

- `while`, `do`, `for`: Estruturas de repetição.
  ```c
  while (condição) {
      // código
  }

  do {
      // código
  } while (condição);

  for (inicialização; condição; incremento) {
      // código
  }
  ```

- `break`, `continue`: Controle de laços.
  ```c
  while (condição) {
      if (condição) break;
      // código
      if (condição) continue;
  }
  ```

### Declaração de Tipos
- `int`, `char`, `float`, `double`: Tipos de dados básicos.
  ```c
  int a = 10;
  char b = 'c';
  float c = 3.14f;
  double d = 6.28;
  ```

- `struct`, `union`, `enum`: Tipos de dados compostos.
  ```c
  struct Point {
      int x;
      int y;
  };

  union Data {
      int i;
      float f;
  };

  enum Color {
      RED, GREEN, BLUE
  };
  ```

### Modificadores de Tipo
- `signed`, `unsigned`, `short`, `long`: Modificadores para tipos inteiros.
  ```c
  unsigned int e = 100;
  long int f = 1000L;
  ```

### Qualificadores de Tipo
- `const`, `volatile`, `restrict`: Qualificadores que modificam o comportamento de variáveis.
  ```c
  const int g = 50;
  volatile int h = 60;
  int * restrict ptr = &a;
  ```

### Outras Palavras-chave
- `void`: Indica ausência de tipo.
  ```c
  void func(void) {
      // código
  }
  ```

- `return`: Retorna um valor de uma função.
  ```c
  int func(void) {
      return 0;
  }
  ```

- `sizeof`: Operador que retorna o tamanho de um tipo.
  ```c
  int size = sizeof(int);
  ```

### Manipulação de Memória
- `malloc`, `free`: Funções para alocação e liberação de memória dinâmica.
  ```c
  int *ptr = (int *)malloc(sizeof(int) * 10);
  free(ptr);
  ```

### Controle de Acesso
- `static`, `extern`: Controle de visibilidade e duração de variáveis.
  ```c
  static int i = 10;
  extern int j;
  ```

## Dicas de Boas Práticas
- **Evite Conflitos de Nomes:** Não use palavras-chave como identificadores.
- **Use Qualificadores Adequadamente:** Aplique `const`, `volatile`, e `restrict` para melhorar a segurança e a eficiência do código.
- **Conheça as Palavras-chave:** Entenda o propósito de cada palavra-chave para escrever código C eficaz e correto.
