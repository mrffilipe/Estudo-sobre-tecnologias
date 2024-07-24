# 2.1 Introdução ao JSON

## O que é JSON

JSON (JavaScript Object Notation) é um formato leve de intercâmbio de dados, fácil para os humanos lerem e escreverem, e fácil para as máquinas parsearem e gerarem. JSON é um formato de texto completamente independente de linguagem, mas usa convenções que são familiares aos programadores de linguagens da família C, incluindo C, C++, C#, Java, JavaScript, Perl, Python, e muitas outras. Esses recursos fazem do JSON um formato de dados ideal.

## Estrutura de um documento JSON

Um documento JSON é composto de duas estruturas básicas:
- **Objeto**: Uma coleção de pares chave-valor. As chaves são strings e os valores podem ser de vários tipos (string, número, objeto, array, true, false, null).
  - Exemplo: `{"nome": "Marcos", "idade": 20, "cidade": "Goiânia"}`
- **Array**: Uma lista ordenada de valores. Os valores podem ser de qualquer tipo, incluindo outro array ou objeto.
  - Exemplo: `["Goiânia", "São Paulo", "Rio de Janeiro"]`

## Sintaxe JSON

A sintaxe JSON é baseada em um subconjunto da linguagem de programação JavaScript, especificamente, a sintaxe de objetos e arrays:
- **Objetos** são delimitados por chaves `{}` e contêm uma coleção de pares chave-valor.
  - Chaves são strings delimitadas por aspas duplas.
  - Valores podem ser strings, números, objetos, arrays, true, false ou null.
  - Exemplo: `{"nome": "Marcos", "idade": 20}`
- **Arrays** são delimitados por colchetes `[]` e contêm uma lista de valores.
  - Valores dentro de um array são separados por vírgulas.
  - Exemplo: `["Goiânia", "São Paulo", "Rio de Janeiro"]`
- **Strings** são delimitadas por aspas duplas e podem conter qualquer caractere Unicode.
  - Exemplo: `"Marcos"`
- **Números** são escritos da mesma maneira que em JavaScript, podendo incluir números inteiros ou de ponto flutuante.
  - Exemplo: `20` ou `3.14`
- **Booleanos** são os valores `true` e `false`.
- **null** é um valor especial que representa a ausência de valor.

Exemplo de um documento JSON completo:
```json
{
  "nome": "Marcos",
  "idade": 20,
  "cidade": "Goiânia",
  "hobbies": ["programar", "jogar", "ler"],
  "contato": {
    "email": "marcos@example.com",
    "telefone": "1234-5678"
  },
  "isStudent": true,
  "nota": null
}