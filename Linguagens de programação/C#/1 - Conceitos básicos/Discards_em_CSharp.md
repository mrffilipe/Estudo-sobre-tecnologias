
# Discards em C#

Os discards (descartes) são um recurso do C# que permite ignorar valores que não são necessários. Eles são representados pelo caractere de sublinhado `_` e são úteis para tornar o código mais legível e expressivo ao indicar que certos valores não serão utilizados. Abaixo estão as principais informações e observações importantes sobre discards conforme apresentadas na documentação:

## Características Principais
- **Simplicidade**: Discards simplificam o código ao ignorar valores desnecessários.
- **Legibilidade**: Melhoram a legibilidade do código, indicando claramente que certos valores são intencionalmente ignorados.
- **Versatilidade**: Podem ser usados em diversas situações, como deconstrução, pattern matching, e parâmetros de saída.

## Usos Comuns
- **Deconstrução**: Ignorar valores durante a deconstrução de tuplas ou tipos complexos.
```csharp
(int, int) coordinates = (1, 2);
var (x, _) = coordinates;
Console.WriteLine($"X: {x}"); // Output: X: 1
```

- **Pattern Matching**: Ignorar partes de um padrão durante a correspondência.
```csharp
if (obj is (int _, int y))
{
    Console.WriteLine($"Y: {y}");
}
```

- **Parâmetros de Saída**: Ignorar valores de saída de métodos que usam parâmetros `out`.
```csharp
if (int.TryParse("123", out _))
{
    Console.WriteLine("Parsing succeeded.");
}
```

- **Expressões Lambda**: Ignorar parâmetros não utilizados em expressões lambda.
```csharp
Action<int> print = _ => Console.WriteLine("Ignored parameter.");
print(10); // Output: Ignored parameter.
```

## Exemplos de Uso
- **Ignorando Múltiplos Valores**: Em cenários onde múltiplos valores precisam ser ignorados.
```csharp
var (x, _, z, _) = (1, 2, 3, 4);
Console.WriteLine($"X: {x}, Z: {z}"); // Output: X: 1, Z: 3
```

- **Usando Discards com Tipos Anônimos**: Ignorar propriedades de tipos anônimos.
```csharp
var person = new { Name = "Alice", Age = 30 };
var (_, age) = (person.Name, person.Age);
Console.WriteLine($"Age: {age}"); // Output: Age: 30
```

## Observações Importantes
- **Sem Alocação**: Discards não alocam memória ou geram código adicional, pois são puramente sintáticos.
- **Intencionalidade**: O uso de discards indica claramente a intenção de ignorar certos valores, melhorando a documentação implícita do código.

## Dicas de Boas Práticas
- **Claridade**: Use discards para tornar o código mais claro e expressivo.
- **Evitar Descartes Desnecessários**: Não use discards se o valor pode ser relevante para futuras manutenções ou para outros desenvolvedores.
- **Comentários**: Adicione comentários explicativos se o uso de discards não for imediatamente óbvio.
