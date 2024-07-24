
# Exceções em C#

Exceções em C# são eventos inesperados que ocorrem durante a execução de um programa e que interrompem o fluxo normal do código. A manipulação de exceções permite tratar esses eventos de forma controlada, garantindo que o programa possa continuar ou encerrar de maneira limpa. Abaixo estão as principais informações e observações importantes sobre exceções conforme apresentadas na documentação:

## Características Principais
- **Interrupção do Fluxo**: Exceções interrompem o fluxo normal do programa quando ocorrem.
- **Tipos de Exceções**: Existem várias exceções predefinidas, como `ArgumentNullException`, `InvalidOperationException`, `DivideByZeroException`, entre outras.
- **Herança**: Todas as exceções derivam da classe base `Exception`.

## Manipulação de Exceções
- **Bloco try-catch**: Permite capturar e tratar exceções.
```csharp
try
{
    // Código que pode lançar uma exceção
}
catch (Exception ex)
{
    // Código para tratar a exceção
    Console.WriteLine(ex.Message);
}
```

- **Bloco finally**: Usado para executar código que deve ser executado independentemente de uma exceção ter sido lançada ou não.
```csharp
try
{
    // Código que pode lançar uma exceção
}
catch (Exception ex)
{
    // Código para tratar a exceção
    Console.WriteLine(ex.Message);
}
finally
{
    // Código que sempre será executado
    Console.WriteLine("Execução finalizada.");
}
```

- **Captura de Exceções Específicas**: É possível capturar exceções específicas em vez de capturar todas as exceções.
```csharp
try
{
    int result = 10 / int.Parse("0");
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("Divisão por zero não permitida.");
}
catch (FormatException ex)
{
    Console.WriteLine("Formato inválido.");
}
```

## Lançamento de Exceções
- **Palavra-chave throw**: Usada para lançar exceções.
```csharp
public void ValidateAge(int age)
{
    if (age < 0)
    {
        throw new ArgumentOutOfRangeException(nameof(age), "Idade não pode ser negativa.");
    }
}
```

## Exceções Personalizadas
- **Criação de Exceções Personalizadas**: Permite definir tipos de exceção específicos para sua aplicação.
```csharp
public class InvalidUserException : Exception
{
    public InvalidUserException(string message) : base(message)
    {
    }
}
```

## Observações Importantes
- **Desempenho**: O lançamento e captura de exceções podem ter um impacto no desempenho, por isso deve ser usado com cuidado.
- **Boa Prática**: Evite capturar exceções gerais como `Exception` sem uma boa razão.
- **Mensagem de Erro**: Forneça mensagens de erro claras e significativas ao lançar exceções.

## Dicas de Boas Práticas
- **Especifique Exceções**: Capture exceções específicas em vez de usar exceções gerais.
- **Use Finally**: Utilize blocos `finally` para liberar recursos ou executar código de limpeza.
- **Valide Dados**: Valide dados antes de operações críticas para evitar exceções.
- **Documentação**: Documente as exceções que seus métodos podem lançar para melhorar a manutenção e compreensão do código.
