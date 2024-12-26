### Funções em C++ (Functions)

#### Resumo do Conteúdo:
As **funções** em C++ são blocos de código reutilizáveis que realizam tarefas específicas. Elas recebem entradas (parâmetros), realizam operações e podem retornar um resultado. C++ oferece suporte a várias funcionalidades avançadas para funções, como sobrecarga, templates, lambdas, e padrões modernos como `constexpr` e `noexcept`.

---

#### Estrutura Básica de uma Função:

1. **Declaração (Protótipo):**
   Define a assinatura da função, informando o tipo de retorno, nome e parâmetros.
   ```cpp
   int soma(int a, int b); // Protótipo
   ```

2. **Definição:**
   Contém a implementação da função.
   ```cpp
   int soma(int a, int b) {
       return a + b;
   }
   ```

3. **Chamada:**
   Executa a função.
   ```cpp
   int resultado = soma(10, 20);
   ```

---

#### Tipos de Funções:

1. **Funções com Retorno:**
   Retornam um valor utilizando a palavra-chave `return`.
   ```cpp
   int quadrado(int x) {
       return x * x;
   }
   ```

2. **Funções sem Retorno:**
   Usam o tipo `void`.
   ```cpp
   void mostrarMensagem() {
       std::cout << "Olá, C++!";
   }
   ```

3. **Funções Inline:**
   São otimizadas pelo compilador, substituindo a chamada pela implementação.
   ```cpp
   inline int soma(int a, int b) {
       return a + b;
   }
   ```

4. **Funções `constexpr`:**
   Avaliadas em tempo de compilação (C++11 e posterior).
   ```cpp
   constexpr int quadrado(int x) {
       return x * x;
   }
   constexpr int area = quadrado(5); // Avaliado em tempo de compilação
   ```

5. **Funções `noexcept`:**
   Indicam que não lançam exceções (C++11 e posterior).
   ```cpp
   int soma(int a, int b) noexcept {
       return a + b;
   }
   ```

6. **Funções Lambda:**
   Funções anônimas introduzidas no C++11.
   ```cpp
   auto soma = [](int a, int b) { return a + b; };
   int resultado = soma(5, 10);
   ```

7. **Funções Template:**
   Permitem criar funções genéricas.
   ```cpp
   template <typename T>
   T maior(T a, T b) {
       return (a > b) ? a : b;
   }
   ```

---

#### Parâmetros em Funções:

1. **Parâmetros por Valor:**
   Faz uma cópia do argumento.
   ```cpp
   void dobrar(int x) {
       x = x * 2; // Não altera o valor original
   }
   ```

2. **Parâmetros por Referência:**
   Permite modificar o argumento original.
   ```cpp
   void dobrar(int& x) {
       x = x * 2; // Modifica o valor original
   }
   ```

3. **Parâmetros por Ponteiro:**
   Passa o endereço da variável.
   ```cpp
   void dobrar(int* x) {
       *x = *x * 2;
   }
   ```

4. **Parâmetros com Valor Padrão:**
   Possuem valores opcionais.
   ```cpp
   void saudacao(std::string nome = "Visitante") {
       std::cout << "Olá, " << nome;
   }
   ```

---

#### Sobrecarga de Funções:
Permite criar múltiplas versões de uma função com assinaturas diferentes.
```cpp
int soma(int a, int b) {
    return a + b;
}

double soma(double a, double b) {
    return a + b;
}
```

---

#### Exemplos Práticos:

1. **Função Simples:**
   ```cpp
   int soma(int a, int b) {
       return a + b;
   }
   ```

2. **Função com Referência:**
   ```cpp
   void dobrar(int& x) {
       x = x * 2;
   }
   ```

3. **Lambda:**
   ```cpp
   auto dobro = [](int x) { return x * 2; };
   int resultado = dobro(10);
   ```

4. **Template:**
   ```cpp
   template <typename T>
   T menor(T a, T b) {
       return (a < b) ? a : b;
   }
   ```

---

#### Boas Práticas para Funções:

- **Mantenha funções pequenas e específicas:** Cada função deve ter uma responsabilidade bem definida.
- **Use nomes descritivos:** O nome da função deve indicar claramente o que ela faz.
- **Evite efeitos colaterais:** Prefira funções que não alteram variáveis globais diretamente.
- **Prefira `constexpr` e `noexcept` sempre que aplicável:** Essas práticas aumentam a eficiência e segurança do código.
- **Documente funções:** Explique seus parâmetros, retornos e comportamento.

---

#### Referência:
Para mais informações sobre funções em C++, consulte [cppreference: Functions](https://en.cppreference.com/w/cpp/language/functions).