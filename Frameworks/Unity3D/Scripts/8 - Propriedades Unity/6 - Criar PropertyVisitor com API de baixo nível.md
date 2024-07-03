
# Documentação sobre a API de Baixo Nível dos Property Visitors no Unity3D

## Introdução

A API de Baixo Nível dos Property Visitors no Unity3D permite a criação de visitantes personalizados para inspeção e modificação de propriedades de objetos. Ela oferece uma maior flexibilidade e controle em comparação com as APIs de nível mais alto.

## Componentes Principais

1. **Low-Level API**:
   - Oferece métodos para criar visitantes personalizados que podem operar em propriedades de objetos.
   - Exemplo:
     ```csharp
     public class CustomPropertyVisitor : IPropertyVisitor
     {
         public void Visit<TContainer, TValue>(Property<TContainer, TValue> property, ref TContainer container, ref TValue value)
         {
             Debug.Log($"Property Name: {property.Name}, Value: {value}");
         }
     }
     ```

2. **PropertyPath**:
   - Utilizado para acessar e manipular propriedades aninhadas dentro de objetos.
   - Exemplo:
     ```csharp
     var path = new PropertyPath("Transform.Position.x");
     ```

## Uso da Low-Level API

1. **Criação de um Visitante Personalizado**:
   - Implemente a interface `IPropertyVisitor` para criar um visitante personalizado.
   - Exemplo:
     ```csharp
     public class CustomPropertyVisitor : IPropertyVisitor
     {
         public void Visit<TContainer, TValue>(Property<TContainer, TValue> property, ref TContainer container, ref TValue value)
         {
             Debug.Log($"Property Name: {property.Name}, Value: {value}");
         }
     }

     void Start()
     {
         var visitor = new CustomPropertyVisitor();
         Example example = new Example { Value = 5 };
         PropertyContainer.Visit(ref example, visitor);
     }
     ```

2. **Manipulação de Propriedades Aninhadas**:
   - Utilize `PropertyPath` para acessar e modificar propriedades aninhadas.
   - Exemplo:
     ```csharp
     public class CustomPropertyVisitor : IPropertyVisitor
     {
         public void Visit<TContainer, TValue>(Property<TContainer, TValue> property, ref TContainer container, ref TValue value)
         {
             if (property.Name == "x" && typeof(TContainer) == typeof(Vector3))
             {
                 value = (TValue)(object)10f;
             }
         }
     }

     void Start()
     {
         Example example = new Example();
         var visitor = new CustomPropertyVisitor();
         var path = new PropertyPath("Transform.Position.x");
         PropertyContainer.SetValue(ref example, path, 10f);
     }
     ```

## Benefícios do Uso da Low-Level API

1. **Flexibilidade e Controle**:
   - Permite a criação de visitantes altamente personalizados para casos de uso específicos.
   - Oferece controle detalhado sobre como propriedades são acessadas e modificadas.

2. **Independência de Tipo**:
   - Opera sobre objetos de maneira genérica, sem precisar conhecer os tipos específicos em tempo de compilação.
   - Reduz a necessidade de código repetitivo para diferentes tipos de objetos.

3. **Integração Simplificada**:
   - Integra-se facilmente com sistemas de serialização, UI de editores e outras ferramentas.
   - Aumenta a produtividade ao facilitar operações comuns sobre objetos.

## Considerações

1. **Desempenho**:
   - Embora flexível, o uso da API de baixo nível pode introduzir uma pequena sobrecarga em comparação com acesso direto a propriedades.
   - Use com cautela em partes críticas de desempenho do código.

2. **Manutenção**:
   - Mantenha os visitantes atualizados ao modificar os tipos subjacentes para garantir a consistência.
   - Teste rigorosamente para evitar problemas com propriedades não registradas ou mal configuradas.

3. **Segurança de Tipos**:
   - O uso genérico pode levar a erros em tempo de execução se não for cuidadosamente gerenciado.
   - Implemente validações e testes para garantir a robustez do sistema.

## Exemplo Completo de Uso da Low-Level API dos Property Visitors

```csharp
using UnityEngine;
using Unity.Properties;

public class Example
{
    public Transform Transform { get; set; }
}

public class CustomPropertyVisitor : IPropertyVisitor
{
    public void Visit<TContainer, TValue>(Property<TContainer, TValue> property, ref TContainer container, ref TValue value)
    {
        Debug.Log($"Property Name: {property.Name}, Value: {value}");
        if (property.Name == "x" && typeof(TContainer) == typeof(Vector3))
        {
            value = (TValue)(object)10f;
        }
    }
}

public class LowLevelAPIExample : MonoBehaviour
{
    void Start()
    {
        Example example = new Example { Transform = new Transform() };
        var visitor = new CustomPropertyVisitor();
        var path = new PropertyPath("Transform.Position.x");
        
        // Acessando valor
        var value = PropertyContainer.GetValue<float>(ref example, path);
        Debug.Log($"Value: {value}");

        // Modificando valor
        PropertyContainer.SetValue(ref example, path, 10f);
        PropertyContainer.Visit(ref example, visitor);
        Debug.Log($"New Value: {example.Transform.Position.x}");
    }
}
```
