Метод `includes()` в JavaScript используется для проверки наличия элемента в массиве или подстроки в строке. Он возвращает логическое значение `true`, если элемент или подстрока найдены, и `false`, если нет.

Синтаксис `includes()` для массивов: `array.includes(searchElement, fromIndex);`

Синтаксис `includes()` для строк: `string.includes(searchString, position);`

- `array` или `string`: Исходный массив или строка, в которой производится поиск.
- `searchElement` или `searchString`: Элемент или строка, которую нужно найти в массиве или строке.
- `fromIndex` (необязательный для массивов): Начальный индекс поиска. По умолчанию поиск начинается с индекса 0. Если `fromIndex` отрицателен, он рассчитывается как `array.length + fromIndex`.
- `position` (необязательный для строк): Позиция, с которой начинается поиск. По умолчанию `0`.

#### Примеры использования `includes()` для массивов:

```javascript
const array = [1, 2, 3, 4, 5];

console.log(array.includes(3)); // Вывод: true
console.log(array.includes(6)); // Вывод: false

console.log(array.includes(3, 3)); // Вывод: false, начиная с индекса 3
```

#### Примеры использования `includes()` для строк:

```js
const str = "Hello, world!";

console.log(str.includes("world")); // Вывод: true
console.log(str.includes("goodbye")); // Вывод: false

console.log(str.includes("Hello", 1)); // Вывод: false, начиная с позиции 1
```

Метод `includes()` особенно полезен, когда вам нужно быстро проверить наличие элемента или подстроки без необходимости получать их индекс. Он возвращает `true`, если элемент или подстрока найдены, и `false`, если нет.
