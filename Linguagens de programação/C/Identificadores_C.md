
# Identificadores na Linguagem C

## Visão Geral
Identificadores são nomes utilizados para identificar variáveis, funções, tipos, rótulos e outros objetos e entidades em um programa C. Eles são fundamentais para a escrita de código claro e organizado.

## Regras para Identificadores

### Composição
- Um identificador deve começar com uma letra (a-z, A-Z) ou um sublinhado (_).
- Os caracteres subsequentes podem ser letras, dígitos (0-9), ou sublinhados.

### Sensibilidade a Maiúsculas e Minúsculas
- A linguagem C é sensível a maiúsculas e minúsculas, ou seja, `var`, `Var`, e `VAR` são considerados identificadores distintos.

### Comprimento
- Embora o padrão da linguagem C não imponha um limite específico ao comprimento dos identificadores, algumas implementações podem ter restrições.

### Palavras Reservadas
- Identificadores não podem ser iguais a palavras reservadas da linguagem C (como `int`, `return`, `if`, etc.).

## Regras de Escopo e Ligação

### Escopo de Bloco
- Identificadores declarados dentro de um bloco `{}` têm escopo local ao bloco.

### Escopo de Função
- Identificadores declarados dentro de uma função têm escopo local à função.

### Escopo de Arquivo
- Identificadores declarados fora de todas as funções e blocos têm escopo global ao arquivo.

### Escopo de Parâmetro de Função
- Identificadores usados como parâmetros em uma função têm escopo local ao corpo da função.

### Ligação
- **Ligação Interna:** O identificador é visível apenas dentro do arquivo de origem.
- **Ligação Externa:** O identificador é visível a partir de outros arquivos de origem.

## Exemplos
```c
int global_var;  // Identificador com escopo global

void func(int param) {  // Identificador de parâmetro de função
    int local_var;  // Identificador com escopo local à função
    {
        int block_var;  // Identificador com escopo de bloco
    }
}
```

## Dicas de Boas Práticas
- **Nomes Descritivos:** Use identificadores que descrevam claramente a finalidade da variável ou função.
- **Padrão de Nomenclatura Consistente:** Adote um padrão de nomenclatura consistente (como camelCase ou snake_case).
- **Evite Nomes Curtos Demais:** Identificadores como `a`, `b`, `c` devem ser evitados, exceto em contextos muito limitados.
- **Documentação:** Utilize comentários para explicar o propósito de identificadores importantes ou complexos.
