
# Formatação de Saída no Docker CLI

## Visão Geral
O Docker CLI permite personalizar a formatação da saída dos comandos que listam objetos, como containers, imagens, volumes, e redes. Isso é útil para exibir exatamente as informações de que você precisa em um formato legível ou em um layout específico para integração com outras ferramentas.

## 1. Formatos de Saída Suportados

### Formato Padrão
- Por padrão, os comandos do Docker CLI retornam a saída em um formato tabular, apresentando informações em colunas bem definidas.

### Formatos Personalizados
- Você pode personalizar a saída usando os seguintes formatos:
  - `table`: Exibe a saída em formato tabular (padrão).
  - `json`: Exibe a saída em formato JSON, adequado para processamento por outras ferramentas.
  - `template`: Permite especificar um modelo (template) para exibir os campos desejados.

## 2. Usando o Parâmetro `--format`

### Sintaxe Básica
- O parâmetro `--format` pode ser usado com vários comandos Docker para definir o formato da saída.
- Exemplo:

```bash
docker ps --format "{{.ID}}: {{.Image}}"
```

## 3. Campos Comuns para Formatação

### Exemplos de Campos Usados em Templates
- `{{.ID}}`: ID do container ou imagem.
- `{{.Image}}`: Nome da imagem.
- `{{.Status}}`: Status do container.
- `{{.Names}}`: Nome do container.
- `{{.Size}}`: Tamanho da imagem ou volume.

### Exemplo de Uso
- Para exibir apenas os IDs e nomes dos containers em execução:

```bash
docker ps --format "{{.ID}}: {{.Names}}"
```

## 4. Usando JSON para Formatação

### Formato JSON
- Você pode usar o formato JSON para integrar a saída do Docker CLI com outras ferramentas ou scripts.
- Exemplo:

```bash
docker images --format "{{json .}}"
```

## 5. Personalizando a Saída com Templates

### Uso Avançado de Templates
- Os templates no Docker CLI permitem o uso de lógica condicional e loops para criar saídas mais complexas.
- Exemplo com lógica condicional:

```bash
docker ps --format "{{if eq .Status "running"}}RUNNING: {{.ID}}: {{.Names}}{{end}}"
```

- Este comando exibe uma mensagem personalizada para containers que estão em execução.

## 6. Considerações de Boas Práticas

### Clareza e Simplicidade
- Ao personalizar a formatação, mantenha a saída clara e legível, focando nos campos mais relevantes para suas necessidades.

### Integração com Scripts
- Use formatação JSON ou templates personalizados para integrar o Docker CLI com scripts e outras ferramentas de automação.

### Documentação e Reusabilidade
- Documente os templates personalizados e reutilize-os em diferentes scripts e ambientes para manter a consistência.

## 7. Casos de Uso Comuns

### Relatórios Personalizados
- Use formatação personalizada para criar relatórios específicos, como uma lista de containers com suas respectivas imagens e status.

### Automação de Tarefas
- Integre saídas formatadas do Docker CLI com scripts de automação, facilitando tarefas como monitoramento e gerenciamento de recursos.

### Análise e Auditoria
- Exporte dados em formato JSON para análise em ferramentas externas, ajudando em auditorias e conformidade.

## Dicas de Boas Práticas
- Mantenha a saída das formatações clara e objetiva, focando nas informações mais relevantes.
- Use templates e JSON para integrar a saída do Docker CLI com outras ferramentas e scripts de automação.
- Documente e reutilize os templates personalizados para garantir consistência e eficiência em diferentes ambientes e projetos.

