
# Duração de Armazenamento na Linguagem C

## Visão Geral
A duração de armazenamento na linguagem C refere-se ao tempo de vida de uma variável, que determina quando a memória para essa variável é alocada e desalocada. Existem quatro tipos de duração de armazenamento: automática, estática, thread e dinâmica.

## Tipos de Duração de Armazenamento

### Duração de Armazenamento Automática
- Variáveis locais dentro de funções têm duração de armazenamento automática.
- A memória é alocada quando a função é chamada e desalocada quando a função retorna.
- Exemplo:
  ```c
  void func() {
      int a = 10;  // 'a' tem duração de armazenamento automática
  }
  ```

### Duração de Armazenamento Estática
- Variáveis globais, variáveis estáticas locais e variáveis estáticas em funções têm duração de armazenamento estática.
- A memória é alocada quando o programa começa e desalocada quando o programa termina.
- Exemplo:
  ```c
  static int b = 20;  // 'b' tem duração de armazenamento estática

  void func() {
      static int c = 30;  // 'c' tem duração de armazenamento estática
  }
  ```

### Duração de Armazenamento Thread
- Variáveis locais do tipo thread têm duração de armazenamento que coincide com a duração da thread.
- A memória é alocada quando a thread é criada e desalocada quando a thread termina.
- Exemplo:
  ```c
  _Thread_local int d = 40;  // 'd' tem duração de armazenamento thread
  ```

### Duração de Armazenamento Dinâmica
- Variáveis alocadas dinamicamente usando `malloc`, `calloc` ou `realloc` têm duração de armazenamento dinâmica.
- A memória é alocada explicitamente e deve ser liberada explicitamente usando `free`.
- Exemplo:
  ```c
  int *ptr = (int *)malloc(sizeof(int) * 10);  // 'ptr' tem duração de armazenamento dinâmica
  free(ptr);  // Libera a memória alocada dinamicamente
  ```

## Escopo e Ligação

### Escopo de Bloco
- Variáveis declaradas dentro de um bloco têm escopo de bloco e só podem ser acessadas dentro desse bloco.
- Exemplo:
  ```c
  void func() {
      int e = 50;  // 'e' tem escopo de bloco
  }
  ```

### Escopo de Arquivo
- Variáveis globais têm escopo de arquivo e podem ser acessadas de qualquer função no mesmo arquivo.
- Exemplo:
  ```c
  int f = 60;  // 'f' tem escopo de arquivo
  ```

### Escopo de Função
- Variáveis declaradas dentro de uma função, mas fora de qualquer bloco, têm escopo de função.
- Exemplo:
  ```c
  void func() {
      int g;  // 'g' tem escopo de função
      {
          g = 70;
      }
  }
  ```

### Ligação Externa
- Variáveis globais e funções podem ser acessadas em outros arquivos usando a palavra-chave `extern`.
- Exemplo:
  ```c
  extern int h;  // 'h' tem ligação externa
  ```

### Ligação Interna
- Variáveis e funções declaradas como `static` têm ligação interna e só podem ser acessadas dentro do arquivo onde são declaradas.
- Exemplo:
  ```c
  static int i = 80;  // 'i' tem ligação interna
  ```

## Dicas de Boas Práticas
- **Use `static` para Persistência Local:** Utilize variáveis estáticas locais para manter o estado entre chamadas de função.
- **Gerencie Memória Dinâmica com Cuidado:** Sempre libere a memória alocada dinamicamente para evitar vazamentos de memória.
- **Prefira Escopo Restrito:** Declare variáveis no menor escopo possível para melhorar a legibilidade e manutenção do código.
- **Documente Durações de Armazenamento Especiais:** Adicione comentários explicativos para variáveis com durações de armazenamento não triviais.
