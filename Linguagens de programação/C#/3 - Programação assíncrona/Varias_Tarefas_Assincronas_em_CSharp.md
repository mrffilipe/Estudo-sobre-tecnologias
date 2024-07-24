
# Iniciar Várias Tarefas Assíncronas e Processá-las Conforme Concluem em C#

Iniciar várias tarefas assíncronas e processá-las conforme são concluídas pode melhorar a eficiência e a responsividade das aplicações em C#. Abaixo estão as principais informações e práticas recomendadas conforme apresentadas na documentação:

## Iniciando Múltiplas Tarefas
- **Iniciar Tarefas**: Use o método `Task.Run` ou métodos assíncronos para iniciar várias tarefas em paralelo.
```csharp
Task<string> task1 = Task.Run(() => FetchDataAsync("https://example.com/1"));
Task<string> task2 = Task.Run(() => FetchDataAsync("https://example.com/2"));
Task<string> task3 = Task.Run(() => FetchDataAsync("https://example.com/3"));
```

## Processando Tarefas Conforme Concluem
- **Task.WhenAny**: Processa cada tarefa à medida que ela é concluída.
```csharp
public async Task ProcessTasksAsync()
{
    var tasks = new List<Task<string>> {
        FetchDataAsync("https://example.com/1"),
        FetchDataAsync("https://example.com/2"),
        FetchDataAsync("https://example.com/3")
    };

    while (tasks.Any())
    {
        Task<string> completedTask = await Task.WhenAny(tasks);
        tasks.Remove(completedTask);
        
        string result = await completedTask;
        Console.WriteLine(result);
    }
}
```

## Usando Task.WhenAll
- **Task.WhenAll**: Espera todas as tarefas serem concluídas.
```csharp
public async Task ProcessAllTasksAsync()
{
    var tasks = new List<Task<string>> {
        FetchDataAsync("https://example.com/1"),
        FetchDataAsync("https://example.com/2"),
        FetchDataAsync("https://example.com/3")
    };

    string[] results = await Task.WhenAll(tasks);
    foreach (var result in results)
    {
        Console.WriteLine(result);
    }
}
```

## Tratamento de Exceções
- **Try-Catch**: Envolva a chamada `await` em um bloco `try-catch` para tratar exceções.
```csharp
public async Task ProcessTasksWithExceptionHandlingAsync()
{
    var tasks = new List<Task<string>> {
        FetchDataAsync("https://example.com/1"),
        FetchDataAsync("https://example.com/2"),
        FetchDataAsync("https://example.com/3")
    };

    while (tasks.Any())
    {
        Task<string> completedTask = await Task.WhenAny(tasks);
        tasks.Remove(completedTask);

        try
        {
            string result = await completedTask;
            Console.WriteLine(result);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Task failed: {ex.Message}");
        }
    }
}
```

## Observações Importantes
- **Performance**: Processar tarefas conforme elas são concluídas pode melhorar a performance em comparação a esperar todas as tarefas terminarem.
- **Gerenciamento de Recursos**: Remova tarefas da lista à medida que são concluídas para evitar a repetição de processamento.

## Dicas de Boas Práticas
- **Use Task.WhenAny para Processamento Imediato**: Prefira `Task.WhenAny` para começar a processar resultados assim que uma tarefa é concluída.
- **Use Task.WhenAll para Aguardar Todas as Tarefas**: Utilize `Task.WhenAll` quando for necessário aguardar a conclusão de todas as tarefas.
- **Tratamento Adequado de Exceções**: Sempre trate exceções para evitar que erros em uma tarefa afetem o processamento das demais.
