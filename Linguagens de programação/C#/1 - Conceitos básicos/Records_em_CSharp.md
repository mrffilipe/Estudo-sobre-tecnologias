
# Records em C#

Records são uma forma especial de definir tipos de referência em C#, introduzida no C# 9.0, projetada para armazenar dados de forma imutável e facilitar a comparação de valores. Abaixo estão as principais informações e observações importantes sobre records conforme apresentadas na documentação:

## Características Principais
- **Imutabilidade**: Records são imutáveis por padrão, ou seja, seus membros não podem ser alterados após a criação do objeto.
- **Comparação de Valores**: A comparação de records é baseada nos valores de seus membros, ao contrário de classes, onde a comparação padrão é baseada na referência.

## Declaração de Records
- **Sintaxe Básica**: Um record é declarado usando a palavra-chave `record` seguida pelo nome do record e opcionalmente pelos parâmetros do construtor primário.
```csharp
public record Person(string FirstName, string LastName);
```

- **Propriedades**: As propriedades do record são definidas no construtor primário e são `public` e `init` apenas, o que significa que só podem ser atribuídas durante a inicialização.

## Benefícios dos Records
- **Desestruturação**: Records suportam desestruturação para facilitar a extração de valores.
```csharp
var person = new Person("John", "Doe");
var (firstName, lastName) = person;
Console.WriteLine($"First Name: {firstName}, Last Name: {lastName}");
```

- **With Expressions**: Permite criar cópias de records com algumas propriedades modificadas, mantendo a imutabilidade.
```csharp
var person1 = new Person("John", "Doe");
var person2 = person1 with { LastName = "Smith" };
```

## Herança de Records
- **Herança**: Records suportam herança, similar às classes.
```csharp
public record Person(string FirstName, string LastName);
public record Employee(string FirstName, string LastName, string Position) : Person(FirstName, LastName);
```

## Comparação e Igualdade
- **Equals e GetHashCode**: Os métodos `Equals` e `GetHashCode` são gerados automaticamente, baseados nos valores dos membros do record.
- **Operador == e !=**: Os operadores de igualdade (`==` e `!=`) são redefinidos para comparar os valores dos membros.

## Expressões de Membros de Dados
- **Com Expressões de Membros de Dados**: Permitem definir membros adicionais que não estão no construtor primário.
```csharp
public record Person(string FirstName, string LastName)
{
    public string FullName => $"{FirstName} {LastName}";
}
```

## Observações Importantes
- **Modificadores de Acesso**: Assim como em classes, os records podem ter modificadores de acesso.
- **Modificadores de Imutabilidade**: O uso de `init` para as propriedades permite definir valores apenas durante a inicialização, mantendo a imutabilidade.
- **Herança e Sealed**: Se a herança não for necessária, considere marcar o record como `sealed` para impedir a herança.

## Dicas de Boas Práticas
- **Uso Apropriado**: Utilize records quando precisar de um tipo principalmente para armazenar dados com imutabilidade e comparação de valores.
- **Desempenho**: Lembre-se de que a comparação de valores pode ter um impacto no desempenho para records com muitos membros.
- **Documentação**: Documente as propriedades e o propósito do record para facilitar a manutenção e compreensão do código.
