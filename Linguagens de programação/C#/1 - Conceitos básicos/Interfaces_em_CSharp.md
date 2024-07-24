
# Interfaces em C#

Interfaces em C# são tipos que definem um contrato que outras classes ou structs podem implementar. Elas especificam membros que devem ser implementados pelas classes ou structs que adotam a interface, mas não fornecem uma implementação. Abaixo estão as principais informações e observações importantes sobre interfaces conforme apresentadas na documentação:

## Características Principais
- **Contrato**: Interfaces definem um conjunto de membros que as classes ou structs devem implementar.
- **Sem Implementação**: Interfaces não contêm implementação de métodos ou propriedades, apenas suas assinaturas.
- **Multiplicidade**: Uma classe ou struct pode implementar várias interfaces.

## Declaração de Interfaces
- **Sintaxe Básica**: Uma interface é declarada usando a palavra-chave `interface` seguida pelo nome da interface.
```csharp
public interface IShape
{
    double Area { get; }
    double Perimeter();
}
```

## Implementação de Interfaces
- **Implementação em Classes**: Classes que implementam uma interface devem fornecer uma implementação para todos os membros da interface.
```csharp
public class Rectangle : IShape
{
    public double Length { get; set; }
    public double Width { get; set; }

    public double Area => Length * Width;

    public double Perimeter()
    {
        return 2 * (Length + Width);
    }
}
```

- **Implementação em Structs**: Structs também podem implementar interfaces.
```csharp
public struct Circle : IShape
{
    public double Radius { get; set; }

    public double Area => Math.PI * Radius * Radius;

    public double Perimeter()
    {
        return 2 * Math.PI * Radius;
    }
}
```

## Herança de Interfaces
- **Interface Herança**: Interfaces podem herdar de outras interfaces, permitindo a criação de hierarquias de interfaces.
```csharp
public interface IPolygon : IShape
{
    int NumberOfSides { get; }
}
```

## Polimorfismo
- **Polimorfismo**: Interfaces permitem o uso de polimorfismo, onde uma variável do tipo de uma interface pode referenciar qualquer objeto que implemente essa interface.
```csharp
IShape shape = new Rectangle { Length = 5, Width = 3 };
Console.WriteLine($"Area: {shape.Area}, Perimeter: {shape.Perimeter()}");
```

## Membros da Interface
- **Métodos**: Interfaces podem declarar métodos que devem ser implementados.
- **Propriedades**: Interfaces podem declarar propriedades.
- **Eventos**: Interfaces podem declarar eventos.
- **Indexadores**: Interfaces podem declarar indexadores.

## Default Interface Methods
- **Métodos Padrão**: A partir do C# 8.0, as interfaces podem conter métodos padrão com implementação.
```csharp
public interface ILoggable
{
    void Log(string message)
    {
        Console.WriteLine(message);
    }
}
```

## Observações Importantes
- **Modificadores de Acesso**: Os membros de uma interface são implicitamente `public` e não podem ter modificadores de acesso.
- **Flexibilidade**: Interfaces oferecem flexibilidade ao permitir que diferentes classes ou structs implementem o mesmo conjunto de membros de maneiras diferentes.
- **Desempenho**: Implementações de interfaces podem ter uma ligeira sobrecarga de desempenho devido ao despacho de método virtual.

## Dicas de Boas Práticas
- **Nomenclatura**: Use o prefixo `I` para nomes de interfaces para diferenciá-las facilmente de classes e structs.
- **Coerência**: Mantenha as interfaces coesas, definindo membros que estão logicamente relacionados.
- **Documentação**: Documente claramente o contrato da interface para que os implementadores entendam as expectativas.
- **Reutilização**: Utilize interfaces para promover a reutilização de código e evitar duplicação.
