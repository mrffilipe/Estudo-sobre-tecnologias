
# Classes em C#

Classes são os blocos de construção fundamentais da programação orientada a objetos em C#. Elas permitem encapsular dados e comportamentos que operam sobre esses dados. Abaixo estão as principais informações e observações importantes sobre classes conforme apresentadas na documentação:

## Características Principais
- **Encapsulamento**: Classes encapsulam dados (campos) e comportamentos (métodos) que operam sobre esses dados.
- **Reutilização de Código**: Classes permitem a reutilização de código através da herança e composição.
- **Modularidade**: Classes ajudam a modularizar o código, tornando-o mais fácil de entender, manter e escalar.

## Declaração de Classes
- **Sintaxe Básica**: Uma classe é declarada usando a palavra-chave `class` seguida pelo nome da classe.
```csharp
public class MyClass
{
    // Campos, propriedades, métodos, etc.
}
```

- **Acessibilidade**: Modificadores de acesso, como `public`, `private`, `protected` e `internal`, controlam a visibilidade e o acesso aos membros da classe.
```csharp
public class MyClass
{
    private int myField;
    public int MyProperty { get; set; }

    public void MyMethod()
    {
        // Implementação do método
    }
}
```

## Membros da Classe
- **Campos**: Variáveis que armazenam dados da classe.
- **Propriedades**: Mecanismos para ler, escrever ou computar os valores dos campos privados.
- **Métodos**: Funções definidas dentro da classe que realizam operações sobre os dados da classe.
- **Construtores**: Métodos especiais chamados quando uma instância da classe é criada. Eles inicializam os campos da classe.

Exemplo de uma classe com campos, propriedades, métodos e um construtor:
```csharp
public class Car
{
    private string model;
    private int year;

    // Construtor
    public Car(string model, int year)
    {
        this.model = model;
        this.year = year;
    }

    // Propriedade
    public string Model
    {
        get { return model; }
        set { model = value; }
    }

    // Método
    public void DisplayInfo()
    {
        Console.WriteLine($"Model: {model}, Year: {year}");
    }
}
```

## Herança
- **Conceito**: A herança permite que uma classe (classe derivada) herde membros de outra classe (classe base).
- **Sintaxe**: Utiliza-se o símbolo `:` para indicar que uma classe está herdando de outra.
```csharp
public class ElectricCar : Car
{
    private int batteryCapacity;

    public ElectricCar(string model, int year, int batteryCapacity)
        : base(model, year)
    {
        this.batteryCapacity = batteryCapacity;
    }

    public void DisplayBattery()
    {
        Console.WriteLine($"Battery Capacity: {batteryCapacity} kWh");
    }
}
```

## Polimorfismo
- **Conceito**: Permite que métodos em classes derivadas tenham comportamentos diferentes, mas sejam chamados através de uma referência da classe base.
- **Métodos Virtuais**: Métodos na classe base que podem ser sobrescritos nas classes derivadas.
```csharp
public class Car
{
    public virtual void Drive()
    {
        Console.WriteLine("The car is driving.");
    }
}

public class ElectricCar : Car
{
    public override void Drive()
    {
        Console.WriteLine("The electric car is driving silently.");
    }
}
```

## Observações Importantes
- **Construtores**: Podem ser sobrecarregados para fornecer diferentes formas de inicializar uma classe.
- **Destrutores**: Usados para liberar recursos quando uma instância da classe é destruída.
- **Membros Estáticos**: Pertencem à classe em si, em vez de instâncias individuais.

## Dicas de Boas Práticas
- **Encapsulamento**: Sempre que possível, use encapsulamento para proteger os dados internos da classe.
- **Nomeação**: Use convenções de nomeação claras e consistentes para classes, métodos e propriedades.
- **Coesão**: Mantenha as classes coesas, com responsabilidade única.
- **Documentação**: Documente as classes e seus membros para facilitar a manutenção e o entendimento do código.
- **Testes**: Escreva testes unitários para classes para garantir que elas funcionem conforme esperado.
