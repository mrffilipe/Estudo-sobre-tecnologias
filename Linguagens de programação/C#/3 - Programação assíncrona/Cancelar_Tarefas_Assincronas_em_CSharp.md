
# Cancelar uma Tarefa Assíncrona ou uma Lista de Tarefas em C#

O cancelamento de tarefas assíncronas em C# permite que você encerre operações que não são mais necessárias, liberando recursos e melhorando a eficiência da aplicação. Abaixo estão as principais informações e práticas recomendadas sobre como cancelar uma tarefa assíncrona ou uma lista de tarefas conforme a documentação.

## Uso de CancellationToken
- **CancellationTokenSource**: Crie uma instância de `CancellationTokenSource` para obter um `CancellationToken`.
```csharp
var cts = new CancellationTokenSource();
CancellationToken token = cts.Token;
```

- **Passando o Token**: Passe o `CancellationToken` para métodos que suportam cancelamento.
```csharp
public async Task PerformTaskAsync(CancellationToken token)
{
    for (int i = 0; i < 10; i++)
    {
        token.ThrowIfCancellationRequested();
        await Task.Delay(1000);
    }
}
```

- **Cancelando a Tarefa**: Chame `Cancel` no `CancellationTokenSource` para solicitar o cancelamento.
```csharp
cts.Cancel();
```

## Exemplo de Cancelamento de Tarefa
- **Exemplo Completo**:
```csharp
public async Task RunAsyncTask()
{
    var cts = new CancellationTokenSource();
    CancellationToken token = cts.Token;

    var task = PerformTaskAsync(token);

    // Cancelar a tarefa após 3 segundos
    cts.CancelAfter(3000);

    try
    {
        await task;
    }
    catch (OperationCanceledException)
    {
        Console.WriteLine("Task was canceled.");
    }
}
```

## Cancelamento de Múltiplas Tarefas
- **Cancelando uma Lista de Tarefas**: Use o mesmo `CancellationToken` para cancelar várias tarefas simultaneamente.
```csharp
public async Task PerformMultipleTasksAsync()
{
    var cts = new CancellationTokenSource();
    CancellationToken token = cts.Token;

    var tasks = new List<Task>
    {
        Task.Run(() => PerformTaskAsync(token)),
        Task.Run(() => PerformTaskAsync(token)),
        Task.Run(() => PerformTaskAsync(token))
    };

    cts.CancelAfter(3000);

    try
    {
        await Task.WhenAll(tasks);
    }
    catch (OperationCanceledException)
    {
        Console.WriteLine("One or more tasks were canceled.");
    }
}
```

## Observações Importantes
- **ThrowIfCancellationRequested**: Sempre verifique `token.ThrowIfCancellationRequested()` em pontos críticos do método para permitir o cancelamento.
- **OperationCanceledException**: Capturar `OperationCanceledException` para lidar com tarefas canceladas corretamente.

## Dicas de Boas Práticas
- **Cancelamento Antecipado**: Solicite o cancelamento o mais cedo possível para liberar recursos.
- **Tratamento de Exceções**: Trate `OperationCanceledException` para garantir que o cancelamento seja gerenciado de forma adequada.
- **Uso de CancellationToken**: Utilize `CancellationToken` em todos os métodos assíncronos que possam ser cancelados para manter a consistência.
