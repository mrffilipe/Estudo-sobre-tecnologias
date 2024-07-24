
# Conformidade na Linguagem C

## Visão Geral
A conformidade na linguagem C refere-se à aderência a padrões estabelecidos pela ISO (International Organization for Standardization) e ANSI (American National Standards Institute). Esses padrões definem como a linguagem deve se comportar e quais funcionalidades devem ser suportadas para garantir a portabilidade e interoperabilidade do código C em diferentes ambientes e compiladores.

## Padrões da Linguagem C

### ANSI C (C89/C90)
- Publicado pelo ANSI em 1989 e adotado pela ISO em 1990 como ISO/IEC 9899:1990. Este é o primeiro padrão oficial da linguagem C.
- Características: Funções padrão da biblioteca, regras de sintaxe e semântica, tipos de dados primitivos.

### C95
- Uma pequena atualização do padrão C90 publicada em 1995, adicionando funcionalidades como a biblioteca `wchar.h`.

### C99
- Publicado em 1999 como ISO/IEC 9899:1999. Introduziu várias melhorias e novos recursos, incluindo:
  - Tipos inteiros de largura fixa.
  - Variáveis podem ser declaradas em qualquer lugar.
  - Novas funções da biblioteca padrão.
  - Suporte para matemática complexa.
  - Palavras-chave `inline`, `_Bool`, `_Complex`.

### C11
- Publicado em 2011 como ISO/IEC 9899:2011. Introduziu novos recursos, como:
  - Suporte a múltiplas threads (`_Thread_local`, `_Atomic`).
  - Melhor compatibilidade com C++.
  - Novas funções de biblioteca.
  - Melhorias na segurança de tipos e controle de acesso à memória.

### C18
- Publicado em 2018 como ISO/IEC 9899:2018. Principalmente uma revisão menor de C11, com correções de erros e clarificações.

## Compiladores e Conformidade

### Conformidade Estrita
- Compiladores que seguem estritamente os padrões garantem que o código compilado seja portável e compatível com outras implementações padrão.
- Exemplo: GCC, Clang.

### Extensões do Compilador
- Muitos compiladores fornecem extensões além do padrão C, oferecendo funcionalidades adicionais que podem não ser portáveis.
- Exemplo: Extensões GNU C em GCC.

### Modos de Conformidade
- Compiladores geralmente oferecem modos para verificar a conformidade com diferentes padrões.
- Exemplo: GCC oferece `-std=c99`, `-std=c11`, `-ansi` para especificar o padrão a ser seguido.

## Uso de Padrões

### Especificação de Padrões
- Para garantir a conformidade com um padrão específico, pode-se utilizar flags do compilador.
- Exemplo:
  ```sh
  gcc -std=c11 -pedantic -Wall -Wextra -o programa programa.c
  ```

### Bibliotecas Padrão
- Utilização de bibliotecas padrão de acordo com o padrão especificado para garantir compatibilidade.
- Exemplo:
  ```c
  #include <stdio.h>
  #include <stdlib.h>
  ```

## Exemplos Práticos

### Código Conforme ao C99
```c
#include <stdio.h>
#include <stdint.h>

int main() {
    int32_t a = 10;
    int32_t b = 20;
    int32_t sum = a + b;
    printf("Sum: %d\n", sum);
    return 0;
}
```

### Uso de `_Thread_local` em C11
```c
#include <stdio.h>
#include <threads.h>

_Thread_local int count = 0;

int thread_func(void *arg) {
    count++;
    printf("Thread %d, Count: %d\n", *(int *)arg, count);
    return 0;
}

int main() {
    thrd_t t1, t2;
    int id1 = 1, id2 = 2;
    thrd_create(&t1, thread_func, &id1);
    thrd_create(&t2, thread_func, &id2);
    thrd_join(t1, NULL);
    thrd_join(t2, NULL);
    return 0;
}
```

## Dicas de Boas Práticas
- **Especifique o Padrão:** Sempre especifique o padrão que seu código deve seguir para garantir conformidade e portabilidade.
- **Evite Extensões Proprietárias:** Use apenas extensões do compilador quando absolutamente necessário e documente seu uso.
- **Teste em Múltiplos Compiladores:** Compile e teste seu código em diferentes compiladores para garantir portabilidade.
- **Atualize seu Conhecimento:** Mantenha-se atualizado com as revisões e atualizações dos padrões da linguagem C.
