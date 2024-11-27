### **4. Divisão e Conquista (Divide-and-Conquer)**

#### **Visão Geral**
O método de **divisão e conquista** é uma poderosa estratégia de design de algoritmos para resolver problemas de maneira eficiente. Ele se baseia em dividir um problema maior em subproblemas menores, resolvê-los recursivamente e então combinar suas soluções para resolver o problema original.

---

### **Estrutura do Método**
1. **Dividir (Divide)**:
   - O problema é dividido em um ou mais subproblemas, que são instâncias menores do problema original.

2. **Conquistar (Conquer)**:
   - Os subproblemas são resolvidos recursivamente. Se o problema for pequeno o suficiente (caso base), ele é resolvido diretamente.

3. **Combinar (Combine)**:
   - As soluções dos subproblemas são combinadas para formar a solução do problema original.

Exemplo: O algoritmo **Merge Sort** segue essa estrutura:
- Divide a entrada em duas metades.
- Ordena cada metade recursivamente.
- Combina as duas metades ordenadas em uma única sequência ordenada.

---

### **Análise Matemática: Recorrências**
A análise de algoritmos de divisão e conquista geralmente utiliza recorrências para descrever o tempo de execução. Uma recorrência expressa o custo de resolver um problema de tamanho \( n \) em termos de subproblemas menores.

#### **Forma Geral**
Se um problema de tamanho \( n \) é dividido em \( a \) subproblemas, cada um de tamanho \( n/b \), com custo \( D(n) \) para dividir e \( C(n) \) para combinar, o tempo de execução \( T(n) \) é:
\[
T(n) = aT\left(\frac{n}{b}\right) + D(n) + C(n)
\]

---

### **Exemplo de Recorrências**
1. **Merge Sort**:
   - Divide: \( D(n) = \Theta(1) \).
   - Conquista: \( a = 2 \), \( b = 2 \) (dois subproblemas de tamanho \( n/2 \)).
   - Combina: \( C(n) = \Theta(n) \).
   - Recorrência:
     \[
     T(n) = 2T\left(\frac{n}{2}\right) + \Theta(n)
     \]
   - Solução: \( T(n) = \Theta(n \log n) \).

2. **Multiplicação de Matrizes (Simples)**:
   - Divide: Matriz \( n \times n \) dividida em 4 submatrizes \( n/2 \times n/2 \).
   - Conquista: \( a = 8 \), \( b = 2 \) (8 subproblemas de tamanho \( n/2 \)).
   - Combina: \( \Theta(n^2) \).
   - Recorrência:
     \[
     T(n) = 8T\left(\frac{n}{2}\right) + \Theta(n^2)
     \]
   - Solução: \( T(n) = \Theta(n^3) \).

3. **Strassen’s Algorithm**:
   - Divide: Usa álgebra para reduzir multiplicações.
   - Conquista: \( a = 7 \), \( b = 2 \) (7 subproblemas).
   - Combina: \( \Theta(n^2) \).
   - Recorrência:
     \[
     T(n) = 7T\left(\frac{n}{2}\right) + \Theta(n^2)
     \]
   - Solução: \( T(n) = \Theta(n^{\log_2 7}) \approx \Theta(n^{2.81}) \).

---

### **Métodos para Resolver Recorrências**
1. **Método da Substituição**:
   - Adota uma hipótese e prova por indução.
2. **Árvore de Recursão**:
   - Representa a recorrência como uma árvore para somar os custos em cada nível.
3. **Teorema Mestre**:
   - Aplica-se a recorrências da forma:
     \[
     T(n) = aT\left(\frac{n}{b}\right) + f(n)
     \]
   - Classifica o crescimento de \( T(n) \) com base em \( f(n) \) e \( a/b^k \), onde \( k = \log_b a \).

---

### **Aplicações**
- Ordenação: Merge Sort.
- Multiplicação de Matrizes: Strassen’s Algorithm.
- Pesquisa: Pesquisa Binária.
- Algoritmos Geométricos: Divisão de planos.

---

### **Resumo**
O método de divisão e conquista é amplamente utilizado por sua capacidade de resolver problemas complexos ao dividir a complexidade em partes menores e gerenciáveis. A análise cuidadosa dessas técnicas, usando ferramentas como recorrências, garante eficiência e escalabilidade.