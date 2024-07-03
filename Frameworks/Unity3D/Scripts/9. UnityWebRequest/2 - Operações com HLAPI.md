
# Documentação sobre UnityWebRequest High-Level API no Unity3D

## Introdução

A High-Level API do `UnityWebRequest` no Unity3D simplifica o uso de operações de rede, proporcionando uma interface mais fácil para tarefas comuns como downloads e uploads de arquivos, e comunicação com servidores. Esta API é projetada para ser mais acessível e menos verbosa do que a API de baixo nível.

## Componentes Principais

1. **UnityWebRequest**:
   - A classe principal para fazer requisições HTTP.
   - Exemplo:
     ```csharp
     UnityWebRequest request = UnityWebRequest.Get("http://example.com");
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

2. **DownloadHandler**:
   - Classe para processar dados recebidos da web.
   - Tipos comuns incluem `DownloadHandlerBuffer` e `DownloadHandlerFile`.
   - Exemplo:
     ```csharp
     DownloadHandler downloadHandler = new DownloadHandlerBuffer();
     ```

3. **UploadHandler**:
   - Classe para enviar dados para a web.
   - Tipos comuns incluem `UploadHandlerRaw`.
   - Exemplo:
     ```csharp
     UploadHandler uploadHandler = new UploadHandlerRaw(myData);
     ```

## Uso da High-Level API

1. **Requisição GET**:
   - Para recuperar dados de um servidor.
   - Exemplo:
     ```csharp
     UnityWebRequest request = UnityWebRequest.Get("http://example.com");
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

2. **Requisição POST**:
   - Para enviar dados para um servidor.
   - Exemplo:
     ```csharp
     WWWForm form = new WWWForm();
     form.AddField("name", "value");

     UnityWebRequest request = UnityWebRequest.Post("http://example.com", form);
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

3. **Upload de Arquivo**:
   - Para enviar arquivos usando uma requisição POST.
   - Exemplo:
     ```csharp
     byte[] fileData = System.IO.File.ReadAllBytes("path/to/file");
     UnityWebRequest request = new UnityWebRequest("http://example.com/upload", "POST");
     request.uploadHandler = new UploadHandlerRaw(fileData);
     request.downloadHandler = new DownloadHandlerBuffer();
     request.SetRequestHeader("Content-Type", "application/octet-stream");
     yield return request.SendWebRequest();

     if (request.result == UnityWebRequest.Result.Success)
     {
         Debug.Log("Upload complete!");
     }
     else
     {
         Debug.LogError(request.error);
     }
     ```

4. **Download de Arquivo**:
   - Para baixar arquivos da web.
   - Exemplo:
     ```csharp
     UnityWebRequest request = UnityWebRequest.Get("http://example.com/file");
     request.downloadHandler = new DownloadHandlerFile("path/to/save/file");
     yield return request.SendWebRequest();

     if (request.result == UnityWebRequest.Result.Success)
     {
         Debug.Log("Download complete!");
     }
     else
     {
         Debug.LogError(request.error);
     }
     ```

## Benefícios do Uso da High-Level API

1. **Simplicidade**:
   - Proporciona uma interface mais simples e menos verbosa para operações de rede comuns.
   - Facilita o desenvolvimento rápido de funcionalidades de rede.

2. **Flexibilidade**:
   - Suporta diversos métodos HTTP e pode ser personalizado para diferentes tipos de requisições e respostas.
   - Permite manipulação avançada de headers e conteúdo.

3. **Desempenho**:
   - Mais eficiente que o antigo `WWW`.
   - Suporta operações assíncronas, melhorando a performance e a responsividade da aplicação.

## Considerações

1. **Tratamento de Erros**:
   - Sempre verifique `request.result` para capturar e tratar erros de rede.
   - Exemplo:
     ```csharp
     if (request.result != UnityWebRequest.Result.Success)
     {
         Debug.LogError(request.error);
     }
     ```

2. **Certificados SSL**:
   - Utilize `CertificateHandler` para validar certificados SSL conforme necessário.
   - Evite ignorar certificados SSL em produção.

3. **Limpeza de Recursos**:
   - Utilize `Dispose` para liberar recursos após a conclusão das requisições.
   - Exemplo:
     ```csharp
     request.Dispose();
     ```

## Exemplo Completo de Uso da High-Level API do UnityWebRequest

```csharp
using UnityEngine;
using UnityEngine.Networking;
using System.Collections;

public class WebRequestExample : MonoBehaviour
{
    void Start()
    {
        StartCoroutine(GetRequest("http://example.com"));
    }

    IEnumerator GetRequest(string uri)
    {
        UnityWebRequest request = UnityWebRequest.Get(uri);
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
```
