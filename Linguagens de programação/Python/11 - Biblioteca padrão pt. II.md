
# Biblioteca Padrão — Parte II

## Introdução

A biblioteca padrão do Python é extensa e cobre uma ampla gama de funcionalidades. Além das funcionalidades básicas, a biblioteca padrão oferece módulos para suporte a testes, depuração, introspecção, processamento de texto, e muito mais.

## Principais Informações

1. **Opções de Comando**
   - O módulo `argparse` facilita a escrita de programas que aceitam argumentos de linha de comando.
   - Permite a definição de argumentos obrigatórios e opcionais, além de gerar automaticamente mensagens de ajuda e uso.

    ```python
    import argparse

    parser = argparse.ArgumentParser(description='Exemplo com argparse')
    parser.add_argument('echo', help='Texto para ecoar')
    args = parser.parse_args()
    print(args.echo)
    ```

2. **Processamento de Padrões e Arquivos**
   - O módulo `glob` fornece uma maneira de usar curingas para buscar arquivos e diretórios.
   - O módulo `fnmatch` oferece suporte para a correspondência de padrões de nomes de arquivos.

    ```python
    import glob

    arquivos = glob.glob('*.txt')
    print(arquivos)
    ```

3. **Acesso a Arquivos e Diretórios**
   - O módulo `shutil` fornece funções para operações de alto nível em arquivos e coleções de arquivos.
   - Permite copiar, mover, remover arquivos e diretórios, entre outras operações.

    ```python
    import shutil

    shutil.copy('origem.txt', 'destino.txt')
    shutil.move('arquivo.txt', 'novo_diretorio/')
    ```

4. **Gerenciamento de Processos**
   - O módulo `subprocess` permite criar novos processos, conectar-se a seus canais de entrada/saída e obter seus códigos de retorno.
   - É uma substituição mais poderosa para os módulos `os.system` e `os.spawn*`.

    ```python
    import subprocess

    resultado = subprocess.run(['ls', '-l'], capture_output=True, text=True)
    print(resultado.stdout)
    ```

5. **Verificação e Teste**
   - O módulo `unittest` fornece uma estrutura para a criação de testes automatizados.
   - Permite agrupar testes, verificar resultados esperados e relatar falhas de maneira estruturada.

    ```python
    import unittest

    class TesteSimples(unittest.TestCase):
        def test_soma(self):
            self.assertEqual(soma(1, 2), 3)

    if __name__ == '__main__':
        unittest.main()
    ```

6. **Depuração e Perfis**
   - O módulo `pdb` é o depurador interativo do Python.
   - O módulo `cProfile` fornece um profiler para medir o tempo de execução de diferentes partes do código.

    ```python
    import pdb

    def soma(a, b):
        pdb.set_trace()
        return a + b

    resultado = soma(1, 2)
    ```

## Observações Importantes

- **Facilidade de Uso**: Muitos módulos da biblioteca padrão são projetados para serem fáceis de usar e integrar em seus programas.
- **Suporte a Testes e Depuração**: A biblioteca padrão inclui ferramentas poderosas para ajudar no desenvolvimento, teste e depuração de código Python.

## Dicas de Boas Práticas

- **Aproveite as Ferramentas de Teste**: Use o `unittest` ou outras bibliotecas de teste para garantir que seu código funcione conforme esperado.
- **Use Depuração e Perfis**: Utilize `pdb` e `cProfile` para identificar e corrigir bugs e otimizar o desempenho do seu código.
- **Explore e Experimente**: A biblioteca padrão do Python é extensa. Explore os módulos disponíveis para encontrar soluções prontas para os desafios de programação que você enfrenta.
