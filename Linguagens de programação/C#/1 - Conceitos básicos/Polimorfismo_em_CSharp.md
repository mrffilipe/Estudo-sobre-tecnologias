
# Polimorfismo em C#

O polimorfismo é um dos quatro pilares da Programação Orientada a Objetos (POO) em C#. Ele permite que objetos de diferentes classes sejam tratados de forma unificada, possibilitando a utilização de um método de várias maneiras. Abaixo estão as principais informações e observações importantes sobre polimorfismo conforme apresentadas na documentação:

## Características Principais
- **Definição**: Polimorfismo permite que métodos em classes derivadas tenham comportamentos diferentes, mas sejam chamados através de uma referência da classe base.
- **Tipos de Polimorfismo**: Em C#, o polimorfismo pode ser alcançado através de sobrecarga de métodos, sobreposição de métodos e interfaces.

## Sobrecarga de Métodos
- **Definição**: Permite a criação de vários métodos com o mesmo nome, mas com diferentes assinaturas.
```csharp
public class MathOperations
{
    public int Add(int a, int b) => a + b;
    public double Add(double a, double b) => a + b;
}
```

## Sobrescrita de Métodos
- **Definição**: Permite que uma classe derivada forneça uma implementação específica de um método que já é definido em sua classe base.
- **Métodos Virtuais**: A classe base define um método como `virtual` e a classe derivada o sobrescreve usando a palavra-chave `override`.
```csharp
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("Animal speaks.");
    }
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Dog barks.");
    }
}
```

## Polimorfismo em Ação
- **Referência da Classe Base**: Um objeto da classe derivada pode ser tratado como um objeto da classe base.
```csharp
Animal myAnimal = new Dog();
myAnimal.Speak(); // Output: Dog barks.
```

- **Coleções Polimórficas**: Permite armazenar diferentes tipos de objetos em uma coleção unificada.
```csharp
List<Animal> animals = new List<Animal>
{
    new Dog(),
    new Cat()
};

foreach (var animal in animals)
{
    animal.Speak();
}
```

## Interfaces e Polimorfismo
- **Interfaces**: As interfaces definem contratos que podem ser implementados por qualquer classe ou struct, permitindo o polimorfismo.
```csharp
public interface IShape
{
    double Area();
}

public class Circle : IShape
{
    public double Radius { get; set; }
    public double Area() => Math.PI * Radius * Radius;
}

public class Square : IShape
{
    public double Side { get; set; }
    public double Area() => Side * Side;
}
```

## Observações Importantes
- **Segurança em Tempo de Execução**: A verificação de tipos em tempo de execução garante que as operações polimórficas sejam seguras.
- **Performance**: Embora o polimorfismo aumente a flexibilidade e a reutilização, pode haver um pequeno impacto na performance devido ao despacho de método virtual.

## Dicas de Boas Práticas
- **Usar Polimorfismo com Moderação**: Utilize o polimorfismo de maneira sensata para evitar complexidade desnecessária.
- **Interfaces para Flexibilidade**: Prefira usar interfaces para promover a flexibilidade e a manutenção do código.
- **Documentação e Testes**: Documente claramente o comportamento esperado dos métodos polimórficos e escreva testes para garantir a corretude do código.
