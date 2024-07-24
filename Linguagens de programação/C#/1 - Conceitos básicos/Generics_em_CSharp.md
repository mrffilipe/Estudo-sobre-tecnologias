
# Genéricos em C#

Genéricos são um recurso poderoso da linguagem C# que permite definir classes, métodos, interfaces e delegados com um ou mais parâmetros de tipo. Eles ajudam a criar componentes reutilizáveis e tipos seguros em tempo de compilação. Abaixo estão as principais informações e observações importantes sobre genéricos conforme apresentadas na documentação:

## Características Principais
- **Reutilização de Código**: Genéricos permitem escrever código que pode funcionar com qualquer tipo de dados.
- **Segurança em Tempo de Compilação**: Genéricos fornecem verificação de tipos em tempo de compilação, evitando muitos erros em tempo de execução.
- **Performance**: Genéricos podem melhorar a performance, pois evitam o boxing e unboxing de tipos de valor.

## Declaração de Genéricos
- **Sintaxe Básica**: Um tipo genérico é declarado usando a notação de colchetes angulares (`<T>`), onde `T` é um placeholder para o tipo que será fornecido pelo usuário.
```csharp
public class GenericClass<T>
{
    public T Data { get; set; }

    public void Display(T item)
    {
        Console.WriteLine(item);
    }
}
```

## Métodos Genéricos
- **Métodos Genéricos**: Métodos em classes genéricas ou não genéricas podem ser definidos como genéricos.
```csharp
public class GenericMethods
{
    public void Display<T>(T item)
    {
        Console.WriteLine(item);
    }
}
```

## Interfaces Genéricas
- **Interfaces Genéricas**: Interfaces também podem ser definidas como genéricas.
```csharp
public interface IRepository<T>
{
    void Add(T item);
    T Get(int id);
}
```

## Delegados Genéricos
- **Delegados Genéricos**: Delegados podem ser definidos como genéricos para encapsular métodos que têm parâmetros de tipo.
```csharp
public delegate T GenericDelegate<T>(T item);
```

## Restrições de Tipo
- **Restrições**: Genéricos podem ter restrições de tipo que especificam os requisitos que os tipos de argumento devem cumprir.
```csharp
public class GenericClass<T> where T : class
{
    public T Data { get; set; }
}
```

Tipos de restrições comuns:
- `where T : struct` - O tipo deve ser um tipo de valor.
- `where T : class` - O tipo deve ser um tipo de referência.
- `where T : new()` - O tipo deve ter um construtor sem parâmetros.
- `where T : <base class>` - O tipo deve ser ou derivar da classe base especificada.
- `where T : <interface>` - O tipo deve implementar a interface especificada.

## Coleções Genéricas
- **Coleções Genéricas**: A biblioteca de classes do .NET fornece várias coleções genéricas, como `List<T>`, `Dictionary<TKey, TValue>`, e `Queue<T>`.
```csharp
List<int> numbers = new List<int> { 1, 2, 3 };
Dictionary<int, string> dict = new Dictionary<int, string>();
dict.Add(1, "One");
dict.Add(2, "Two");
```

## Comparação com Não Genéricos
- **Não Genéricos vs Genéricos**: Comparado com as coleções não genéricas (`ArrayList`, `Hashtable`), as coleções genéricas são mais seguras e eficientes.

## Observações Importantes
- **Covariância e Contravariância**: Genéricos suportam covariância e contravariância, permitindo mais flexibilidade na atribuição de tipos.
- **Construtores Genéricos**: Classes genéricas podem ter construtores genéricos.
- **Especialização**: Genéricos podem ser especializados para tipos específicos, fornecendo implementações diferentes para tipos diferentes.

## Dicas de Boas Práticas
- **Uso Apropriado**: Use genéricos para criar APIs e bibliotecas reutilizáveis e seguras.
- **Restrições**: Utilize restrições de tipo para garantir que os tipos genéricos atendam aos requisitos necessários.
- **Documentação**: Documente claramente as expectativas e restrições dos tipos genéricos.
- **Testes**: Teste os tipos genéricos com vários tipos de dados para garantir a corretude e a flexibilidade.
