### Templates em C++ (Templates)

#### Resumo do Conteúdo:
Os **templates** em C++ permitem a criação de **código genérico**, ou seja, funções e classes que podem operar com diferentes tipos de dados sem necessidade de reescrever o código. Essa funcionalidade é essencial para reutilização, flexibilidade e desempenho.

Templates são amplamente usados para implementar estruturas e algoritmos genéricos, como `std::vector` e `std::sort`.

---

#### Tipos de Templates:

1. **Templates de Função:**
   - Definem funções genéricas que podem operar com diferentes tipos.
   ```cpp
   template <typename T>
   T maior(T a, T b) {
       return (a > b) ? a : b;
   }

   int main() {
       std::cout << maior(10, 20) << std::endl; // Usa int
       std::cout << maior(3.14, 2.71) << std::endl; // Usa double
   }
   ```

2. **Templates de Classe:**
   - Definem classes genéricas que aceitam diferentes tipos.
   ```cpp
   template <typename T>
   class Caixa {
   private:
       T valor;
   public:
       Caixa(T v) : valor(v) {}
       T obter() { return valor; }
   };

   int main() {
       Caixa<int> c1(10);
       Caixa<std::string> c2("Olá");

       std::cout << c1.obter() << std::endl;
       std::cout << c2.obter() << std::endl;
   }
   ```

3. **Templates Variádicos (C++11):**
   - Aceitam um número arbitrário de argumentos.
   ```cpp
   template <typename... Args>
   void imprimir(Args... args) {
       (std::cout << ... << args) << std::endl; // Expansão de parâmetros
   }

   int main() {
       imprimir(1, 2, 3, "Olá", 3.14);
   }
   ```

4. **Non-Type Template Parameters:**
   - Usam valores constantes como parâmetros de template.
   ```cpp
   template <typename T, int N>
   class Array {
   private:
       T dados[N];
   public:
       T& operator[](int i) { return dados[i]; }
   };

   int main() {
       Array<int, 10> arr;
       arr[0] = 42;
       std::cout << arr[0] << std::endl;
   }
   ```

5. **Templates Especiais (Specialization):**
   - Permitem fornecer implementações específicas para certos tipos.
   ```cpp
   template <typename T>
   class Exemplo {
   public:
       void exibir() { std::cout << "Genérico\n"; }
   };

   template <>
   class Exemplo<int> {
   public:
       void exibir() { std::cout << "Especializado para int\n"; }
   };

   int main() {
       Exemplo<double> e1;
       Exemplo<int> e2;

       e1.exibir(); // Genérico
       e2.exibir(); // Especializado para int
   }
   ```

---

#### Recursos Avançados:

1. **Alias Templates (C++11):**
   - Permitem criar alias para templates complexos.
   ```cpp
   template <typename T>
   using Vec = std::vector<T>;

   Vec<int> v; // Equivalente a std::vector<int>
   ```

2. **Concepts (C++20):**
   - Restringem os tipos que podem ser usados com templates.
   ```cpp
   template <typename T>
   concept Numerico = std::is_arithmetic_v<T>;

   template <Numerico T>
   T soma(T a, T b) {
       return a + b;
   }

   int main() {
       std::cout << soma(10, 20) << std::endl; // OK
       // std::cout << soma("Olá", "Mundo"); // Erro
   }
   ```

3. **Templates de Classe Internos:**
   - Usam templates dentro de outras classes.
   ```cpp
   template <typename T>
   class Externo {
   public:
       template <typename U>
       class Interno {
           U valor;
       };
   };
   ```

---

#### Exemplos Práticos:

1. **Função Genérica:**
   ```cpp
   template <typename T>
   T somar(T a, T b) {
       return a + b;
   }

   int main() {
       std::cout << somar(3, 4) << std::endl; // int
       std::cout << somar(3.14, 2.71) << std::endl; // double
   }
   ```

2. **Classe com Template:**
   ```cpp
   template <typename T>
   class Pilha {
   private:
       std::vector<T> dados;
   public:
       void empilhar(T valor) { dados.push_back(valor); }
       T desempilhar() {
           T valor = dados.back();
           dados.pop_back();
           return valor;
       }
   };

   int main() {
       Pilha<int> p;
       p.empilhar(10);
       p.empilhar(20);
       std::cout << p.desempilhar() << std::endl; // 20
   }
   ```

---

#### Boas Práticas com Templates:

- **Use nomes descritivos para parâmetros de template:** Prefira `T`, `U` ou nomes específicos como `Tipo` ou `Chave`.
- **Evite instanciar templates desnecessariamente:** Isso aumenta o tamanho do código gerado.
- **Prefira `concepts` quando possível:** Eles tornam os templates mais seguros e fáceis de entender.
- **Documente claramente os templates:** Explique os tipos esperados e os casos de uso.
- **Evite sobre-especializar:** Especializações devem ser usadas apenas quando necessário.

---

#### Referência:
Para mais informações sobre templates em C++, consulte [cppreference: Templates](https://en.cppreference.com/w/cpp/language/templates).