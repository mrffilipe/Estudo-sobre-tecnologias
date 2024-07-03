
# Documentação sobre UnityWebRequest Low-Level API no Unity3D

## Introdução

A Low-Level API do `UnityWebRequest` no Unity3D proporciona um controle detalhado sobre as requisições HTTP, permitindo uma maior personalização e flexibilidade. Esta API é ideal para desenvolvedores que precisam de funcionalidades avançadas ou específicas em suas operações de rede.

## Componentes Principais

1. **UnityWebRequest**:
   - A classe principal para fazer requisições HTTP e recuperar dados.
   - Exemplo:
     ```csharp
     UnityWebRequest request = new UnityWebRequest("http://example.com", "GET");
     yield return request.SendWebRequest();
     ```

2. **DownloadHandler**:
   - Classe base para processar dados recebidos da web.
   - Pode ser estendida para criar manipuladores personalizados.
   - Exemplo:
     ```csharp
     request.downloadHandler = new DownloadHandlerBuffer();
     ```

3. **UploadHandler**:
   - Classe base para enviar dados para a web.
   - Pode ser estendida para criar manipuladores personalizados.
   - Exemplo:
     ```csharp
     byte[] data = System.Text.Encoding.UTF8.GetBytes("My raw data");
     request.uploadHandler = new UploadHandlerRaw(data);
     ```

4. **CertificateHandler**:
   - Utilizado para validar certificados SSL.
   - Pode ser estendida para criar validadores personalizados.
   - Exemplo:
     ```csharp
     public class AcceptAllCertificates : CertificateHandler
     {
         protected override bool ValidateCertificate(byte[] certificateData)
         {
             return true;
         }
     }
     ```

## Uso da Low-Level API

1. **Configuração de Requisição Personalizada**:
   - Configure uma requisição HTTP personalizada com métodos e cabeçalhos específicos.
   - Exemplo:
     ```csharp
     UnityWebRequest request = new UnityWebRequest("http://example.com", "POST");
     request.uploadHandler = new UploadHandlerRaw(data);
     request.downloadHandler = new DownloadHandlerBuffer();
     request.SetRequestHeader("Content-Type", "application/json");
     yield return request.SendWebRequest();

     if (request.result == UnityWebRequest.Result.Success)
     {
         Debug.Log(request.downloadHandler.text);
     }
     else
     {
         Debug.LogError(request.error);
     }
     ```

2. **Manipulação de Certificados**:
   - Utilize `CertificateHandler` para validar ou ignorar certificados SSL conforme necessário.
   - Exemplo:
     ```csharp
     request.certificateHandler = new AcceptAllCertificates();
     ```

3. **Implementação de Handlers Personalizados**:
   - Crie classes derivadas de `DownloadHandler` ou `UploadHandler` para processar dados de forma personalizada.
   - Exemplo:
     ```csharp
     public class CustomDownloadHandler : DownloadHandlerScript
     {
         protected override bool ReceiveData(byte[] data, int dataLength)
         {
             // Processar dados recebidos
             return true;
         }
     }

     UnityWebRequest request = new UnityWebRequest("http://example.com", "GET");
     request.downloadHandler = new CustomDownloadHandler();
     yield return request.SendWebRequest();
     ```

## Benefícios do Uso da Low-Level API

1. **Flexibilidade**:
   - Permite criar requisições HTTP altamente personalizadas.
   - Ideal para casos de uso avançados e específicos.

2. **Controle Detalhado**:
   - Oferece controle total sobre a configuração e manipulação de requisições e respostas HTTP.
   - Permite a criação de manipuladores personalizados para upload e download de dados.

3. **Segurança**:
   - Suporte a validação de certificados SSL, proporcionando segurança nas operações de rede.
   - Permite implementar validadores de certificados personalizados conforme necessário.

## Considerações

1. **Complexidade**:
   - A Low-Level API é mais complexa e exige um entendimento mais profundo das operações de rede.
   - Recomendada para desenvolvedores experientes ou para necessidades específicas.

2. **Desempenho**:
   - Embora ofereça maior controle, o uso inadequado pode impactar negativamente o desempenho.
   - Certifique-se de otimizar manipulações de dados e configurações de rede.

3. **Manutenção de Código**:
   - Código que utiliza a Low-Level API pode ser mais difícil de manter.
   - Documente e comente adequadamente para facilitar futuras manutenções.

## Exemplo Completo de Uso da Low-Level API do UnityWebRequest

```csharp
using UnityEngine;
using UnityEngine.Networking;
using System.Collections;

public class LowLevelAPIExample : MonoBehaviour
{
    void Start()
    {
        StartCoroutine(CustomRequest("http://example.com"));
    }

    IEnumerator CustomRequest(string uri)
    {
        byte[] data = System.Text.Encoding.UTF8.GetBytes("My raw data");
        UnityWebRequest request = new UnityWebRequest(uri, "POST");
        request.uploadHandler = new UploadHandlerRaw(data);
        request.downloadHandler = new DownloadHandlerBuffer();
        request.SetRequestHeader("Content-Type", "application/json");
        request.certificateHandler = new AcceptAllCertificates();
        yield return request.SendWebRequest();

        if (request.result == UnityWebRequest.Result.Success)
        {
            Debug.Log(request.downloadHandler.text);
        }
        else
        {
            Debug.LogError(request.error);
        }

        request.Dispose();
    }
}

public class AcceptAllCertificates : CertificateHandler
{
    protected override bool ValidateCertificate(byte[] certificateData)
    {
        return true;
    }
}
```
