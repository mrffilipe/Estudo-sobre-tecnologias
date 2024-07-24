
# Pattern Matching em C#

Pattern Matching (Correspondência de Padrões) é um recurso poderoso em C# que permite inspeção e deconstrução de dados de maneira expressiva e concisa. Ele facilita a verificação e a manipulação de valores complexos, tornando o código mais legível e menos propenso a erros. Abaixo estão as principais informações e observações importantes sobre Pattern Matching conforme apresentadas na documentação:

## Características Principais
- **Expressividade**: Permite escrever código que verifica e manipula valores complexos de maneira clara e concisa.
- **Segurança de Tipos**: Oferece verificação de tipos em tempo de compilação, reduzindo erros em tempo de execução.
- **Versatilidade**: Suporta correspondência com tipos, valores e estruturas.

## Tipos de Pattern Matching
- **Patterns Literais**: Compara diretamente com um valor literal.
```csharp
object obj = 5;
if (obj is 5)
{
    Console.WriteLine("The object is 5.");
}
```

- **Patterns de Tipo**: Verifica se um objeto é de um tipo específico.
```csharp
object obj = "hello";
if (obj is string s)
{
    Console.WriteLine($"The object is a string: {s}");
}
```

- **Patterns de Constante**: Compara um valor com uma constante.
```csharp
const int x = 10;
object obj = 10;
if (obj is x)
{
    Console.WriteLine("The object is 10.");
}
```

- **Patterns de Propriedade**: Verifica propriedades de um objeto.
```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

Person person = new Person { Name = "Alice", Age = 30 };
if (person is { Name: "Alice", Age: 30 })
{
    Console.WriteLine("The person is Alice and is 30 years old.");
}
```

- **Patterns Posicionais**: Decompõe um objeto em seus componentes.
```csharp
public record Point(int X, int Y);

Point point = new Point(3, 4);
if (point is (3, 4))
{
    Console.WriteLine("The point is at (3, 4).");
}
```

## Usos Comuns
- **Switch Expressions**: Utiliza pattern matching dentro de expressões `switch` para simplificar a lógica de ramificação.
```csharp
static string Classify(object obj) => obj switch
{
    1 => "One",
    int n when n > 0 => "Positive integer",
    string s => $"String of length {s.Length}",
    _ => "Other"
};
```

- **Expressões Is**: Usa a expressão `is` para verificar e deconstruir valores.
```csharp
if (obj is int n && n > 0)
{
    Console.WriteLine($"The object is a positive integer: {n}");
}
```

- **Deconstrução**: Deconstrói objetos em seus componentes diretamente nas variáveis.
```csharp
var (x, y) = point;
Console.WriteLine($"X: {x}, Y: {y}");
```

## Observações Importantes
- **Desempenho**: Pattern matching é otimizado para desempenho, mas deve ser usado com cuidado em casos críticos de performance.
- **Legibilidade**: Facilita a legibilidade do código, especialmente ao lidar com estruturas de dados complexas.
- **Manutenibilidade**: Simplifica a manutenção do código, tornando a lógica mais clara e menos propensa a erros.

## Dicas de Boas Práticas
- **Clareza**: Use pattern matching para tornar o código mais claro e expressivo.
- **Simplicidade**: Evite padrões complexos que possam comprometer a legibilidade.
- **Documentação**: Documente os padrões usados para facilitar a compreensão do código.
- **Testes**: Escreva testes abrangentes para garantir que os padrões correspondam corretamente aos casos esperados.
