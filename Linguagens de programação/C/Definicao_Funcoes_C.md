
# Definição de Funções na Linguagem C

## Visão Geral
A definição de funções na linguagem C inclui a implementação do código que a função executa. Ela especifica o tipo de retorno, o nome da função, os parâmetros e o bloco de código que realiza a tarefa designada pela função.

## Definição de Função

### Sintaxe Básica
- A definição de função consiste em um cabeçalho que declara o tipo de retorno, o nome da função e seus parâmetros, seguido por um bloco de código entre chaves `{}`.
- Exemplo:
  ```c
  int add(int a, int b) {
      return a + b;
  }
  ```

### Parâmetros da Função
- Os parâmetros da função são declarados no cabeçalho da função e usados dentro do corpo da função.
- Exemplo:
  ```c
  void print_message(const char *message) {
      printf("%s\n", message);
  }
  ```

### Tipo de Retorno
- O tipo de retorno é declarado no início do cabeçalho da função e determina o tipo de valor que a função retorna ao chamador.
- Exemplo:
  ```c
  double multiply(double x, double y) {
      return x * y;
  }
  ```

## Funções `inline`

### Funções `inline`
- A palavra-chave `inline` sugere ao compilador que expanda a função no local da chamada para otimizar o desempenho.
- Exemplo:
  ```c
  inline int square(int x) {
      return x * x;
  }
  ```

## Funções Recursivas

### Funções Recursivas
- Funções que chamam a si mesmas para resolver problemas dividindo-os em subproblemas menores.
- Exemplo:
  ```c
  int factorial(int n) {
      if (n == 0) return 1;
      else return n * factorial(n - 1);
  }
  ```

## Funções Variádicas

### Funções Variádicas
- Funções que aceitam um número variável de argumentos usando a biblioteca `<stdarg.h>`.
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

## Especificadores de Classe de Armazenamento

### `extern`
- Indica que a função é definida em outro arquivo.
- Exemplo:
  ```c
  extern void update_data(void);
  ```

### `static`
- Indica que a função tem ligação interna, visível apenas dentro do arquivo onde é definida.
- Exemplo:
  ```c
  static void helper_function(void) {
      // implementação
  }
  ```

### `_Thread_local`
- Indica que uma variável é local a uma thread.
- Exemplo:
  ```c
  _Thread_local int thread_id;
  ```

## Funções de Ordem Superior

### Funções que Aceitam Funções como Parâmetros
- Funções podem receber ponteiros para outras funções como parâmetros.
- Exemplo:
  ```c
  void execute(void (*func)(void)) {
      func();
  }
  ```

### Funções que Retornam Funções
- Funções podem retornar ponteiros para outras funções.
- Exemplo:
  ```c
  int (*get_operation(char op))(int, int) {
      if (op == '+') return add;
      if (op == '-') return subtract;
      return NULL;
  }
  ```

## Exemplos Práticos

### Definição de Função Simples
```c
int add(int a, int b) {
    return a + b;
}
```

### Função `inline`
```c
inline int max(int a, int b) {
    return (a > b) ? a : b;
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

### Função com Ligação Interna
```c
static void internal_function(void) {
    // implementação
}
```

## Dicas de Boas Práticas
- **Defina Funções Claras e Concisas:** Mantenha as funções curtas e focadas em uma única tarefa.
- **Documente o Código:** Adicione comentários explicativos sobre a finalidade e o uso das funções.
- **Modularize o Código:** Divida o código em funções menores e reutilizáveis para melhorar a legibilidade e manutenção.
- **Use `inline` com Moderação:** Utilize `inline` apenas quando houver um benefício claro de desempenho, pois pode aumentar o tamanho do código.
- **Verifique a Ligação:** Use `static` para funções internas que não precisam ser visíveis fora do arquivo e `extern` para funções que serão usadas em outros arquivos.
