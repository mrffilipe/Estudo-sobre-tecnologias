### Exceções em C++ (Exceptions)

#### Resumo do Conteúdo:
O mecanismo de **exceções** em C++ é usado para tratar erros e situações inesperadas em tempo de execução de forma estruturada. Exceções permitem separar o código principal da lógica de tratamento de erros, aumentando a legibilidade e a manutenção do programa.

Exceções são geradas com a palavra-chave `throw` e capturadas com blocos `try` e `catch`.

---

#### Estrutura Básica:

1. **Lançamento de Exceção:**
   - Utiliza a palavra-chave `throw`.
   ```cpp
   throw std::runtime_error("Erro ocorrido");
   ```

2. **Bloco de Captura:**
   - Um bloco `try` delimita o código que pode lançar exceções.
   - Um ou mais blocos `catch` capturam e tratam as exceções.
   ```cpp
   try {
       // Código que pode lançar uma exceção
   } catch (const std::exception& e) {
       // Tratamento da exceção
       std::cout << "Erro: " << e.what() << std::endl;
   }
   ```

3. **Fluxo de Controle:**
   - Quando uma exceção é lançada:
     1. O programa abandona o código dentro do bloco `try`.
     2. Busca o primeiro bloco `catch` compatível com o tipo da exceção.
     3. Após o tratamento, o programa continua a partir do final do bloco `catch`.

---

#### Principais Tipos de Exceções:

1. **Exceções Padrão:**
   - Definidas na biblioteca `<stdexcept>` e derivados de `std::exception`.
   ```cpp
   #include <stdexcept>

   throw std::invalid_argument("Argumento inválido");
   throw std::out_of_range("Índice fora do intervalo");
   ```

2. **Exceções Personalizadas:**
   - Você pode criar suas próprias classes de exceção.
   ```cpp
   class MinhaExcecao : public std::exception {
   public:
       const char* what() const noexcept override {
           return "Erro personalizado";
       }
   };
   ```

3. **Exceções de Tipo Genérico:**
   - Qualquer tipo pode ser lançado como exceção, mas é recomendado usar classes derivadas de `std::exception` para maior consistência.

---

#### Exemplos Práticos:

1. **Tratamento Básico de Exceção:**
   ```cpp
   #include <iostream>
   #include <stdexcept>

   int dividir(int a, int b) {
       if (b == 0) throw std::runtime_error("Divisão por zero");
       return a / b;
   }

   int main() {
       try {
           std::cout << dividir(10, 0) << std::endl;
       } catch (const std::exception& e) {
           std::cout << "Erro: " << e.what() << std::endl;
       }
   }
   ```

2. **Multiplos Blocos `catch`:**
   ```cpp
   try {
       throw std::out_of_range("Fora do intervalo");
   } catch (const std::invalid_argument& e) {
       std::cout << "Erro de argumento: " << e.what() << std::endl;
   } catch (const std::out_of_range& e) {
       std::cout << "Erro de intervalo: " << e.what() << std::endl;
   }
   ```

3. **Exceções Personalizadas:**
   ```cpp
   class MinhaExcecao : public std::exception {
   public:
       const char* what() const noexcept override {
           return "Erro personalizado";
       }
   };

   int main() {
       try {
           throw MinhaExcecao();
       } catch (const MinhaExcecao& e) {
           std::cout << e.what() << std::endl;
       }
   }
   ```

4. **Re-lançamento de Exceção:**
   ```cpp
   try {
       try {
           throw std::runtime_error("Erro interno");
       } catch (...) {
           std::cout << "Tratando e re-lançando\n";
           throw; // Re-lança a exceção
       }
   } catch (const std::exception& e) {
       std::cout << "Erro capturado novamente: " << e.what() << std::endl;
   }
   ```

---

#### Palavras-Chave Especiais:

1. **`throw`:**
   - Lança uma exceção.
   ```cpp
   throw std::logic_error("Erro lógico");
   ```

2. **`try` e `catch`:**
   - `try` marca o código que pode lançar exceções.
   - `catch` trata as exceções.
   ```cpp
   try {
       // Código
   } catch (const std::exception& e) {
       // Tratamento
   }
   ```

3. **`noexcept`:**
   - Indica que uma função não lançará exceções.
   - Melhor para otimizações e documentação.
   ```cpp
   void funcao() noexcept {
       // Garantido sem exceções
   }
   ```

---

#### Boas Práticas para Exceções:

- **Lance exceções somente para erros excepcionais:** Evite usá-las para controle de fluxo comum.
- **Use tipos derivados de `std::exception`:** Oferece consistência e permite acesso ao método `what()`.
- **Evite lançar exceções em destrutores:** Isso pode causar terminação do programa.
- **Documente exceções lançadas por funções:** Facilita o uso e manutenção do código.
- **Use `noexcept` quando apropriado:** Ajuda o compilador a otimizar código seguro.

---

#### Referência:
Para mais informações sobre exceções em C++, consulte [cppreference: Exceptions](https://en.cppreference.com/w/cpp/language/exceptions).