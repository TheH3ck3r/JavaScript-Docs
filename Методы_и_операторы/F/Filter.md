`filter()` - это один из методов массивов в JavaScript. Этот метод позволяет создать новый массив, включающий в себя только те элементы исходного массива, которые удовлетворяют определенному условию, заданному с помощью функции обратного вызова.

Синтаксис: `array.filter(callback(element, index, array))`

- `array`: Исходный массив, который нужно отфильтровать.
- `callback`: Функция, которая будет вызываться для каждого элемента массива.
  - `element`: Текущий элемент массива, который анализируется.
  - `index` (необязательный): Индекс текущего элемента.
  - `array` (необязательный): Исходный массив.

#### Возвращаемое значение:

`filter()` создает и возвращает новый массив, содержащий только элементы исходного массива, для которых функция обратного вызова возвращает `true`.

#### Примеры использования `filter()`:

**Фильтрация чисел больше заданного порога:**

```js
const numbers = [1, 5, 10, 15, 20];
const threshold = 10;
const filteredNumbers = numbers.filter((number) => number > threshold);

console.log(filteredNumbers); // Выведет: [15, 20]
```

**Фильтрация строк, содержащих определенную подстроку:**

```js
const words = ["apple", "banana", "cherry", "date"];
const searchTerm = "a";
const filteredWords = words.filter((word) => word.includes(searchTerm));

console.log(filteredWords); // Выведет: ["apple", "banana", "date"]
```

**Фильтрация объектов в массиве:**

```js
const products = [
  { name: "Apple", price: 1.99 },
  { name: "Banana", price: 0.99 },
  { name: "Cherry", price: 2.49 },
];
const affordableProducts = products.filter((product) => product.price < 2.0);

console.log(affordableProducts); // Выведет: [{ name: "Banana", price: 0.99 }]
```

#### Заключение

`filter()` полезен для выбора подмножества элементов массива, которые соответствуют определенным критериям, и создания нового массива на основе этих элементов.
