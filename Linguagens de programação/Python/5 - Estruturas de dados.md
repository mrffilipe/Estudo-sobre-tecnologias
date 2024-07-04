
# Estruturas de Dados

## Introdução

Python oferece várias estruturas de dados integradas, permitindo armazenar e gerenciar coleções de dados de maneira eficiente. Entre essas estruturas estão listas, conjuntos, dicionários e tuplas. Cada uma delas possui características e usos específicos que as tornam adequadas para diferentes tipos de tarefas.

## Principais Informações

1. **Listas**
   - As listas são coleções ordenadas e mutáveis de itens.
   - Podem conter elementos de diferentes tipos e suportam várias operações, como indexação, fatiamento, adição, remoção e iteração.

    ```python
    lista = [1, 2, 3, 4, 5]
    lista.append(6)
    lista.remove(3)
    ```

2. **List Comprehensions**
   - List comprehensions são uma maneira concisa de criar listas.
   - Permitem criar listas a partir de iteráveis, aplicando uma expressão opcionalmente filtrada por uma condição.

    ```python
    quadrados = [x**2 for x in range(10)]
    pares = [x for x in range(10) if x % 2 == 0]
    ```

3. **Tuplas**
   - Tuplas são semelhantes às listas, mas são imutáveis.
   - Úteis para armazenar coleções de dados heterogêneos e como chaves em dicionários.

    ```python
    tupla = (1, 2, 3)
    ```

4. **Conjuntos**
   - Conjuntos são coleções não ordenadas de itens únicos.
   - Suportam operações matemáticas como união, interseção e diferença.

    ```python
    conjunto = {1, 2, 3, 4, 5}
    conjunto.add(6)
    conjunto.remove(2)
    ```

5. **Dicionários**
   - Dicionários são coleções de pares chave-valor.
   - Permitem o acesso, adição e remoção de itens usando chaves únicas.

    ```python
    dicionario = {"nome": "Alice", "idade": 25}
    dicionario["cidade"] = "Goiânia"
    ```

6. **Iterando Sobre Estruturas de Dados**
   - Você pode iterar sobre os elementos de listas, tuplas, conjuntos e dicionários usando loops `for`.
   - Em dicionários, pode-se iterar sobre chaves, valores ou ambos.

    ```python
    for chave, valor in dicionario.items():
        print(chave, valor)
    ```

7. **Funções `zip` e `enumerate`**
   - A função `zip` combina elementos de múltiplos iteráveis.
   - A função `enumerate` retorna pares índice-valor ao iterar sobre uma sequência.

    ```python
    for i, valor in enumerate(lista):
        print(i, valor)

    lista1 = [1, 2, 3]
    lista2 = ['a', 'b', 'c']
    for num, letra in zip(lista1, lista2):
        print(num, letra)
    ```

## Observações Importantes

- **Mutabilidade**: Entenda quais estruturas de dados são mutáveis (listas, conjuntos, dicionários) e quais são imutáveis (tuplas). Use-as adequadamente conforme a necessidade.
- **Desempenho**: Cada estrutura de dados tem características de desempenho diferentes para operações de acesso, adição e remoção. Escolha a estrutura adequada para otimizar a performance.

## Dicas de Boas Práticas

- **Escolha a Estrutura Adequada**: Utilize a estrutura de dados que melhor se adapta ao seu problema. Por exemplo, use listas para coleções ordenadas, dicionários para associações chave-valor e conjuntos para coleções de itens únicos.
- **List Comprehensions**: Use list comprehensions para criar listas de forma concisa e legível.
- **Documente Seu Código**: Adicione comentários e docstrings para explicar a lógica e o uso das estruturas de dados em seu código.
