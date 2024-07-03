
# Documentação sobre o Uso de DLLs no Unity3D

## Introdução

O Unity3D permite a integração de bibliotecas de link dinâmico (DLLs) para estender as funcionalidades do jogo ou aplicativo. As DLLs podem ser usadas para compartilhar código entre projetos, integrar bibliotecas de terceiros e acessar APIs específicas da plataforma.

## Tipos de DLLs

1. **DLLs Gerenciadas**:
   - Escrito em C# ou outra linguagem .NET.
   - Utilizado para compartilhar código entre diferentes plataformas sem recompilação.

2. **DLLs Nativas**:
   - Escrito em C ou C++.
   - Utilizado para acessar APIs específicas da plataforma e funcionalidades de baixo nível.

## Estrutura de Pastas para DLLs

1. **DLLs Gerenciadas**:
   - Devem ser colocadas na pasta `Assets/Plugins` ou em qualquer outra pasta dentro do projeto.
   - Exemplo de estrutura:
     ```
     Assets/
     ├── Plugins/
     │   └── MyManagedLibrary.dll
     ```

2. **DLLs Nativas**:
   - Devem ser colocadas na pasta `Assets/Plugins` ou em subpastas específicas da plataforma.
   - Exemplo de estrutura:
     ```
     Assets/
     ├── Plugins/
     │   ├── x86/
     │   │   └── myplugin.dll
     │   ├── x86_64/
     │   │   └── myplugin.dll
     │   ├── Android/
     │   │   └── libmyplugin.so
     │   └── iOS/
     │       └── myplugin.a
     ```

## Uso de DLLs no Unity

1. **Importando DLLs Gerenciadas**:
   - Basta referenciar o namespace e usar as classes e métodos fornecidos pela DLL.
   - Exemplo:
     ```csharp
     using MyManagedLibrary;

     public class ManagedLibraryExample : MonoBehaviour
     {
         void Start()
         {
             MyClass myClass = new MyClass();
             myClass.DoSomething();
         }
     }
     ```

2. **Importando DLLs Nativas**:
   - Use a diretiva `DllImport` em C# para chamar funções da DLL nativa.
   - Exemplo:
     ```csharp
     using System.Runtime.InteropServices;
     using UnityEngine;

     public class NativeLibraryExample : MonoBehaviour
     {
         [DllImport("myplugin")]
         private static extern int MyFunction();

         void Start()
         {
             int result = MyFunction();
             Debug.Log("Resultado da função nativa: " + result);
         }
     }
     ```

## Configuração de DLLs no Unity

1. **Configuração de Importação**:
   - Selecione a DLL na janela do Projeto e configure as opções de importação no Inspector.
   - Configure as plataformas de destino e outras opções específicas da DLL.

2. **Definindo Plataformas Específicas**:
   - Marque as plataformas apropriadas na seção `Select platforms for plugin`.

## Benefícios do Uso de DLLs

1. **Reutilização de Código**:
   - Facilita o compartilhamento de bibliotecas de código existentes entre diferentes projetos e plataformas.

2. **Acesso a Funcionalidades de Baixo Nível**:
   - DLLs nativas permitem acessar APIs específicas da plataforma e funcionalidades de baixo nível.

3. **Desempenho Melhorado**:
   - DLLs nativas podem melhorar o desempenho ao permitir a execução de código nativo mais rápido que o código gerenciado.

## Considerações

1. **Compatibilidade de Plataforma**:
   - Certifique-se de que as DLLs sejam compatíveis com todas as plataformas alvo do projeto.
   - Teste as DLLs em todas as plataformas suportadas para garantir a funcionalidade.

2. **Gerenciamento de Dependências**:
   - Mantenha o controle das dependências de DLLs para evitar conflitos e garantir que todas as bibliotecas necessárias estejam presentes.

3. **Segurança**:
   - Verifique a origem das DLLs para garantir que sejam seguras e confiáveis.
   - Evite usar DLLs de fontes desconhecidas ou não confiáveis.

## Exemplo Completo de Configuração de DLL Nativa

```csharp
using System.Runtime.InteropServices;
using UnityEngine;

public class NativeLibraryExample : MonoBehaviour
{
    [DllImport("myplugin")]
    private static extern int MyFunction();

    void Start()
    {
        int result = MyFunction();
        Debug.Log("Resultado da função nativa: " + result);
    }
}
```

