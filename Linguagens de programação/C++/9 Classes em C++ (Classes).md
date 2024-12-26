### Classes em C++ (Classes)

#### Resumo do Conteúdo:
As **classes** em C++ são a base da programação orientada a objetos (OOP). Elas permitem agrupar dados e comportamentos relacionados em uma única estrutura, chamada **objeto**. Uma classe define o molde (ou blueprint) para criar objetos, encapsulando variáveis (atributos) e funções (métodos) que interagem com esses dados.

---

#### Estrutura Básica de uma Classe:

1. **Definição de Classe:**
   - Uma classe é definida usando a palavra-chave `class` ou `struct` (para structs).
   ```cpp
   class Pessoa {
   public:
       std::string nome;
       int idade;

       void apresentar() {
           std::cout << "Olá, meu nome é " << nome << " e tenho " << idade << " anos.\n";
       }
   };
   ```

2. **Acessibilidade:**
   - Classes possuem três níveis de acesso:
     - **Public:** Acessível de fora da classe.
     - **Private:** Acessível apenas dentro da classe.
     - **Protected:** Acessível dentro da classe e de classes derivadas.
   ```cpp
   class Exemplo {
   private:
       int privado; // Acesso restrito
   public:
       int publico; // Acesso liberado
   protected:
       int protegido; // Acesso restrito a derivadas
   };
   ```

3. **Criação de Objetos:**
   ```cpp
   Pessoa p;
   p.nome = "Carlos";
   p.idade = 30;
   p.apresentar();
   ```

---

#### Recursos Avançados de Classes:

1. **Construtores:**
   - Funções especiais chamadas automaticamente ao criar um objeto.
   ```cpp
   class Pessoa {
   public:
       std::string nome;
       int idade;

       Pessoa(const std::string& n, int i) : nome(n), idade(i) {} // Construtor
   };

   Pessoa p("Ana", 25);
   ```

2. **Destrutores:**
   - Funções chamadas automaticamente quando um objeto é destruído.
   ```cpp
   class Recurso {
   public:
       ~Recurso() {
           std::cout << "Recurso liberado\n";
       }
   };
   ```

3. **Membros Estáticos:**
   - Pertencem à classe, não a um objeto específico.
   ```cpp
   class Contador {
   public:
       static int contador;
       Contador() { contador++; }
   };

   int Contador::contador = 0;
   ```

4. **Sobrecarga de Operadores:**
   - Define comportamentos personalizados para operadores.
   ```cpp
   class Numero {
   public:
       int valor;
       Numero(int v) : valor(v) {}
       Numero operator+(const Numero& outro) {
           return Numero(valor + outro.valor);
       }
   };

   Numero n1(10), n2(20);
   Numero n3 = n1 + n2; // Usa o operador sobrecarregado
   ```

5. **Herança:**
   - Permite que uma classe derive de outra, herdando seus membros.
   ```cpp
   class Animal {
   public:
       void som() { std::cout << "Som genérico\n"; }
   };

   class Cachorro : public Animal {
   public:
       void som() { std::cout << "Latido\n"; }
   };

   Cachorro c;
   c.som(); // Saída: Latido
   ```

6. **Polimorfismo:**
   - Classes derivadas podem sobrescrever métodos da classe base.
   ```cpp
   class Animal {
   public:
       virtual void som() { std::cout << "Som genérico\n"; }
   };

   class Gato : public Animal {
   public:
       void som() override { std::cout << "Miau\n"; }
   };

   Animal* a = new Gato();
   a->som(); // Saída: Miau
   ```

---

#### Exemplos Práticos:

1. **Classe Básica:**
   ```cpp
   class Carro {
   public:
       std::string marca;
       int ano;

       void exibir() {
           std::cout << "Marca: " << marca << ", Ano: " << ano << std::endl;
       }
   };

   Carro c;
   c.marca = "Toyota";
   c.ano = 2022;
   c.exibir();
   ```

2. **Herança e Polimorfismo:**
   ```cpp
   class Veiculo {
   public:
       virtual void mover() { std::cout << "Veículo em movimento\n"; }
   };

   class Bicicleta : public Veiculo {
   public:
       void mover() override { std::cout << "Bicicleta pedalando\n"; }
   };

   Veiculo* v = new Bicicleta();
   v->mover(); // Saída: Bicicleta pedalando
   ```

3. **Uso de Construtores e Destrutores:**
   ```cpp
   class Livro {
   public:
       std::string titulo;

       Livro(const std::string& t) : titulo(t) {
           std::cout << "Livro criado: " << titulo << std::endl;
       }

       ~Livro() {
           std::cout << "Livro destruído: " << titulo << std::endl;
       }
   };

   Livro l("C++ Avançado");
   ```

---

#### Boas Práticas para Uso de Classes:

- **Encapsule dados sensíveis:** Use membros privados e métodos de acesso (getters/setters).
- **Prefira inicialização em lista:** Torna o código mais eficiente.
  ```cpp
  Pessoa(const std::string& n, int i) : nome(n), idade(i) {}
  ```

- **Evite copiar objetos grandes:** Use ponteiros ou referências.
- **Utilize `virtual` para métodos polimórficos:** Isso garante que a versão correta será chamada em tempo de execução.

---

#### Referência:
Para mais informações sobre classes em C++, consulte [cppreference: Classes](https://en.cppreference.com/w/cpp/language/classes).