`Set` - это встроенный объект в JavaScript, представляющий собой коллекцию уникальных значений, то есть набор элементов, в котором каждое значение может встречаться только один раз.

**Методы и операции:**

- `add(value)`: Добавляет значение value в множество Set.
- `delete(value)`: Удаляет значение value из множества Set, если оно существует.
- `has(value)`: Проверяет наличие значения value в множестве Set и возвращает true, если оно есть, и false, если нет.
- `clear()`: Удаляет все элементы из множества Set.
- `size (или length)`: Свойство, которое возвращает количество элементов в множестве.

#### Пример использования `Set`:

```js
const uniqueNumbers = new Set();

uniqueNumbers.add(1);
uniqueNumbers.add(2);
uniqueNumbers.add(2); // Этот элемент не будет добавлен второй раз

console.log(uniqueNumbers); // Выведет: Set { 1, 2 }

console.log(uniqueNumbers.has(1)); // Выведет: true

uniqueNumbers.delete(1);
console.log(uniqueNumbers); // Выведет: Set { 2 }

uniqueNumbers.clear();
console.log(uniqueNumbers); // Выведет: Set {}
```
