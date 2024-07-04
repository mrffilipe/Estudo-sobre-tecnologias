
# Entrada e Saída

## Introdução

Entrada e saída (I/O) são operações fundamentais em qualquer linguagem de programação. Em Python, a leitura de dados do usuário e a escrita de dados na tela ou em arquivos são realizadas de maneira simples e intuitiva.

## Principais Informações

1. **Saída para a Tela**
   - Use a função `print()` para exibir dados na tela.
   - Você pode formatar strings usando f-strings, o método `str.format()`, ou o operador `%`.

    ```python
    print("Olá, mundo!")
    nome = "Marcos"
    print(f"Olá, {nome}!")
    print("Olá, {}!".format(nome))
    ```

2. **Entrada do Usuário**
   - Use a função `input()` para ler dados do usuário.
   - A função `input()` retorna sempre uma string; use a conversão de tipos se necessário.

    ```python
    nome = input("Digite seu nome: ")
    idade = int(input("Digite sua idade: "))
    print(f"Nome: {nome}, Idade: {idade}")
    ```

3. **Leitura e Escrita de Arquivos**
   - Use a função `open()` para abrir um arquivo. O modo de abertura pode ser leitura (`'r'`), escrita (`'w'`), ou append (`'a'`).
   - Sempre feche o arquivo após a operação com `close()` ou utilize o gerenciador de contexto `with` para garantir o fechamento automático.

    ```python
    # Escrita em arquivo
    with open("arquivo.txt", "w") as arquivo:
        arquivo.write("Olá, mundo!")

    # Leitura de arquivo
    with open("arquivo.txt", "r") as arquivo:
        conteudo = arquivo.read()
        print(conteudo)
    ```

4. **Leitura Linha a Linha**
   - Use `readline()` para ler uma linha de cada vez ou itere sobre o objeto arquivo para ler linha por linha.

    ```python
    with open("arquivo.txt", "r") as arquivo:
        for linha in arquivo:
            print(linha, end="")
    ```

5. **Métodos de Arquivo**
   - `read(size)`: Lê `size` bytes do arquivo.
   - `readline()`: Lê uma linha do arquivo.
   - `readlines()`: Lê todas as linhas do arquivo e as retorna como uma lista.
   - `write(s)`: Escreve a string `s` no arquivo.
   - `writelines(lines)`: Escreve uma lista de strings no arquivo.

    ```python
    with open("arquivo.txt", "r") as arquivo:
        linhas = arquivo.readlines()
        for linha em linhas:
            print(linha, end="")
    ```

## Observações Importantes

- **Encerramento de Arquivos**: Sempre feche os arquivos para liberar recursos do sistema. O uso do gerenciador de contexto `with` é recomendado para garantir o fechamento automático.
- **Modos de Abertura**: Escolha o modo correto (`'r'`, `'w'`, `'a'`, `'b'`) de acordo com a operação desejada e o tipo de arquivo (texto ou binário).

## Dicas de Boas Práticas

- **Use `with` para Gerenciamento de Arquivos**: Utilize o gerenciador de contexto `with` ao trabalhar com arquivos para garantir o fechamento correto dos mesmos.
- **Valide Entradas do Usuário**: Sempre valide e trate as entradas do usuário para evitar erros e comportamentos inesperados.
- **Formatação de Strings**: Prefira f-strings para formatação de strings por serem mais legíveis e eficientes.
