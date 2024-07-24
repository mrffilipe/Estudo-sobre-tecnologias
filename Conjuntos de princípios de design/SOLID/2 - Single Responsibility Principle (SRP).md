
# 1. Single Responsibility Principle (SRP)

## 1.1 O que é responsabilidade única

O Princípio da Responsabilidade Única (Single Responsibility Principle - SRP) afirma que uma classe deve ter uma, e somente uma, razão para mudar. Isso significa que cada classe deve ser responsável por uma única funcionalidade ou tarefa no sistema. Uma classe que segue o SRP tem uma responsabilidade clara e bem definida, facilitando a manutenção e a evolução do software.

## 1.2 Vantagens do SRP

- **Facilidade de manutenção**: Classes com responsabilidades únicas são mais fáceis de entender e modificar, reduzindo a complexidade do código.
- **Reutilização de código**: Componentes com responsabilidades bem definidas são mais fáceis de reutilizar em diferentes partes do sistema ou em projetos futuros.
- **Testabilidade**: Classes focadas em uma única responsabilidade são mais fáceis de testar de forma isolada, melhorando a qualidade do software.
- **Menor acoplamento**: Seguir o SRP reduz o acoplamento entre classes, permitindo que mudanças em uma classe tenham menos impacto sobre outras classes.

## 1.3 Identificação de múltiplas responsabilidades em uma classe

Para identificar múltiplas responsabilidades em uma classe, considere os seguintes pontos:

- **Tamanho da classe**: Classes muito grandes geralmente indicam a presença de múltiplas responsabilidades.
- **Métodos e atributos**: Verifique se os métodos e atributos da classe estão relacionados a diferentes tipos de funcionalidades.
- **Motivos para mudança**: Considere quantas razões diferentes existem para alterar a classe. Cada razão adicional pode indicar uma responsabilidade distinta.

## 1.4 Refatoração para SRP

Refatorar uma classe para seguir o SRP envolve dividir a classe em várias classes menores, cada uma com uma responsabilidade única. Isso pode incluir a criação de novas classes ou a extração de métodos e atributos para outras classes.

## Exemplo em C#

### Antes da refatoração:
```csharp
public class UsuarioService
{
    public void AdicionarUsuario(string nome, string email)
    {
        // Lógica para adicionar usuário
    }

    public void EnviarEmailBoasVindas(string email)
    {
        // Lógica para enviar email de boas-vindas
    }

    public void SalvarLog(string mensagem)
    {
        // Lógica para salvar log
    }
}
```

### Após a refatoração:
```csharp
public class UsuarioService
{
    private readonly IEmailService _emailService;
    private readonly ILogService _logService;

    public UsuarioService(IEmailService emailService, ILogService logService)
    {
        _emailService = emailService;
        _logService = logService;
    }

    public void AdicionarUsuario(string nome, string email)
    {
        // Lógica para adicionar usuário
        _emailService.EnviarEmailBoasVindas(email);
        _logService.SalvarLog("Usuário adicionado: " + nome);
    }
}

public interface IEmailService
{
    void EnviarEmailBoasVindas(string email);
}

public class EmailService : IEmailService
{
    public void EnviarEmailBoasVindas(string email)
    {
        // Lógica para enviar email de boas-vindas
    }
}

public interface ILogService
{
    void SalvarLog(string mensagem);
}

public class LogService : ILogService
{
    public void SalvarLog(string mensagem)
    {
        // Lógica para salvar log
    }
}
```

Neste exemplo, a classe `UsuarioService` foi refatorada para seguir o SRP. As responsabilidades de enviar e-mails e salvar logs foram extraídas para as classes `EmailService` e `LogService`, respectivamente, cada uma com uma responsabilidade única.
