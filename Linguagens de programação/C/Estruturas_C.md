
# Estruturas (Structs) na Linguagem C

## Visão Geral
Estruturas (structs) na linguagem C são tipos de dados compostos que permitem agrupar variáveis de diferentes tipos sob um único nome. Elas são usadas para representar registros ou objetos mais complexos, facilitando a manipulação de dados relacionados.

## Declaração de Estruturas

### Declaração Básica
- Uma estrutura é declarada usando a palavra-chave `struct`, seguida por um nome opcional e uma lista de membros entre chaves.
- Exemplo:
  ```c
  struct Point {
      int x;
      int y;
  };
  ```

### Definição e Instanciação
- Após declarar uma estrutura, você pode criar variáveis (instâncias) desse tipo.
- Exemplo:
  ```c
  struct Point p1;  // Declaração de uma variável do tipo 'struct Point'
  ```

### Acesso aos Membros
- Os membros de uma estrutura são acessados usando o operador de ponto (`.`).
- Exemplo:
  ```c
  p1.x = 10;
  p1.y = 20;
  ```

### Declaração com Typedef
- Usando `typedef`, você pode criar um alias para a estrutura, simplificando sua utilização.
- Exemplo:
  ```c
  typedef struct {
      int x;
      int y;
  } Point;

  Point p2;
  ```

## Inicialização de Estruturas

### Inicialização na Declaração
- Estruturas podem ser inicializadas no momento da declaração.
- Exemplo:
  ```c
  struct Point p3 = {30, 40};
  ```

### Inicialização com Designadores
- É possível inicializar membros específicos de uma estrutura usando designadores.
- Exemplo:
  ```c
  struct Point p4 = {.y = 50, .x = 60};
  ```

## Estruturas Aninhadas

### Declaração de Estruturas Aninhadas
- Estruturas podem conter outras estruturas como membros.
- Exemplo:
  ```c
  struct Rectangle {
      struct Point top_left;
      struct Point bottom_right;
  };

  struct Rectangle rect = {{0, 0}, {100, 100}};
  ```

## Passagem de Estruturas para Funções

### Por Valor
- Estruturas podem ser passadas por valor para funções, o que cria uma cópia da estrutura.
- Exemplo:
  ```c
  void print_point(struct Point p) {
      printf("(%d, %d)
", p.x, p.y);
  }

  struct Point p5 = {70, 80};
  print_point(p5);
  ```

### Por Referência
- Estruturas podem ser passadas por referência usando ponteiros, evitando a cópia da estrutura.
- Exemplo:
  ```c
  void move_point(struct Point *p, int dx, int dy) {
      p->x += dx;
      p->y += dy;
  }

  move_point(&p5, 10, 10);
  ```

## Operações com Estruturas

### Atribuição
- Estruturas podem ser atribuídas a outras estruturas do mesmo tipo.
- Exemplo:
  ```c
  struct Point p6 = p5;
  ```

### Comparação
- Estruturas não podem ser comparadas diretamente usando operadores de comparação; a comparação deve ser feita membro a membro.
- Exemplo:
  ```c
  if (p6.x == p5.x && p6.y == p5.y) {
      // As estruturas são iguais
  }
  ```

## Exemplos Práticos

### Declaração e Inicialização
```c
struct Point {
    int x;
    int y;
};

struct Point p1 = {10, 20};
```

### Acesso aos Membros
```c
printf("x: %d, y: %d
", p1.x, p1.y);
```

### Estruturas Aninhadas
```c
struct Rectangle {
    struct Point top_left;
    struct Point bottom_right;
};

struct Rectangle rect = {{0, 0}, {50, 50}};
```

### Passagem para Funções
```c
void print_point(struct Point p) {
    printf("(%d, %d)
", p.x, p.y);
}

print_point(p1);
```

## Dicas de Boas Práticas
- **Use `typedef` para Simplificar:** Utilize `typedef` para criar aliases para estruturas, tornando o código mais legível.
- **Prefira Passagem por Referência:** Para evitar a sobrecarga de cópia, passe estruturas grandes por referência.
- **Inicialize Estruturas:** Sempre inicialize estruturas para garantir que todos os membros tenham valores definidos.
- **Documente Estruturas Complexas:** Adicione comentários para explicar a finalidade de cada membro em estruturas complexas.
