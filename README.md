# Fila de Impressão (Queue) em Python

Este projeto implementa uma **fila de impressão** (Queue) utilizando estruturas de dados personalizadas em Python. O código simula o comportamento de uma fila, onde os documentos são enfileirados para impressão e retirados na ordem correta (FIFO - First In, First Out).

## Descrição

A fila de impressão é implementada com base em um **array personalizado**, onde os elementos são gerenciados manualmente. Os documentos são adicionados ao final da fila (com o método `append()`) e removidos a partir da primeira posição (com o método `dequeue()`), garantindo que o primeiro documento a ser enfileirado seja o primeiro a ser impresso.

## Funcionalidades

- **Adição de documentos na fila** (`enqueue`): Os documentos são inseridos no final da fila.
- **Remoção de documentos da fila** (`dequeue`): O documento mais antigo (primeiro da fila) é removido para ser impresso.
- **Gerenciamento de memória**: Quando o array atinge a capacidade máxima, ele é automaticamente expandido.

## Como Funciona

### 1. Estrutura de Dados Personalizada
A implementação utiliza um **array personalizado** (`PersonalArray`) para armazenar os elementos da fila, com métodos para verificar se o array está cheio ou vazio, adicionar e remover elementos.

### 2. Métodos Principais
- **`enqueue(newElement)`**: Adiciona um novo documento na fila (no final da fila).
- **`dequeue()`**: Remove o primeiro documento da fila (o mais antigo).

### 3. Expansão Automática
Quando a capacidade do array é atingida, o array é expandido automaticamente para acomodar mais elementos.

## Código

A classe `PersonalArray` gerencia o armazenamento dos elementos da fila, oferecendo métodos para adicionar, remover e verificar o estado dos elementos.

```python
class PersonalArray:
    SIZE = 5  # Tamanho inicial do array
    insertPosition = 0  # Posição de inserção
    elements = [None] * SIZE  # Array inicial com valores None
    
    def isEmpty(self):
        return self.size() == 0
    
    def size(self):
        return self.insertPosition
    
    def isMemoryFull(self):
        return self.insertPosition == len(self.elements)
    
    def append(self, newElement):
        if self.isMemoryFull():
            self.updateMemory()
        self.elements[self.insertPosition] = newElement
        self.insertPosition += 1
    
    def updateMemory(self):
        newArray = [None] * (self.size() + self.SIZE)
        for position in range(self.insertPosition):
            newArray[position] = self.elements[position]
        self.elements = newArray

### PersonalQueue
A classe PersonalQueue implementa a fila de impressão, utilizando o array personalizado para gerenciar os documentos na fila.

python
Copiar
class PersonalQueue:
    list = PersonalArray()
    
    def enqueue(self, newElement):
        self.list.append(newElement)
    
    def dequeue(self):
        return self.list.removePosition(0)

### Exemplo de Uso
python
Copiar
fila_impressao = PersonalQueue()

# Enfileirando documentos
fila_impressao.enqueue("Document1")
fila_impressao.enqueue("Document2")
fila_impressao.enqueue("Document3")

# Desenfileirando e imprimindo documentos
print(fila_impressao.dequeue())  # Saída: "Document1"
print(fila_impressao.dequeue())  # Saída: "Document2"
print(fila_impressao.dequeue())  # Saída: "Document3"

