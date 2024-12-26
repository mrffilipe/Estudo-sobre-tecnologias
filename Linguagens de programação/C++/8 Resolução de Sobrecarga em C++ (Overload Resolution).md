### Resolução de Sobrecarga em C++ (Overload Resolution)

#### Resumo do Conteúdo:
A **resolução de sobrecarga** em C++ refere-se ao processo pelo qual o compilador escolhe a melhor função ou operador sobrecarregado para ser chamado quando várias versões estão disponíveis. Esse processo ocorre durante a compilação e é baseado nas regras de conversão de tipos, prioridade de correspondência e contexto da chamada.

---

#### Etapas de Resolução de Sobrecarga:

1. **Identificação de Funções Viáveis:**
   - O compilador lista todas as funções candidatas com o mesmo nome que sejam acessíveis no escopo e que tenham o número correto de parâmetros.

2. **Correspondência de Tipos:**
   - O compilador analisa se os tipos dos argumentos fornecidos podem ser convertidos nos parâmetros das funções candidatas.

3. **Escolha da Melhor Correspondência:**
   - A função com os melhores tipos correspondentes é escolhida.
   - Regras:
     - Correspondência exata (sem conversões) é priorizada.
     - Conversões padrão (ex.: `int` para `float`) são aceitas.
     - Conversões mais complexas (ex.: `int*` para `void*`) têm menor prioridade.

4. **Rejeição de Ambiguidade:**
   - Se mais de uma função for igualmente válida, ocorre um erro de ambiguidade.

---

#### Exemplos de Sobrecarga:

1. **Funções com Assinaturas Diferentes:**
   ```cpp
   void imprimir(int x) {
       std::cout << "Número inteiro: " << x << std::endl;
   }

   void imprimir(double x) {
       std::cout << "Número double: " << x << std::endl;
   }

   void imprimir(const std::string& s) {
       std::cout << "Texto: " << s << std::endl;
   }

   int main() {
       imprimir(10);          // Chama a versão para int
       imprimir(3.14);        // Chama a versão para double
       imprimir("Olá, C++!"); // Chama a versão para string
   }
   ```

2. **Funções com Argumentos Padrão:**
   ```cpp
   void saudacao(const std::string& nome = "Visitante") {
       std::cout << "Olá, " << nome << "!" << std::endl;
   }

   int main() {
       saudacao();               // Usa o valor padrão
       saudacao("Carlos");       // Usa o argumento fornecido
   }
   ```

3. **Sobrecarga de Operadores:**
   ```cpp
   class Numero {
   public:
       int valor;
       Numero(int v) : valor(v) {}

       Numero operator+(const Numero& outro) const {
           return Numero(valor + outro.valor);
       }
   };

   int main() {
       Numero a(10), b(20);
       Numero c = a + b; // Usa o operador sobrecarregado
       std::cout << c.valor; // Saída: 30
   }
   ```

---

#### Regras de Prioridade de Resolução:

1. **Correspondência Exata:**
   ```cpp
   void func(int x);
   func(10); // Correspondência exata
   ```

2. **Conversão de Tipos Automática:**
   ```cpp
   void func(double x);
   func(10); // Conversão de int para double
   ```

3. **Conversões Personalizadas:**
   - Conversões definidas pelo usuário ou implícitas têm menor prioridade.
   ```cpp
   class A {
   public:
       operator int() const { return 42; }
   };

   void func(int x);
   A obj;
   func(obj); // Usa a conversão definida pelo usuário
   ```

4. **Ambiguidade:**
   ```cpp
   void func(int x);
   void func(float x);
   func(10); // Erro: Ambiguidade entre int e float
   ```

---

#### Exemplos de Ambiguidade e Erros:

1. **Ambiguidade entre Sobrecargas:**
   ```cpp
   void func(int x);
   void func(float x);

   int main() {
       func(10); // Ambíguo: int pode ser convertido para float
   }
   ```

2. **Erro com Conversões Indiretas:**
   ```cpp
   void func(int x);
   void func(double x);

   func('A'); // Ambíguo: char pode ser convertido para int ou double
   ```

---

#### Dicas de Boas Práticas:

- **Evite sobrecargas excessivamente similares:** Isso reduz ambiguidades e facilita a manutenção do código.
- **Documente cada sobrecarga claramente:** Explique o propósito de cada versão.
- **Prefira funções com nomes diferentes para comportamentos distintos:** Ajuda a evitar ambiguidade.
- **Use argumentos padrão com cuidado:** Eles podem causar conflitos com outras sobrecargas.

---

#### Referência:
Para mais detalhes sobre resolução de sobrecarga em C++, consulte [cppreference: Overload Resolution](https://en.cppreference.com/w/cpp/language/overload_resolution).