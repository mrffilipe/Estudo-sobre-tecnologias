
# Usando Exceções em C#

A utilização correta de exceções é fundamental para a criação de aplicações robustas e resilientes. Abaixo estão as principais informações e boas práticas sobre como usar exceções em C# conforme apresentadas na documentação:

## Características Principais
- **Mecanismo de Tratamento**: Exceções fornecem um mecanismo para tratar erros em tempo de execução de maneira estruturada.
- **Códigos de Erro vs. Exceções**: O uso de exceções é preferido em relação a códigos de erro, pois oferece um mecanismo mais claro e seguro para sinalizar e tratar erros.

## Uso Adequado de Exceções
- **Quando Usar**: Utilize exceções para condições de erro que são inesperadas ou não recuperáveis.
- **Quando Evitar**: Evite usar exceções para controle de fluxo ou para situações que podem ser tratadas por lógica normal do programa.

## Criação e Lançamento de Exceções
- **Exceções Predefinidas**: Use exceções predefinidas sempre que possível, como `ArgumentNullException`, `InvalidOperationException`, etc.
- **Exceções Personalizadas**: Crie exceções personalizadas apenas quando uma exceção predefinida não é adequada.
```csharp
public class CustomException : Exception
{
    public CustomException(string message) : base(message)
    {
    }
}
```

- **Lançamento de Exceções**: Lance exceções usando a palavra-chave `throw`.
```csharp
if (age < 0)
{
    throw new ArgumentOutOfRangeException(nameof(age), "Idade não pode ser negativa.");
}
```

## Manipulação de Exceções
- **Bloco try-catch-finally**: Use `try` para o código que pode gerar exceções, `catch` para tratar exceções, e `finally` para executar código que deve ser executado independentemente de uma exceção.
```csharp
try
{
    // Código que pode gerar exceção
}
catch (Exception ex)
{
    // Tratamento da exceção
    Console.WriteLine(ex.Message);
}
finally
{
    // Código de limpeza
    Console.WriteLine("Bloco finally executado.");
}
```

- **Captura de Exceções Específicas**: Capture exceções específicas para tratar casos distintos de maneira adequada.
```csharp
try
{
    // Código que pode gerar exceção
}
catch (ArgumentNullException ex)
{
    // Tratamento específico para ArgumentNullException
    Console.WriteLine("Argumento nulo não permitido.");
}
catch (Exception ex)
{
    // Tratamento genérico para outras exceções
    Console.WriteLine(ex.Message);
}
```

## Boas Práticas
- **Documentação**: Documente as exceções que os métodos podem lançar usando comentários XML.
```csharp
/// <summary>
/// Calcula a divisão de dois números.
/// </summary>
/// <param name="numerator">O numerador.</param>
/// <param name="denominator">O denominador.</param>
/// <returns>O resultado da divisão.</returns>
/// <exception cref="DivideByZeroException">Lançada quando o denominador é zero.</exception>
public static double Divide(int numerator, int denominator)
{
    if (denominator == 0)
    {
        throw new DivideByZeroException("O denominador não pode ser zero.");
    }
    return (double)numerator / denominator;
}
```

- **Evite Swallowing Exceptions**: Não capture exceções sem tratá-las ou sem registrar a ocorrência.
```csharp
try
{
    // Código que pode gerar exceção
}
catch (Exception)
{
    // Não fazer nada aqui é uma má prática
}
```

- **Use Exceções com Moderação**: Exceções devem ser usadas para situações excepcionais. Para lógica de fluxo normal, use estruturas de controle padrão como `if-else`.

## Observações Importantes
- **Impacto no Desempenho**: O uso excessivo de exceções pode afetar o desempenho da aplicação. Use-as judiciosamente.
- **Exceções Não Verificadas**: Em C#, todas as exceções são não verificadas, ou seja, o compilador não força o tratamento de exceções, mas é importante tratá-las adequadamente para evitar falhas em tempo de execução.
