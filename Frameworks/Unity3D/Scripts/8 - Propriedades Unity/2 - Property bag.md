
# Documentação sobre Property Bags no Unity3D

## Introdução

Property Bags no Unity3D são usadas para inspecionar, editar e serializar propriedades de maneira genérica. Elas são particularmente úteis para ferramentas e sistemas que precisam operar sobre objetos de forma extensível e independente de tipos específicos.

## Componentes Principais

1. **`PropertyBag`**:
   - Uma coleção de propriedades de um tipo específico.
   - Facilita o acesso genérico a propriedades de objetos.
   - Exemplo:
     ```csharp
     public class Example
     {
         public int Value { get; set; }
     }

     var propertyBag = PropertyBagStore.GetPropertyBag<Example>();
     ```

2. **`IProperty`**:
   - Interface que representa uma propriedade.
   - Contém informações como nome, tipo e métodos para obter e definir valores.
   - Exemplo:
     ```csharp
     foreach (var property in propertyBag.GetProperties(ref example))
     {
         Debug.Log(property.Name);
     }
     ```

3. **`PropertyBagStore`**:
   - Armazena e fornece acesso aos `PropertyBag` registrados.
   - Facilita o registro e a recuperação de `PropertyBags`.
   - Exemplo:
     ```csharp
     PropertyBagStore.AddPropertyBag(new ExamplePropertyBag());
     var propertyBag = PropertyBagStore.GetPropertyBag<Example>();
     ```

## Uso de Property Bags

1. **Inspeção de Propriedades**:
   - Obtenha um `PropertyBag` para o tipo desejado.
   - Liste e acesse propriedades de instâncias desse tipo.
   - Exemplo:
     ```csharp
     var propertyBag = PropertyBagStore.GetPropertyBag<Example>();
     Example example = new Example();
     foreach (var property in propertyBag.GetProperties(ref example))
     {
         Debug.Log($"Property Name: {property.Name}, Value: {property.GetValue(ref example)}");
     }
     ```

2. **Edição de Propriedades**:
   - Modifique os valores das propriedades de uma instância.
   - Exemplo:
     ```csharp
     var propertyBag = PropertyBagStore.GetPropertyBag<Example>();
     Example example = new Example();
     foreach (var property in propertyBag.GetProperties(ref example))
     {
         if (property.Name == "Value")
         {
             property.SetValue(ref example, 10);
         }
     }
     ```

3. **Serialização**:
   - Use `PropertyBags` para serializar e desserializar objetos de forma genérica.
   - Facilita a integração com sistemas de persistência de dados.
   - Exemplo:
     ```csharp
     var propertyBag = PropertyBagStore.GetPropertyBag<Example>();
     Example example = new Example { Value = 5 };
     string json = JsonUtility.ToJson(example);
     Example deserializedExample = JsonUtility.FromJson<Example>(json);
     ```

## Benefícios do Uso de Property Bags

1. **Flexibilidade**:
   - Permitem o desenvolvimento de ferramentas genéricas para inspecionar, editar e serializar objetos.
   - Facilitam a extensão e manutenção de código.

2. **Independência de Tipo**:
   - Operam sobre objetos de maneira genérica, sem precisar conhecer os tipos específicos em tempo de compilação.
   - Reduzem a necessidade de código repetitivo para diferentes tipos.

3. **Integração Simplificada**:
   - Integram-se facilmente com sistemas de serialização, UI de editores e outras ferramentas.
   - Aumentam a produtividade ao facilitar operações comuns sobre objetos.

## Considerações

1. **Desempenho**:
   - Embora flexíveis, o uso de `PropertyBags` pode introduzir uma pequena sobrecarga em comparação com acesso direto a propriedades.
   - Use com cautela em partes críticas de desempenho do código.

2. **Manutenção**:
   - Mantenha os `PropertyBags` atualizados ao modificar os tipos subjacentes para garantir a consistência.
   - Teste rigorosamente para evitar problemas com propriedades não registradas ou mal configuradas.

3. **Segurança de Tipos**:
   - O uso genérico pode levar a erros em tempo de execução se não for cuidadosamente gerenciado.
   - Implemente validações e testes para garantir a robustez do sistema.

## Exemplo Completo de Uso de Property Bags

```csharp
using UnityEngine;
using Unity.Properties;

public class Example
{
    public int Value { get; set; }
}

public class ExamplePropertyBag : ContainerPropertyBag<Example>
{
    public ExamplePropertyBag()
    {
        AddProperty(new DelegateProperty<Example, int>(
            "Value",
            (ref Example c) => c.Value,
            (ref Example c, int v) => c.Value = v
        ));
    }
}

public class PropertyBagExample : MonoBehaviour
{
    void Start()
    {
        PropertyBagStore.AddPropertyBag(new ExamplePropertyBag());
        var propertyBag = PropertyBagStore.GetPropertyBag<Example>();
        Example example = new Example { Value = 5 };

        foreach (var property in propertyBag.GetProperties(ref example))
        {
            Debug.Log($"Property Name: {property.Name}, Value: {property.GetValue(ref example)}");
            if (property.Name == "Value")
            {
                property.SetValue(ref example, 10);
            }
        }

        Debug.Log($"New Value: {example.Value}");
    }
}
```
