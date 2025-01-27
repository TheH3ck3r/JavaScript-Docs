Метод `toSorted()` — это современный метод для сортировки массива, введенный в спецификации ECMAScript. В отличие от метода [!badge variant="contrast" text="sort"](../../Методы_и_операторы/S/Sort.md), он не изменяет исходный массив, а возвращает новый массив с отсортированными элементами. Это делает его полезным для работы с данными, где требуется сохранить неизменным оригинальный массив.

Синтаксис: `array.toSorted(compareFunction)`

- `array`: Массив, который нужно отсортировать.
- `compareFunction` (необязательный): Функция сравнения, определяющая порядок сортировки. Если не указана, элементы сортируются как строки в порядке Unicode.

#### Отличие от `sort()`:

- `sort()` изменяет исходный массив.
- `toSorted()` возвращает новый массив, не затрагивая оригинал.

В остальном `toSorted()` работает аналогично `sort()`.

#### Примеры использования `toSorted()`:

**Сортировка чисел:**

```js
const numbers = [3, 1, 4, 1, 5, 9];
const sortedNumbers = numbers.toSorted((a, b) => a - b);

console.log(sortedNumbers); // [1, 1, 3, 4, 5, 9]
console.log(numbers); // [3, 1, 4, 1, 5, 9] (исходный массив не изменен)
```

**Сортировка строк:**

```js
const fruits = ["date", "pear", "cherry", "apple"];
const sortedFruits = fruits.toSorted();

console.log(sortedFruits); // ['apple', 'cherry', 'date', 'pear']
console.log(fruits); // ['date', 'pear', 'cherry', 'apple'] (исходный массив не изменен)
```

**Сортировка объектов:**

```js
const items = [
  { name: "apple", price: 2 },
  { name: "banana", price: 1 },
  { name: "cherry", price: 3 },
];
const sortedItems = items.toSorted((a, b) => a.price - b.price);

console.log(sortedItems);
// [{name: 'banana', price: 1}, {name: 'apple', price: 2}, {name: 'cherry', price: 3}]
console.log(items);
// [{name: 'apple', price: 2}, {name: 'banana', price: 1}, {name: 'cherry', price: 3}]
```

#### Заключение

Метод `toSorted()` предоставляет удобный способ сортировки массива без изменения исходного массива. Он особенно полезен в случаях, когда требуется сохранить исходные данные неизменными, например, при работе с состояниями в React или других библиотеках. В большинстве случаев он может заменить `sort()` там, где важна неизменяемость данных.
