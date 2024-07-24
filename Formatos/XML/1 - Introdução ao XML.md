# 3.1 Introdução ao XML

## O que é XML

XML (eXtensible Markup Language) é uma linguagem de marcação que define um conjunto de regras para a codificação de documentos em um formato que pode ser lido tanto por humanos quanto por máquinas. XML é amplamente utilizado para representar dados estruturados e para troca de informações entre sistemas diferentes. Ao contrário do HTML, que é utilizado para exibir dados, XML é usado para transportar e armazenar dados.

## Estrutura de um documento XML

Um documento XML é composto por uma hierarquia de elementos, que podem conter outros elementos, atributos e texto. A estrutura básica de um documento XML inclui:
- **Declaração XML**: Uma linha opcional no início do documento que especifica a versão do XML e a codificação do documento.
  - Exemplo: `<?xml version="1.0" encoding="UTF-8"?>`
- **Elemento raiz**: O elemento principal que contém todos os outros elementos do documento.
  - Exemplo: `<livro></livro>`
- **Elementos**: Marcadores que podem conter texto, outros elementos e atributos. Cada elemento é delimitado por uma tag de abertura e uma tag de fechamento.
  - Exemplo: `<titulo>Introdução ao XML</titulo>`
- **Atributos**: Informações adicionais sobre elementos, especificadas dentro das tags de abertura.
  - Exemplo: `<livro id="1">`

## Sintaxe XML

A sintaxe XML segue um conjunto de regras rigorosas para garantir que os documentos sejam bem formados e válidos:
- **Elementos devem ser corretamente aninhados**: Cada elemento deve ser fechado na ordem inversa à sua abertura.
  - Correto: `<livro><titulo>XML</titulo></livro>`
  - Incorreto: `<livro><titulo>XML</livro></titulo>`
- **Tags de abertura e fechamento**: Todos os elementos devem ter uma tag de abertura e uma tag de fechamento correspondente.
  - Correto: `<autor>Marcos</autor>`
  - Incorreto: `<autor>Marcos`
- **Sensibilidade a maiúsculas e minúsculas**: Tags são sensíveis a maiúsculas e minúsculas, ou seja, `<Titulo>` e `<titulo>` são diferentes.
- **Atributos devem estar entre aspas**: Valores de atributos devem ser colocados entre aspas duplas ou simples.
  - Correto: `<livro id="1">`
  - Incorreto: `<livro id=1>`
- **Um único elemento raiz**: O documento XML deve ter um único elemento raiz que contém todos os outros elementos.

Exemplo de um documento XML completo:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<biblioteca>
    <livro id="1">
        <titulo>Introdução ao XML</titulo>
        <autor>Marcos</autor>
        <ano>2024</ano>
    </livro>
</biblioteca>