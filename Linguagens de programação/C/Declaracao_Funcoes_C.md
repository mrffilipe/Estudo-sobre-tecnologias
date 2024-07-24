
# Declaração de Funções na Linguagem C

## Visão Geral
Declaração de funções na linguagem C é uma maneira de informar ao compilador sobre a assinatura de uma função (nome, tipo de retorno e parâmetros) antes de sua definição real no código. Isso permite que funções sejam chamadas antes de serem definidas, facilitando a organização e modularização do código.

## Declaração de Função

### Sintaxe Básica
- A declaração de função inclui o tipo de retorno, o nome da função e uma lista de parâmetros entre parênteses.
- Exemplo:
  ```c
  int add(int, int);
  ```

### Declaração com Nomes de Parâmetros
- A declaração pode opcionalmente incluir os nomes dos parâmetros.
- Exemplo:
  ```c
  int add(int a, int b);
  ```

### Declaração com Parâmetros Opcionais
- Para funções variádicas, a declaração usa reticências (`...`) para indicar parâmetros opcionais.
- Exemplo:
  ```c
  void log_message(const char *format, ...);
  ```

## Funções `inline`

### Declaração `inline`
- A palavra-chave `inline` sugere ao compilador que expanda a função no local da chamada para otimizar o desempenho.
- Exemplo:
  ```c
  inline int square(int x) {
      return x * x;
  }
  ```

### Declaração e Definição em Headers
- Funções `inline` são frequentemente definidas em arquivos de cabeçalho para que possam ser expandidas em qualquer lugar onde são usadas.
- Exemplo:
  ```c
  // math_utils.h
  inline int max(int a, int b) {
      return (a > b) ? a : b;
  }
  ```

## Especificadores de Classe de Armazenamento

### `extern`
- Declara uma função definida em outro arquivo.
- Exemplo:
  ```c
  extern void update_data(void);
  ```

### `static`
- Declara uma função com ligação interna, visível apenas dentro do arquivo onde é definida.
- Exemplo:
  ```c
  static void helper_function(void);
  ```

### `_Thread_local`
- Declara uma variável local a uma thread.
- Exemplo:
  ```c
  _Thread_local int thread_id;
  ```

## Funções com Parâmetros Padrão

### Parâmetros com Valores Padrão
- Em C, não há suporte direto para parâmetros com valores padrão como em C++. No entanto, isso pode ser simulado usando funções sobrecarregadas ou argumentos variádicos.
- Exemplo:
  ```c
  void set_value(int x) {
      // implementação
  }

  void set_value_default() {
      set_value(10);  // Chama a função com um valor padrão
  }
  ```

## Protótipos de Funções

### Importância dos Protótipos
- Protótipos são importantes para permitir que o compilador verifique os tipos de argumentos e o tipo de retorno das funções antes de sua definição.
- Exemplo:
  ```c
  double compute_area(double radius);

  int main() {
      double area = compute_area(5.0);
      // código
      return 0;
  }

  double compute_area(double radius) {
      return 3.14 * radius * radius;
  }
  ```

## Funções Recursivas

### Declaração e Definição de Funções Recursivas
- Funções recursivas chamam a si mesmas para resolver um problema dividindo-o em subproblemas menores.
- Exemplo:
  ```c
  int factorial(int n);

  int factorial(int n) {
      if (n <= 1) return 1;
      else return n * factorial(n - 1);
  }
  ```

## Exemplos Práticos

### Declaração Simples
```c
int multiply(int, int);
```

### Função `inline`
```c
inline int add(int a, int b) {
    return a + b;
}
```

### Uso de `extern`
```c
// header.h
extern void print_message(const char *);

// file1.c
#include "header.h"
void print_message(const char *msg) {
    printf("%s\n", msg);
}

// file2.c
#include "header.h"
int main() {
    print_message("Hello, World!");
    return 0;
}
```

### Função Recursiva
```c
int fibonacci(int n);

int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

## Dicas de Boas Práticas
- **Declare Antes de Usar:** Sempre declare funções antes de usá-las para evitar erros de compilação.
- **Use Protótipos em Headers:** Coloque declarações de função em arquivos de cabeçalho para facilitar a reutilização e manutenção.
- **Documente Funções:** Adicione comentários explicativos sobre a finalidade e o uso das funções.
- **Prefira `inline` com Moderação:** Use `inline` apenas quando houver um benefício claro de desempenho, pois pode aumentar o tamanho do código.
