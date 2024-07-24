
# `extern` na Linguagem C

## Visão Geral
A palavra-chave `extern` na linguagem C é usada para declarar uma variável ou função que é definida em outro arquivo ou escopo. Isso permite que diferentes arquivos de um programa compartilhem variáveis e funções, facilitando a modularização do código.

## Declaração de `extern`

### Declaração de Variáveis
- `extern` é usada para declarar variáveis globais que são definidas em outros arquivos.
- Exemplo:
  ```c
  extern int global_var;
  ```

### Definição de Variáveis
- A definição de uma variável extern ocorre em um único arquivo, sem a palavra-chave `extern`.
- Exemplo:
  ```c
  int global_var = 10;
  ```

### Funções Externas
- Funções também podem ser declaradas como `extern` para indicar que são definidas em outro arquivo.
- Exemplo:
  ```c
  extern void foo(void);
  ```

## Uso de `extern`

### Módulos Separados
- `extern` permite que um programa seja dividido em múltiplos arquivos, cada um contendo definições e declarações que podem ser compartilhadas.
- Exemplo:
  ```c
  // arquivo1.c
  #include <stdio.h>
  extern int shared_var;
  void print_shared_var() {
      printf("%d
", shared_var);
  }

  // arquivo2.c
  #include <stdio.h>
  int shared_var = 5;
  int main() {
      print_shared_var();
      return 0;
  }
  ```

### Declarações em Headers
- Declarações `extern` geralmente são colocadas em arquivos de cabeçalho (.h) para serem incluídas em múltiplos arquivos fonte.
- Exemplo:
  ```c
  // header.h
  extern int count;
  void increment_count(void);

  // source.c
  #include "header.h"
  int count = 0;
  void increment_count(void) {
      count++;
  }

  // main.c
  #include "header.h"
  int main() {
      increment_count();
      printf("%d
", count);
      return 0;
  }
  ```

## Vantagens do Uso de `extern`

### Modularidade
- `extern` facilita a separação de código em módulos, permitindo melhor organização e manutenção.
- Exemplo:
  ```c
  // module1.h
  extern int module_var;
  void module_func(void);

  // module1.c
  #include "module1.h"
  int module_var = 0;
  void module_func(void) {
      module_var++;
  }

  // main.c
  #include "module1.h"
  int main() {
      module_func();
      printf("%d
", module_var);
      return 0;
  }
  ```

### Compartilhamento de Dados
- `extern` permite o compartilhamento de variáveis e funções entre diferentes arquivos de um projeto.
- Exemplo:
  ```c
  // shared.h
  extern int shared_data;

  // file1.c
  #include "shared.h"
  int shared_data = 100;

  // file2.c
  #include "shared.h"
  void print_data(void) {
      printf("%d
", shared_data);
  }
  ```

### Redução de Duplicação
- Declarações `extern` em headers ajudam a evitar duplicação de código, centralizando as declarações.
- Exemplo:
  ```c
  // common.h
  extern int global_var;
  void common_func(void);

  // common.c
  #include "common.h"
  int global_var = 42;
  void common_func(void) {
      global_var++;
  }

  // main.c
  #include "common.h"
  int main() {
      common_func();
      printf("%d
", global_var);
      return 0;
  }
  ```

## Exemplos Práticos

### Declaração e Definição de Variável Externa
```c
// file1.c
extern int x;

// file2.c
int x = 10;
```

### Declaração e Definição de Função Externa
```c
// file1.c
extern void foo(void);

// file2.c
void foo(void) {
    printf("Hello from foo!
");
}
```

### Uso em Múltiplos Arquivos
```c
// header.h
extern int counter;
void increment(void);

// source1.c
#include "header.h"
int counter = 0;
void increment(void) {
    counter++;
}

// main.c
#include "header.h"
int main() {
    increment();
    printf("%d
", counter);
    return 0;
}
```

## Dicas de Boas Práticas
- **Declare em Headers:** Coloque declarações `extern` em arquivos de cabeçalho para fácil inclusão em múltiplos arquivos.
- **Defina em Apenas um Lugar:** Certifique-se de que a definição de variáveis `extern` ocorra em apenas um arquivo para evitar erros de linkagem.
- **Documente Bem:** Adicione comentários para explicar o uso de variáveis e funções `extern`, facilitando a manutenção do código.
