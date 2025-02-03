Очередь (`Queue`) — это структура данных, которая работает по принципу `FIFO` (`First In, First Out`). Это означает, что первый элемент, который добавляется в очередь, будет первым извлечен.

### Создание `Queue`

#### Реализация Очереди с помощью класса (оптимизированная версия)

Чтобы избежать сдвига элементов при удалении, можно использовать объект с двумя указателями (`head` и `tail`).

```js
class Queue {
  constructor() {
    this.items = {};
    this.head = 0;
    this.tail = 0;
  }

  enqueue(element) {
    this.items[this.tail] = element;
    this.tail++;
  }

  dequeue() {
    if (this.isEmpty()) return undefined;

    const item = this.items[this.head];
    delete this.items[this.head];
    this.head++;
    return item;
  }

  peek() {
    return this.isEmpty() ? undefined : this.items[this.head];
  }

  isEmpty() {
    return this.head === this.tail;
  }

  size() {
    return this.tail - this.head;
  }

  clear() {
    this.items = {};
    this.head = 0;
    this.tail = 0;
  }
}
```

---

### Основные методы `Queue`

- `enqueue(element)`: Добавляет элемент в конец очереди
- `dequeue()`: Удаляет и возвращает первый элемент
- `peek()`: Показывает первый элемент без удаления
- `isEmpty()`: Проверяет, пуста ли очередь
- `clear()`: Очищает всю очередь
- `size()`: Возвращает количество элементов в очереди

#### Примеры работы с методами `Queue`

```js
const queue = new Queue();
queue.enqueue("Alice");
queue.enqueue("Bob");
queue.enqueue("Charlie");

console.log(queue.dequeue()); // Alice
console.log(queue.peek()); // Bob
console.log(queue.size()); // 2
console.log(queue.isEmpty()); // false
queue.clear();
console.log(queue.isEmpty()); // true
```

---

### Особенности `Queue`

**1. Очередь работает по принципу `FIFO`**

```js
const queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
queue.enqueue(3);

console.log(queue.dequeue()); // 1
console.log(queue.dequeue()); // 2
console.log(queue.dequeue()); // 3
```

_Первый элемент, который зашел, выходит первым!_

**2. Очередь поддерживает ограничение по размеру (`Fixed Queue`)**

Можно создать очередь с фиксированным размером, которая не позволяет добавлять элементы при переполнении.

```js
class FixedQueue {
  constructor(limit) {
    this.items = {};
    this.head = 0;
    this.tail = 0;
    this.limit = limit;
  }

  enqueue(element) {
    if (this.size() >= this.limit) {
      console.log("Очередь переполнена!");
      return;
    }
    this.items[this.tail] = element;
    this.tail++;
  }

  dequeue() {
    if (this.isEmpty()) return undefined;

    const item = this.items[this.head];
    delete this.items[this.head];
    this.head++;
    return item;
  }

  size() {
    return this.tail - this.head;
  }

  isEmpty() {
    return this.head === this.tail;
  }
}

// Пример использования
const queue = new FixedQueue(2);
queue.enqueue("Task 1");
queue.enqueue("Task 2");
queue.enqueue("Task 3"); // Очередь переполнена!
console.log(queue.dequeue()); // Task 1
console.log(queue.dequeue()); // Task 2
```

#### Заключение

Очередь (`Queue`) — это одна из ключевых структур данных, работающая по принципу `FIFO` (`First In, First Out`). Она широко используется в алгоритмах обработки данных, многозадачности и сетевых технологиях.
