
# 2. Open/Closed Principle (OCP)

## 2.1 O que significa estar aberto para extensão e fechado para modificação

O Princípio Aberto/Fechado (Open/Closed Principle - OCP) afirma que as entidades de software (classes, módulos, funções, etc.) devem estar abertas para extensão, mas fechadas para modificação. Isso significa que o comportamento de uma classe pode ser estendido sem alterar seu código fonte original. Este princípio incentiva a construção de sistemas flexíveis e reutilizáveis, onde novas funcionalidades podem ser adicionadas com o mínimo impacto sobre o código existente.

## 2.2 Vantagens do OCP

- **Manutenção facilitada**: Reduz a necessidade de modificar o código existente, diminuindo o risco de introduzir novos bugs.
- **Extensibilidade**: Facilita a adição de novas funcionalidades sem afetar as implementações existentes.
- **Reutilização de código**: Promove o uso de componentes reutilizáveis, aumentando a eficiência do desenvolvimento.
- **Testabilidade**: Melhora a testabilidade ao isolar novas funcionalidades em componentes separados.

## 2.3 Uso de herança e interfaces para cumprir OCP

Para cumprir o OCP, pode-se usar herança e interfaces para permitir a extensão do comportamento das classes sem modificá-las diretamente. A herança permite criar novas classes baseadas em classes existentes, enquanto as interfaces definem contratos que as classes devem cumprir, permitindo implementações variadas.

## Exemplo em C#

### Antes da refatoração:
```csharp
public class CalculadoraDeDesconto
{
    public double CalcularDesconto(string tipoCliente, double valorCompra)
    {
        if (tipoCliente == "Regular")
        {
            return valorCompra * 0.1;
        }
        else if (tipoCliente == "Premium")
        {
            return valorCompra * 0.2;
        }
        else
        {
            return 0;
        }
    }
}
```

### Após a refatoração usando OCP:
```csharp
public interface IDesconto
{
    double Calcular(double valorCompra);
}

public class DescontoRegular : IDesconto
{
    public double Calcular(double valorCompra)
    {
        return valorCompra * 0.1;
    }
}

public class DescontoPremium : IDesconto
{
    public double Calcular(double valorCompra)
    {
        return valorCompra * 0.2;
    }
}

public class CalculadoraDeDesconto
{
    private readonly IDesconto _desconto;

    public CalculadoraDeDesconto(IDesconto desconto)
    {
        _desconto = desconto;
    }

    public double Calcular(double valorCompra)
    {
        return _desconto.Calcular(valorCompra);
    }
}

// Uso
var calculadoraRegular = new CalculadoraDeDesconto(new DescontoRegular());
var descontoRegular = calculadoraRegular.Calcular(100);

var calculadoraPremium = new CalculadoraDeDesconto(new DescontoPremium());
var descontoPremium = calculadoraPremium.Calcular(100);
```

Neste exemplo, a classe `CalculadoraDeDesconto` foi refatorada para seguir o OCP. As diferentes estratégias de cálculo de desconto foram extraídas para classes separadas (`DescontoRegular` e `DescontoPremium`), que implementam a interface `IDesconto`. Isso permite adicionar novas estratégias de desconto sem modificar a classe `CalculadoraDeDesconto`.
