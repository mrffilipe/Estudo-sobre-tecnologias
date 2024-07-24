
# Criando e Lançando Exceções em C#

Criar e lançar exceções de maneira adequada é essencial para a robustez e manutenção de aplicações em C#. Abaixo estão as principais informações e boas práticas sobre como criar e lançar exceções conforme apresentadas na documentação:

## Criando Exceções Personalizadas
- **Quando Criar**: Crie exceções personalizadas quando as exceções predefinidas não representam adequadamente o erro específico do seu domínio de aplicação.
- **Herdar de Exception**: Todas as exceções personalizadas devem herdar da classe base `Exception`.
```csharp
public class InvalidAgeException : Exception
{
    public InvalidAgeException()
    {
    }

    public InvalidAgeException(string message) 
        : base(message)
    {
    }

    public InvalidAgeException(string message, Exception inner) 
        : base(message, inner)
    {
    }
}
```

- **Adicionar Construtores**: Inclua construtores padrão e sobrecarregados para fornecer flexibilidade ao criar a exceção.
```csharp
public class CustomException : Exception
{
    public CustomException()
    {
    }

    public CustomException(string message) 
        : base(message)
    {
    }

    public CustomException(string message, Exception innerException) 
        : base(message, innerException)
    {
    }
}
```

## Lançando Exceções
- **Throw**: Use a palavra-chave `throw` para lançar exceções.
```csharp
if (age < 0)
{
    throw new InvalidAgeException("A idade não pode ser negativa.");
}
```

- **Encapsular Exceções**: Encapsule exceções internas em exceções mais específicas para adicionar contexto ao erro.
```csharp
try
{
    // Código que pode lançar exceção
}
catch (Exception ex)
{
    throw new CustomException("Erro ao processar a operação.", ex);
}
```

## Boas Práticas para Lançar Exceções
- **Forneça Mensagens Claras**: As mensagens de exceção devem ser claras e descritivas para ajudar na depuração.
```csharp
throw new ArgumentNullException(nameof(param), "O parâmetro não pode ser nulo.");
```

- **Não Lançar Exceções de Controle de Fluxo**: Evite usar exceções para controlar o fluxo normal do programa.
- **Verificação de Argumentos**: Utilize exceções para validar argumentos de métodos.
```csharp
public void SetAge(int age)
{
    if (age < 0 || age > 150)
    {
        throw new ArgumentOutOfRangeException(nameof(age), "A idade deve estar entre 0 e 150.");
    }
    this.age = age;
}
```

- **Inner Exceptions**: Use o parâmetro `innerException` para incluir a exceção original ao lançar uma nova exceção.
```csharp
try
{
    // Código que pode lançar exceção
}
catch (Exception ex)
{
    throw new CustomException("Erro ao processar a operação.", ex);
}
```

## Observações Importantes
- **Performance**: O lançamento de exceções pode ser custoso em termos de desempenho. Use exceções para condições verdadeiramente excepcionais.
- **Evite Swallowing Exceptions**: Não capture exceções sem tratá-las ou sem fornecer informações úteis para a depuração.
- **Documentação**: Documente as exceções que seus métodos podem lançar para facilitar a compreensão e manutenção do código.

## Exemplos Práticos
- **Exceção Simples**:
```csharp
public void ProcessData(object data)
{
    if (data == null)
    {
        throw new ArgumentNullException(nameof(data), "Os dados não podem ser nulos.");
    }
    // Processamento dos dados
}
```

- **Exceção Personalizada**:
```csharp
public class InvalidUserInputException : Exception
{
    public InvalidUserInputException() : base("Entrada de usuário inválida.")
    {
    }

    public InvalidUserInputException(string message) : base(message)
    {
    }

    public InvalidUserInputException(string message, Exception innerException) : base(message, innerException)
    {
    }
}
```
