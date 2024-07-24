
# 3. Liskov Substitution Principle (LSP)

## 3.1 Conceito de substituição de Liskov

O Princípio da Substituição de Liskov (Liskov Substitution Principle - LSP) foi introduzido por Barbara Liskov em 1987. O princípio afirma que se S é um subtipo de T, então objetos do tipo T em um programa devem poder ser substituídos por objetos do tipo S sem alterar as propriedades desejáveis do programa (correção, tarefa realizada, etc.). Em outras palavras, uma subclasse deve ser substituível por sua superclasse sem que o comportamento correto do programa seja alterado.

## 3.2 Vantagens do LSP

- **Correção do programa**: Assegura que o comportamento do programa não seja alterado ao substituir uma classe base por uma classe derivada.
- **Reutilização de código**: Promove a reutilização de código, permitindo que subclasses sejam usadas de forma intercambiável com suas superclasses.
- **Flexibilidade**: Aumenta a flexibilidade do sistema, facilitando a adição de novas funcionalidades através da herança.
- **Facilidade de manutenção**: Reduz o risco de introduzir bugs ao modificar ou estender o sistema.

## 3.3 Identificação de violações do LSP

Para identificar violações do LSP, considere os seguintes pontos:

- **Precondições mais fortes**: A subclasse não deve impor precondições mais fortes do que a classe base.
- **Pós-condições mais fracas**: A subclasse não deve enfraquecer as pós-condições estabelecidas pela classe base.
- **Exceções**: A subclasse não deve lançar exceções que a classe base não esperava ou não declarava.
- **Comportamento diferente**: A subclasse não deve alterar o comportamento que os clientes esperam da classe base.

## 3.4 Refatoração para cumprir LSP

Refatorar para cumprir o LSP envolve garantir que as subclasses respeitem os contratos definidos pelas classes base e que possam ser usadas de forma intercambiável sem alterar o comportamento esperado do programa.

## Exemplo em C#

### Antes da refatoração:
```csharp
public class Pato
{
    public virtual void Voar()
    {
        Console.WriteLine("O pato está voando.");
    }
}

public class PatoDeBorracha : Pato
{
    public override void Voar()
    {
        throw new InvalidOperationException("Patos de borracha não podem voar.");
    }
}
```

Neste exemplo, `PatoDeBorracha` viola o LSP, pois lança uma exceção quando o método `Voar` é chamado, o que não é esperado pela classe `Pato`.

### Após a refatoração:
```csharp
public abstract class Ave
{
    public abstract void FazerSom();
}

public interface IVoador
{
    void Voar();
}

public class Pato : Ave, IVoador
{
    public override void FazerSom()
    {
        Console.WriteLine("Quack");
    }

    public void Voar()
    {
        Console.WriteLine("O pato está voando.");
    }
}

public class PatoDeBorracha : Ave
{
    public override void FazerSom()
    {
        Console.WriteLine("Squeak");
    }
}
```

Neste exemplo, a classe `Ave` é a classe base, e `Pato` e `PatoDeBorracha` são subclasses. `Pato` implementa a interface `IVoador` para representar a capacidade de voar, enquanto `PatoDeBorracha` não implementa essa interface, evitando assim a violação do LSP.
