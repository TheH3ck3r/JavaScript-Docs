`Stack` (стек) — это структура данных, работающая по принципу `LIFO` (`Last In, First Out`), что означает: последний добавленный элемент извлекается первым.

### Создание `Stack`

#### Реализация стека на массиве

В JavaScript массив [!badge variant="contrast" text="Array"](Array.md) можно использовать для создания стека, так как у него есть встроенные методы `.push`() и `.pop()`

```js
class Stack {
  constructor() {
    this.items = [];
  }

  push(value) {
    this.items.push(value);
  }

  pop() {
    if (this.isEmpty()) {
      return "Стек пуст";
    }
    return this.items.pop();
  }

  peek() {
    return this.isEmpty() ? "Стек пуст" : this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }
}
```

#### Реализация стека на объекте

Массивы в JavaScript могут быть менее эффективными для стека, так как `.pop()` может потребовать переиндексации элементов. Альтернативный вариант — использовать объект [!badge variant="contrast" text="Object"](Object.md).

```js
class Stack {
  constructor() {
    this.items = {};
    this.count = 0;
  }

  push(value) {
    this.items[this.count] = value;
    this.count++;
  }

  pop() {
    if (this.isEmpty()) {
      return "Стек пуст";
    }
    this.count--;
    const value = this.items[this.count];
    delete this.items[this.count];
    return value;
  }

  peek() {
    return this.isEmpty() ? "Стек пуст" : this.items[this.count - 1];
  }

  isEmpty() {
    return this.count === 0;
  }

  size() {
    return this.count;
  }
}
```

---

### Основные методы `Stack`

- `push(value)` — добавляет элемент в вершину стека.
- `pop()` — удаляет и возвращает последний добавленный элемент.
- `peek()` — возвращает верхний элемент без удаления.
- `isEmpty()` — проверяет, пуст ли стек.
- `size()` — возвращает количество элементов.

#### Примеры работы с методами `Stack`

```js
const stack = new Stack();
stack.push(1);
stack.push(2);
stack.push(3);
console.log(stack.pop()); // 3
console.log(stack.peek()); // 2
console.log(stack.size()); // 2
console.log(stack.isEmpty()); // false
```

---

### Применение `Stack`

**1. Обратный порядок (реверс) данных**

```js
function reverseString(str) {
  const stack = new Stack();
  for (const char of str) {
    stack.push(char);
  }

  let reversed = "";
  while (!stack.isEmpty()) {
    reversed += stack.pop();
  }
  return reversed;
}

console.log(reverseString("hello")); // "olleh"
```

**2. Проверка сбалансированности скобок**

```js
function isBalanced(expression) {
  const stack = new Stack();
  const pairs = { ")": "(", "}": "{", "]": "[" };

  for (const char of expression) {
    if (Object.values(pairs).includes(char)) {
      stack.push(char);
    } else if (Object.keys(pairs).includes(char)) {
      if (stack.isEmpty() || stack.pop() !== pairs[char]) {
        return false;
      }
    }
  }

  return stack.isEmpty();
}

console.log(isBalanced("{[()]}")); // true
console.log(isBalanced("{[(])}")); // false
```

#### Заключение

`Stack` — это удобная структура данных, которая позволяет управлять элементами по принципу `LIFO` (последний вошел – первый вышел). Она широко применяется в различных алгоритмах, таких как обратный порядок строк, проверка выражений, рекурсия и обработка вызовов функций.