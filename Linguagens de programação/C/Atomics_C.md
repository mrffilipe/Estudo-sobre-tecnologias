
# Operações Atômicas na Linguagem C

## Visão Geral
Operações atômicas na linguagem C são operações indivisíveis que são executadas completamente sem interrupções. Elas são cruciais para a programação concorrente, garantindo que múltiplas threads possam manipular dados compartilhados de maneira segura sem causar condições de corrida.

## Tipos Atômicos

### Tipos Atômicos Padrão
- O cabeçalho `<stdatomic.h>` define tipos atômicos padrão usando macros genéricas.
- Exemplo:
  ```c
  _Atomic int atomic_int;
  ```

### Tipos Atômicos Genéricos
- `atomic_bool`, `atomic_char`, `atomic_short`, `atomic_int`, `atomic_long`, `atomic_llong`, `atomic_uchar`, `atomic_ushort`, `atomic_uint`, `atomic_ulong`, `atomic_ullong`, `atomic_char16_t`, `atomic_char32_t`, `atomic_wchar_t`, `atomic_int_least8_t`, `atomic_uint_least8_t`, etc.
- Exemplo:
  ```c
  atomic_int a;
  atomic_long b;
  ```

### Tipos Atômicos Personalizados
- Qualquer tipo de dado pode ser declarado como atômico usando `_Atomic`.
- Exemplo:
  ```c
  typedef struct {
      int x, y;
  } Point;

  _Atomic Point p;
  ```

## Funções e Operações Atômicas

### Inicialização
- Tipos atômicos podem ser inicializados como qualquer outro tipo de dado.
- Exemplo:
  ```c
  atomic_int a = ATOMIC_VAR_INIT(5);
  ```

### Operações de Carregamento e Armazenamento
- `atomic_store`, `atomic_load` são usadas para armazenar e carregar valores atômicos.
- Exemplo:
  ```c
  atomic_store(&a, 10);
  int value = atomic_load(&a);
  ```

### Operações de Leitura-Modificação-Gravação
- `atomic_exchange`, `atomic_fetch_add`, `atomic_fetch_sub`, `atomic_fetch_or`, `atomic_fetch_and`, `atomic_fetch_xor`.
- Exemplo:
  ```c
  int old = atomic_exchange(&a, 20);
  int new_value = atomic_fetch_add(&a, 5);
  ```

### Comparação e Troca
- `atomic_compare_exchange_strong`, `atomic_compare_exchange_weak` são usadas para comparar e trocar valores atômicos.
- Exemplo:
  ```c
  int expected = 10;
  bool exchanged = atomic_compare_exchange_strong(&a, &expected, 20);
  ```

## Memória e Barreiras

### Ordens de Memória
- `memory_order_relaxed`, `memory_order_consume`, `memory_order_acquire`, `memory_order_release`, `memory_order_acq_rel`, `memory_order_seq_cst`.
- Exemplo:
  ```c
  atomic_store_explicit(&a, 10, memory_order_release);
  int value = atomic_load_explicit(&a, memory_order_acquire);
  ```

### Barreiras de Memória
- Funções como `atomic_thread_fence` e `atomic_signal_fence` impõem barreiras de memória para controlar a ordem das operações.
- Exemplo:
  ```c
  atomic_thread_fence(memory_order_acquire);
  atomic_signal_fence(memory_order_release);
  ```

## Exemplos Práticos

### Inicialização e Operações Simples
```c
atomic_int counter = ATOMIC_VAR_INIT(0);

void increment() {
    atomic_fetch_add(&counter, 1);
}

int get_value() {
    return atomic_load(&counter);
}
```

### Comparação e Troca
```c
atomic_int flag = ATOMIC_VAR_INIT(0);

void set_flag() {
    int expected = 0;
    atomic_compare_exchange_strong(&flag, &expected, 1);
}

int check_flag() {
    return atomic_load(&flag);
}
```

### Uso de Barreiras de Memória
```c
atomic_int data = ATOMIC_VAR_INIT(0);
atomic_int ready = ATOMIC_VAR_INIT(0);

void producer() {
    atomic_store(&data, 42);
    atomic_thread_fence(memory_order_release);
    atomic_store(&ready, 1);
}

void consumer() {
    while (atomic_load(&ready) == 0);
    atomic_thread_fence(memory_order_acquire);
    int value = atomic_load(&data);
}
```

## Dicas de Boas Práticas
- **Use Tipos Atômicos para Dados Compartilhados:** Sempre use tipos atômicos para dados acessados por múltiplas threads.
- **Escolha a Ordem de Memória Adequada:** Use a ordem de memória correta para balancear desempenho e correção.
- **Evite Condições de Corrida:** Utilize operações atômicas para evitar condições de corrida em programação concorrente.
