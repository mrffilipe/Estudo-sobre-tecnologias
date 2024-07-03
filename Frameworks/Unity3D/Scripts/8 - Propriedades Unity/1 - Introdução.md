
# Documentação sobre Propriedades no Unity3D

## Introdução

As propriedades no Unity3D são usadas para expor variáveis na Inspector e para controlar o acesso a essas variáveis, permitindo encapsular dados e aplicar lógica adicional ao obter ou definir valores.

## Tipos de Propriedades

1. **Propriedades de Leitura e Escrita**:
   - Permitem tanto a leitura quanto a escrita do valor.
   - Exemplo:
     ```csharp
     public int Health { get; set; }
     ```

2. **Propriedades Somente Leitura**:
   - Permitem apenas a leitura do valor.
   - Exemplo:
     ```csharp
     public int Health { get { return health; } }
     ```

3. **Propriedades Somente Escrita**:
   - Permitem apenas a escrita do valor.
   - Exemplo:
     ```csharp
     public int Health { set { health = value; } }
     ```

## Propriedades com Lógica Adicional

1. **Propriedades com Validação**:
   - Permitem adicionar lógica de validação ao definir um valor.
   - Exemplo:
     ```csharp
     public int Health
     {
         get { return health; }
         set { health = Mathf.Clamp(value, 0, 100); }
     }
     ```

2. **Propriedades Dependentes**:
   - Calculam o valor com base em outras variáveis.
   - Exemplo:
     ```csharp
     public int Health { get { return health; } set { health = Mathf.Clamp(value, 0, maxHealth); } }
     ```

## Expondo Propriedades na Inspector

1. **Propriedades Públicas**:
   - São automaticamente exibidas na Inspector.
   - Exemplo:
     ```csharp
     public int Health { get; set; }
     ```

2. **[SerializeField]**:
   - Exibe campos privados na Inspector mantendo a encapsulação.
   - Exemplo:
     ```csharp
     [SerializeField] private int health;
     public int Health { get { return health; } set { health = value; } }
     ```

## Considerações

1. **Encapsulamento**:
   - Use propriedades para encapsular dados e aplicar lógica adicional.
2. **Desempenho**:
   - Evite lógica complexa em propriedades frequentemente acessadas.
3. **Facilidade de Uso**:
   - Propriedades tornam o código mais legível e fácil de manter.

## Exemplo Completo

```csharp
using UnityEngine;

public class Player : MonoBehaviour
{
    [SerializeField]
    private int health;

    public int Health
    {
        get { return health; }
        set { health = Mathf.Clamp(value, 0, 100); }
    }

    void Start()
    {
        Health = 50;
        Debug.Log("Health: " + Health);
    }
}
```
