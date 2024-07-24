
# `_Noreturn` na Linguagem C

## Visão Geral
A especificação `_Noreturn` na linguagem C é usada para indicar que uma função não retornará ao chamador. Isso é útil para funções que terminam a execução do programa, como funções de saída de erro ou abortos.

## Declaração de Funções `_Noreturn`

### Sintaxe Básica
- `_Noreturn` é colocado antes da declaração da função.
- Exemplo:
  ```c
  #include <stdlib.h>
  
  _Noreturn void terminate_program(const char *message) {
      printf("Error: %s\n", message);
      exit(1);
  }
  ```

### Uso com `void`
- A especificação `_Noreturn` é usada frequentemente com funções que têm `void` como tipo de retorno, pois elas não retornam um valor.
- Exemplo:
  ```c
  _Noreturn void abort_execution(void);
  ```

### Combinação com Outras Especificações
- `_Noreturn` pode ser combinado com outras especificações, como `static` ou `extern`.
- Exemplo:
  ```c
  static _Noreturn void fatal_error(const char *message);
  ```

## Comportamento e Uso

### Indicação de Terminação
- Ao usar `_Noreturn`, o compilador entende que a função não retornará ao ponto de chamada, o que pode ajudar em otimizações e evitar avisos de código não alcançável.
- Exemplo:
  ```c
  _Noreturn void handle_critical_error(void) {
      // Código de tratamento de erro crítico
      exit(EXIT_FAILURE);
  }
  ```

### Funções Comuns com `_Noreturn`
- Funções de saída de erro (`exit`, `abort`) e funções que lançam exceções ou encerram o programa são comuns candidatas ao uso de `_Noreturn`.
- Exemplo:
  ```c
  _Noreturn void exit_with_message(const char *message) {
      printf("Exiting: %s\n", message);
      exit(1);
  }
  ```

### Compatibilidade
- `_Noreturn` é uma especificação introduzida no C11 e pode não ser suportada em compiladores mais antigos. Em compiladores que suportam GNU C, `__attribute__((noreturn))` pode ser usado como alternativa.
- Exemplo:
  ```c
  #ifdef __GNUC__
  #define NORETURN __attribute__((noreturn))
  #else
  #define NORETURN _Noreturn
  #endif

  NORETURN void shutdown_system(void);
  ```

## Exemplos Práticos

### Função que Não Retorna
```c
_Noreturn void fatal_error(const char *msg) {
    fprintf(stderr, "Fatal error: %s\n", msg);
    exit(EXIT_FAILURE);
}
```

### Uso com `static`
```c
static _Noreturn void terminate(void) {
    abort();
}
```

### Combinação com `extern`
```c
extern _Noreturn void panic(const char *msg);
```

### Definindo Macros para Compatibilidade
```c
#ifdef __GNUC__
#define NORETURN __attribute__((noreturn))
#else
#define NORETURN _Noreturn
#endif

NORETURN void custom_exit(int status) {
    exit(status);
}
```

## Dicas de Boas Práticas
- **Use `_Noreturn` para Funções de Terminação:** Aplique `_Noreturn` em funções que encerram o programa ou não retornam ao chamador para melhorar a clareza do código.
- **Documente o Comportamento:** Adicione comentários explicando por que a função não retorna, ajudando na manutenção do código.
- **Verifique a Compatibilidade:** Considere a compatibilidade com compiladores mais antigos e use macros para fornecer alternativas, se necessário.
- **Evite Uso Indevido:** Não use `_Noreturn` em funções que possam retornar, pois isso pode causar comportamento indefinido.
