
# Cancelar Tarefas Assíncronas após um Período de Tempo em C#

Cancelar tarefas assíncronas após um período de tempo pode ser útil para evitar que operações demorem mais do que o esperado, liberando recursos e melhorando a eficiência da aplicação. Abaixo estão as principais informações e práticas recomendadas conforme apresentadas na documentação.

## Uso de CancellationTokenSource com Timeout
- **CancellationTokenSource**: Use `CancellationTokenSource` com o método `CancelAfter` para definir um tempo limite.
```csharp
var cts = new CancellationTokenSource();
cts.CancelAfter(TimeSpan.FromSeconds(5)); // Cancela após 5 segundos
CancellationToken token = cts.Token;
```

## Implementação de Cancelamento com Timeout
- **Exemplo Completo**: Um método que realiza uma tarefa com cancelamento após um tempo limite.
```csharp
public async Task PerformTaskWithTimeoutAsync(CancellationToken token)
{
    for (int i = 0; i < 10; i++)
    {
        token.ThrowIfCancellationRequested();
        await Task.Delay(1000); // Simula uma operação de 1 segundo
    }
}

public async Task RunTaskWithTimeoutAsync()
{
    var cts = new CancellationTokenSource();
    cts.CancelAfter(TimeSpan.FromSeconds(5)); // Define um tempo limite de 5 segundos
    CancellationToken token = cts.Token;

    try
    {
        await PerformTaskWithTimeoutAsync(token);
    }
    catch (OperationCanceledException)
    {
        Console.WriteLine("Task was canceled due to timeout.");
    }
}
```

## Cancelamento de Múltiplas Tarefas com Timeout
- **Cancelamento de Lista de Tarefas**: Usar o mesmo `CancellationToken` para cancelar várias tarefas simultaneamente após um período de tempo.
```csharp
public async Task PerformMultipleTasksWithTimeoutAsync()
{
    var cts = new CancellationTokenSource();
    cts.CancelAfter(TimeSpan.FromSeconds(5)); // Cancela após 5 segundos
    CancellationToken token = cts.Token;

    var tasks = new List<Task>
    {
        Task.Run(() => PerformTaskWithTimeoutAsync(token)),
        Task.Run(() => PerformTaskWithTimeoutAsync(token)),
        Task.Run(() => PerformTaskWithTimeoutAsync(token))
    };

    try
    {
        await Task.WhenAll(tasks);
    }
    catch (OperationCanceledException)
    {
        Console.WriteLine("One or more tasks were canceled due to timeout.");
    }
}
```

## Observações Importantes
- **ThrowIfCancellationRequested**: Sempre verifique `token.ThrowIfCancellationRequested()` em pontos críticos do método para permitir o cancelamento.
- **OperationCanceledException**: Capture `OperationCanceledException` para tratar corretamente tarefas canceladas.

## Dicas de Boas Práticas
- **Cancelamento Antecipado**: Defina o tempo limite de cancelamento o mais cedo possível para evitar operações longas desnecessárias.
- **Tratamento de Exceções**: Capture e trate `OperationCanceledException` para garantir que o cancelamento seja gerenciado adequadamente.
- **Uso de CancellationToken**: Utilize `CancellationToken` em todos os métodos assíncronos que possam ser cancelados para manter a consistência.
