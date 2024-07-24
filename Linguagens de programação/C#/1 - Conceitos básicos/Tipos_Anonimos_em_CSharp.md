
# Tipos Anônimos em C#

Os tipos anônimos em C# permitem a criação de objetos que contêm um conjunto de propriedades de leitura, sem a necessidade de definir uma classe explicitamente. Eles são particularmente úteis para encapsular um conjunto de valores em um único objeto de maneira rápida e conveniente. Abaixo estão as principais informações e observações importantes sobre tipos anônimos conforme apresentadas na documentação:

## Características Principais
- **Leitura-Escrita**: Os tipos anônimos são somente leitura. As propriedades definidas no momento da criação do objeto não podem ser modificadas posteriormente.
- **Inferência de Tipos**: O compilador infere os tipos das propriedades dos tipos anônimos.
- **Uso Temporário**: Eles são geralmente usados em escopos limitados, como consultas LINQ, onde uma estrutura de dados temporária é necessária.

## Criação de Tipos Anônimos
- **Sintaxe Básica**: Um tipo anônimo é criado usando a palavra-chave `new` seguida por uma lista de inicializadores de propriedades entre chaves.
```csharp
var person = new { FirstName = "John", LastName = "Doe" };
```

- **Propriedades**: As propriedades dos tipos anônimos são implicitamente públicas e de somente leitura.
```csharp
Console.WriteLine(person.FirstName); // Output: John
```

## Usos Comuns
- **Consultas LINQ**: Tipos anônimos são frequentemente usados em consultas LINQ para projetar resultados personalizados.
```csharp
var students = new[]
{
    new { Name = "Alice", Age = 23 },
    new { Name = "Bob", Age = 25 }
};

var adults = from s in students
             where s.Age >= 18
             select new { s.Name, IsAdult = true };

foreach (var adult in adults)
{
    Console.WriteLine($"{adult.Name} is an adult.");
}
```

- **Agrupamento de Dados**: Agrupar dados de diferentes fontes em um único objeto.
```csharp
var item = new { Name = "Apple", Category = "Fruit", Price = 1.2 };
```

## Considerações
- **Tipo de Inferência**: O compilador infere o tipo dos campos de um tipo anônimo com base nos valores atribuídos.
- **Membros Somente Leitura**: Todas as propriedades de um tipo anônimo são somente leitura e não podem ser modificadas após a criação.
- **Igualdade**: A igualdade de tipos anônimos é baseada na estrutura e nos valores dos membros. Dois tipos anônimos são considerados iguais se eles têm as mesmas propriedades com os mesmos valores.

## Limitações
- **Escopo Limitado**: Tipos anônimos não podem ser retornados de métodos ou atribuídos a variáveis de classe. Eles são geralmente limitados ao escopo de métodos locais.
- **Manutenção de Código**: O uso excessivo de tipos anônimos pode dificultar a manutenção do código a longo prazo.

## Observações Importantes
- **Utilização Adequada**: Use tipos anônimos para encapsular dados de maneira rápida e temporária.
- **Não Substituem Classes**: Para estruturas de dados complexas e reutilizáveis, é preferível definir classes ou structs nomeados.
- **Propriedades**: A ordem das propriedades e seus nomes são importantes e definem a identidade do tipo anônimo.

## Dicas de Boas Práticas
- **Clareza do Código**: Utilize tipos anônimos para simplificar o código, mas evite usá-los excessivamente em aplicações complexas.
- **Documentação**: Documente o propósito dos tipos anônimos quando usados em consultas ou métodos para facilitar a compreensão do código.
- **Uso Temporário**: Restrinja o uso de tipos anônimos a escopos locais onde uma solução rápida e temporária é suficiente.
