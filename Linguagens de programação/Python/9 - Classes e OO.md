
# Classes

## Introdução

Classes são a fundação da programação orientada a objetos (POO) em Python. Elas permitem agrupar dados e comportamentos relacionados em uma única estrutura, facilitando a criação de objetos que representam entidades do mundo real ou conceitos abstratos.

## Principais Informações

1. **Definindo uma Classe**
   - Use a palavra-chave `class` para definir uma classe.
   - O método `__init__` é um inicializador que define o estado inicial dos objetos da classe.

    ```python
    class Animal:
        def __init__(self, nome):
            self.nome = nome

        def falar(self):
            pass
    ```

2. **Criando Instâncias**
   - Instâncias são criadas chamando a classe como se fosse uma função.
   - Cada instância pode ter atributos diferentes.

    ```python
    meu_animal = Animal("Rex")
    print(meu_animal.nome)
    ```

3. **Atributos de Instância e Classe**
   - Atributos de instância são definidos no método `__init__` e são específicos para cada instância.
   - Atributos de classe são compartilhados por todas as instâncias da classe.

    ```python
    class Animal:
        tipo = "Mamífero"  # Atributo de classe

        def __init__(self, nome):
            self.nome = nome  # Atributo de instância

    print(Animal.tipo)
    ```

4. **Métodos**
   - Métodos são funções definidas dentro de uma classe.
   - O primeiro parâmetro de um método é sempre `self`, que referencia a instância que chamou o método.

    ```python
    class Animal:
        def __init__(self, nome):
            self.nome = nome

        def falar(self):
            return f"{self.nome} faz algum som"

    meu_animal = Animal("Rex")
    print(meu_animal.falar())
    ```

5. **Herança**
   - Herança permite criar novas classes baseadas em classes existentes.
   - A classe derivada herda os atributos e métodos da classe base.

    ```python
    class Cachorro(Animal):
        def falar(self):
            return f"{self.nome} diz Au Au"

    meu_cachorro = Cachorro("Rex")
    print(meu_cachorro.falar())
    ```

6. **Sobrescrita de Métodos**
   - Métodos da classe base podem ser sobrescritos na classe derivada.
   - Use `super()` para chamar métodos da classe base.

    ```python
    class Cachorro(Animal):
        def falar(self):
            return f"{self.nome} diz Au Au"

    meu_cachorro = Cachorro("Rex")
    print(meu_cachorro.falar())
    ```

7. **Encapsulamento**
   - Atributos e métodos podem ser tornados privados prefixando-os com dois underlines (`__`).
   - Acessíveis apenas dentro da própria classe.

    ```python
    class Animal:
        def __init__(self, nome):
            self.__nome = nome

        def get_nome(self):
            return self.__nome

    meu_animal = Animal("Rex")
    print(meu_animal.get_nome())
    ```

## Observações Importantes

- **POO em Python**: A POO em Python é flexível e permite múltiplas heranças, facilitando a reutilização de código.
- **Métodos Especiais**: Métodos como `__init__`, `__str__` e `__repr__` são chamados de métodos especiais ou dunder methods (double underscore). Eles permitem personalizar o comportamento das classes.

## Dicas de Boas Práticas

- **Use Herança com Moderação**: Utilize herança apenas quando fizer sentido lógico. Prefira composição em muitos casos.
- **Documente suas Classes**: Adicione docstrings para explicar o propósito das classes e métodos.
- **Organize o Código**: Mantenha as classes e métodos organizados e bem estruturados para facilitar a manutenção e leitura do código.
