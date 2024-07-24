
# Função `main` na Linguagem C

## Visão Geral
A função `main` é o ponto de entrada de um programa em C. É a função onde a execução do programa começa. Todos os programas em C devem ter exatamente uma função `main`.

## Definição da Função `main`

### Protótipos Aceitáveis
- Existem duas formas padrão para definir a função `main`:
  ```c
  int main(void);  // Forma sem argumentos
  int main(int argc, char *argv[]);  // Forma com argumentos
  ```

### Parâmetros
- `argc` (argument count): Conta o número de argumentos passados na linha de comando, incluindo o nome do programa.
- `argv` (argument vector): Um array de strings contendo os argumentos passados na linha de comando.

## Retorno da Função `main`

### Valor de Retorno
- A função `main` deve retornar um valor inteiro.
- `return 0;` indica que o programa terminou com sucesso.
- Outros valores indicam diferentes códigos de erro.
- Exemplo:
  ```c
  int main(void) {
      // Código
      return 0;  // Terminação bem-sucedida
  }
  ```

## Exemplos

### Sem Argumentos
```c
int main(void) {
    printf("Hello, World!
");
    return 0;
}
```

### Com Argumentos
```c
int main(int argc, char *argv[]) {
    for (int i = 0; i < argc; i++) {
        printf("Argumento %d: %s
", i, argv[i]);
    }
    return 0;
}
```

## Convenções e Comportamento

### Função `exit`
- A função `exit` pode ser usada para terminar o programa, fornecendo um código de retorno.
- Exemplo:
  ```c
  int main(void) {
      // Código
      exit(0);
  }
  ```

### Ambiente `envp`
- Algumas implementações permitem um terceiro parâmetro `envp` que fornece acesso às variáveis de ambiente.
- Exemplo:
  ```c
  int main(int argc, char *argv[], char *envp[]) {
      // Código
      return 0;
  }
  ```

## Dicas de Boas Práticas
- **Utilize Argumentos Adequadamente:** Use `argc` e `argv` para capturar e processar argumentos de linha de comando.
- **Retorne Valores Significativos:** Retorne valores que representem o estado de terminação do programa de forma clara.
- **Documente Argumentos:** Explique os argumentos esperados na linha de comando através de documentação ou mensagens de ajuda no programa.
