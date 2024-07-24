
# Funções na Linguagem C

## Visão Geral
Funções na linguagem C são blocos de código reutilizáveis que realizam tarefas específicas. Elas ajudam a organizar o código, melhorar a legibilidade e facilitar a manutenção.

## Declaração e Definição de Funções

### Declaração de Função
- Uma declaração de função informa ao compilador sobre o nome da função, seu tipo de retorno e os parâmetros que ela aceita.
- Exemplo:
  ```c
  int add(int, int);
  ```

### Definição de Função
- A definição de função inclui a implementação do código que a função executa.
- Exemplo:
  ```c
  int add(int a, int b) {
      return a + b;
  }
  ```

### Função `main`
- A função `main` é o ponto de entrada de um programa C.
- Exemplo:
  ```c
  int main() {
      // código
      return 0;
  }
  ```

## Tipos de Funções

### Funções sem Retorno (`void`)
- Funções que não retornam um valor utilizam o tipo `void`.
- Exemplo:
  ```c
  void print_message() {
      printf("Hello, World!\n");
  }
  ```

### Funções com Retorno
- Funções que retornam um valor especificam o tipo de retorno na declaração.
- Exemplo:
  ```c
  int multiply(int a, int b) {
      return a * b;
  }
  ```

### Funções Recursivas
- Funções que chamam a si mesmas são chamadas de recursivas.
- Exemplo:
  ```c
  int factorial(int n) {
      if (n == 0) return 1;
      else return n * factorial(n - 1);
  }
  ```

## Parâmetros de Funções

### Parâmetros por Valor
- Os parâmetros são passados por valor, criando uma cópia dos argumentos.
- Exemplo:
  ```c
  void increment(int a) {
      a++;
  }
  ```

### Parâmetros por Referência
- Parâmetros podem ser passados por referência usando ponteiros.
- Exemplo:
  ```c
  void increment(int *a) {
      (*a)++;
  }
  ```

### Funções Variádicas
- Funções que aceitam um número variável de argumentos usam a biblioteca `<stdarg.h>`.
- Exemplo:
  ```c
  #include <stdarg.h>
  void print_numbers(int count, ...) {
      va_list args;
      va_start(args, count);
      for (int i = 0; i < count; i++) {
          int num = va_arg(args, int);
          printf("%d ", num);
      }
      va_end(args);
  }
  ```

## Protótipos de Funções

### Declaração Antecipada
- Protótipos de função permitem declarar funções antes de suas definições, facilitando a organização do código.
- Exemplo:
  ```c
  void greet(void);
  
  int main() {
      greet();
      return 0;
  }
  
  void greet() {
      printf("Hello!\n");
  }
  ```

## Escopo e Ligação de Funções

### Escopo Global
- Funções declaradas fora de qualquer bloco têm escopo global.
- Exemplo:
  ```c
  void global_function() {
      // código
  }
  ```

### Ligação Interna
- Funções com a palavra-chave `static` têm ligação interna e são visíveis apenas dentro do arquivo em que são definidas.
- Exemplo:
  ```c
  static void internal_function() {
      // código
  }
  ```

### Ligação Externa
- Funções podem ser declaradas como `extern` para serem usadas em outros arquivos.
- Exemplo:
  ```c
  // arquivo1.c
  void external_function(void);
  
  // arquivo2.c
  extern void external_function(void);
  ```

## Exemplos Práticos

### Função Simples
```c
int add(int a, int b) {
    return a + b;
}
```

### Função com Ponteiros
```c
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

### Função Recursiva
```c
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

### Função Variádica
```c
#include <stdarg.h>
void log_message(const char *format, ...) {
    va_list args;
    va_start(args, format);
    vprintf(format, args);
    va_end(args);
}
```

## Dicas de Boas Práticas
- **Use Nomes Significativos:** Escolha nomes de funções que descrevam claramente sua finalidade.
- **Documente Funções:** Adicione comentários explicativos sobre o propósito e uso das funções.
- **Modularize o Código:** Divida o código em funções menores e reutilizáveis para melhorar a legibilidade e manutenção.
- **Evite Funções Longas:** Mantenha as funções curtas e focadas em uma única tarefa.
