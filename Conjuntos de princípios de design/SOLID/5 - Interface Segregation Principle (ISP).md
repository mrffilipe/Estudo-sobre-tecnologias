
# 4. Interface Segregation Principle (ISP)

## 4.1 Conceito de segregação de interfaces

O Princípio da Segregação de Interfaces (Interface Segregation Principle - ISP) afirma que uma classe não deve ser forçada a implementar interfaces que ela não utiliza. Em vez de uma interface geral e inchada, é preferível ter várias interfaces específicas e coesas que agrupam métodos relacionados. Isso ajuda a reduzir o acoplamento e aumentar a modularidade do sistema.

## 4.2 Vantagens do ISP

- **Redução do acoplamento**: As classes são menos dependentes de métodos que não utilizam, facilitando a manutenção e a evolução do sistema.
- **Maior coesão**: Interfaces menores e mais específicas promovem a coesão, tornando as responsabilidades das interfaces mais claras.
- **Facilidade de implementação**: Classes que implementam interfaces menores têm menos métodos a implementar, simplificando o desenvolvimento.
- **Melhor testabilidade**: Facilita a criação de mocks e stubs para testes unitários, pois as interfaces menores são mais fáceis de simular.

## 4.3 Identificação de interfaces inchadas

Para identificar interfaces inchadas, considere os seguintes pontos:

- **Muitos métodos**: Interfaces com muitos métodos podem estar agrupando funcionalidades não relacionadas.
- **Métodos não utilizados**: Se várias classes que implementam a mesma interface não utilizam todos os métodos, isso pode indicar que a interface está inchada.
- **Responsabilidades múltiplas**: Interfaces que definem métodos para diferentes responsabilidades podem precisar ser segregadas em interfaces menores.

## 4.4 Refatoração para ISP

Refatorar para cumprir o ISP envolve dividir interfaces grandes e inchadas em várias interfaces menores, cada uma focada em um conjunto coeso de métodos. As classes devem então implementar apenas as interfaces que são relevantes para elas.

## Exemplo em C#

### Antes da refatoração:
```csharp
public interface ITrabalhador
{
    void Trabalhar();
    void Descansar();
    void Cozinhar();
    void Dirigir();
}

public class Engenheiro : ITrabalhador
{
    public void Trabalhar()
    {
        // Lógica de trabalho
    }

    public void Descansar()
    {
        // Lógica de descanso
    }

    public void Cozinhar()
    {
        // Não implementado
        throw new NotImplementedException();
    }

    public void Dirigir()
    {
        // Não implementado
        throw new NotImplementedException();
    }
}
```

### Após a refatoração usando ISP:
```csharp
public interface ITrabalho
{
    void Trabalhar();
}

public interface IDescanso
{
    void Descansar();
}

public interface ICozinhar
{
    void Cozinhar();
}

public interface IDirigir
{
    void Dirigir();
}

public class Engenheiro : ITrabalho, IDescanso
{
    public void Trabalhar()
    {
        // Lógica de trabalho
    }

    public void Descansar()
    {
        // Lógica de descanso
    }
}
```

Neste exemplo, a interface `ITrabalhador` foi dividida em várias interfaces menores (`ITrabalho`, `IDescanso`, `ICozinhar`, `IDirigir`), cada uma representando uma responsabilidade específica. A classe `Engenheiro` agora implementa apenas as interfaces `ITrabalho` e `IDescanso`, evitando métodos não utilizados e cumprindo o ISP.
