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

```# Classe para o array personalizado (com métodos para manipulação de dados)
class PersonalArray:
    SIZE = 5  # Tamanho inicial do array
    insertPosition = 0  # Posição de inserção
    elements = [None] * SIZE  # Array inicial com valores None

    # Função que serve para verificar se o array está vazio
    def isEmpty(self):
        return self.size() == 0
    
    # Função que retorna o número de elementos armazenados no array
    def size(self):
        return self.insertPosition
    
    # Função que verifica se o array está cheio
    def isMemoryFull(self):
        return self.insertPosition == len(self.elements)
    
    # Função que adiciona um elemento no final do array
    def append(self, newElement):
        if self.isMemoryFull():  # Verifica se há espaço para mais elementos
            self.updateMemory()  # Expande o array se necessário
        self.elements[self.insertPosition] = newElement  # Adiciona o novo elemento
        self.insertPosition += 1  # Atualiza a posição de inserção
    
    # Função para aumentar a memória do array quando necessário
    def updateMemory(self):
        newArray = [None] * (self.size() + self.SIZE)  # Cria um novo array com mais espaço
        for position in range(self.insertPosition):
            newArray[position] = self.elements[position]  # Copia os elementos existentes
        self.elements = newArray  # Substitui o array antigo pelo novo
    
    # Função para limpar o array (resetando os valores)
    def clear(self):
        self.elements = [None] * self.SIZE  # Limpa o array
        self.insertPosition = 0  # Reseta a posição de inserção
    
    # Função para remover um elemento no final (como em uma fila)
    def remove(self):
        if not self.isEmpty():
            self.elements[self.insertPosition - 1] = None
            self.insertPosition -= 1
    
    # Função para remover um elemento em uma posição específica
    def removePosition(self, position):
        if position < 0 or position >= self.insertPosition:
            print("Posição inválida!")
            return ""
        removedElement = self.elements[position]
        for index in range(position, self.insertPosition - 1):
            self.elements[index] = self.elements[index + 1]
        self.insertPosition -= 1
        return removedElement

    # Função para retornar um elemento em uma posição específica
    def elementAt(self, position):
        if position < 0 or position >= self.insertPosition:
            print("Posição inválida!")
            return None
        return self.elements[position]

# Implementação de uma fila de impressão
class PersonalQueue:
    list = PersonalArray()  # Usando o PersonalArray para armazenar os elementos da fila
    
    # Função que adiciona um elemento no final da fila
    def enqueue(self, newElement):
        self.list.append(newElement)  # Usando o append para adicionar no final
    
    # Função que remove o primeiro elemento da fila (FIFO)
    def dequeue(self):
        return self.list.removePosition(0)  # Remove o primeiro elemento da fila

# Cria uma instância do objeto da fila de impressão
fila_impressao = PersonalQueue()

# Enfileirando documentos para impressão (adicionando no final da fila)
fila_impressao.enqueue("Document1")
fila_impressao.enqueue("Document2")
fila_impressao.enqueue("Document3")

# Desenfileirando e imprimindo os documentos na ordem correta
print(fila_impressao.dequeue())  # Saída: "Document1"
print(fila_impressao.dequeue())  # Saída: "Document2"
print(fila_impressao.dequeue())  # Saída: "Document3"
