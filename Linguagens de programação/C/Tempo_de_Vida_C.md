
# Tempo de Vida na Linguagem C

## Visão Geral
O tempo de vida de uma variável em C refere-se ao período durante o qual a variável existe na memória. O tempo de vida de uma variável está diretamente relacionado ao seu escopo e à forma como ela é declarada.

## Tipos de Tempo de Vida

### Tempo de Vida Automático
- Variáveis declaradas dentro de funções (incluindo parâmetros) têm tempo de vida automático.
- Elas são criadas quando o bloco de código onde estão declaradas é executado e destruídas quando o bloco termina.
- Exemplo:
  ```c
  void func() {
      int a = 5; // 'a' tem tempo de vida automático
  }
  ```

### Tempo de Vida Estático
- Variáveis declaradas com a palavra-chave `static` têm tempo de vida estático.
- Elas são inicializadas apenas uma vez e existem até o término do programa.
- Pode ser usado tanto para variáveis locais quanto globais.
- Exemplo:
  ```c
  static int b = 10; // 'b' tem tempo de vida estático
  
  void func() {
      static int c = 15; // 'c' tem tempo de vida estático dentro da função
  }
  ```

### Tempo de Vida de Ligação Externa
- Variáveis globais e funções têm tempo de vida de ligação externa.
- Elas são visíveis em todo o programa, desde que sejam declaradas em um arquivo de cabeçalho incluído onde necessário.
- Exemplo:
  ```c
  int d = 20; // 'd' tem tempo de vida de ligação externa
  ```

### Tempo de Vida Dinâmico
- Memória alocada dinamicamente usando funções como `malloc`, `calloc`, `realloc` e `free` da biblioteca padrão tem tempo de vida dinâmico.
- Essa memória existe até ser explicitamente liberada com `free`.
- Exemplo:
  ```c
  int *ptr = (int *)malloc(sizeof(int) * 10); // 'ptr' aponta para memória com tempo de vida dinâmico
  free(ptr); // Libera a memória alocada dinamicamente
  ```

## Exemplos
```c
void example() {
    int autoVar = 1; // Tempo de vida automático
    static int staticVar = 2; // Tempo de vida estático
    int *dynamicVar = (int *)malloc(sizeof(int)); // Tempo de vida dinâmico

    // Usando a variável dinâmica
    *dynamicVar = 3;

    // Liberando a memória dinâmica
    free(dynamicVar);
}

int globalVar = 4; // Tempo de vida de ligação externa
```

## Dicas de Boas Práticas
- **Libere Memória Dinamicamente Alocada:** Sempre use `free` para liberar memória alocada dinamicamente para evitar vazamentos de memória.
- **Use `static` com Moderação:** Declare variáveis `static` apenas quando necessário, para evitar uso excessivo de memória.
- **Inicialize Variáveis:** Inicialize todas as variáveis, especialmente aquelas com tempo de vida automático, para evitar comportamento indefinido.
- **Comente o Tempo de Vida:** Utilize comentários para explicar o tempo de vida de variáveis complexas ou críticas.
