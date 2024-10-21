В JavaScript `sort()` - это метод, который используется для сортировки элементов в массиве. Он может сортировать элементы как в алфавитном, так и в числовом порядке, а также выполнять сортировку собственной функцией сравнения.

Синтаксис: `array.sort([compareFunction])`

- `array`: Это массив, который вы хотите отсортировать.
- `compareFunction` (необязательный): Это функция сравнения, которая определяет порядок сортировки. Если этот параметр не указан, элементы массива сортируются как строки (по умолчанию).

#### Примеры использования `sort()`:

**Сортировка чисел:**

```js
const oneDimensionalArray = [3, 1, 2, 5, 4];
oneDimensionalArray.sort((a, b) => a - b);
console.log(oneDimensionalArray); // Выведет: [1, 2, 3, 4, 5]
```

```js
const twoDimensionalArray = [
  [110, 22],
  [5, 66],
  [34, 88],
  [57, 10],
  [61, 41],
];
twoDimensionalArray.sort(([a, b], [c, d]) => a - c);
console.log(twoDimensionalArray);
// Выведет: [[ 5, 66 ], [ 34, 88 ], [ 57, 10 ], [ 61, 41 ], [ 110, 22 ]]
```

**Сортировка строк:**

```js
const fruits = ["date", "pear", "cherry", "apple"];
fruits.sort();
console.log(fruits); // Выведет: ['apple', 'cherry', 'date', 'pear']
```

```js
const fruits = ["Яблоко", "Груша", "Вишня", "Апельсин"];
fruits.sort((a, b) => a.localeCompare(b));
console.log(fruits); // Выведет: ["Апельсин", "Вишня", "Груша", "Яблоко]
```

**Собственная функция сравнения:**

```js
const items = [
  { name: "apple", price: 2 },
  { name: "banana", price: 1 },
  { name: "cherry", price: 3 },
];

items.sort((a, b) => a.price - b.price);
console.log(items);
// Выведет: [{name: 'banana', price: 1}, {name: 'apple', price: 2},
// {name: 'cherry', price: 3}]
```

Обратите внимание, что метод `sort()` изменяет исходный массив. Если вам необходимо сохранить исходный порядок элементов, лучше создайте копию массива перед сортировкой.

**Например:**

```js
const sortAnimal = (names) => [...names].sort((a, b) => a.localeCompare(b));

console.log(sortAnimal(["Mikel", "Jhon", "Sarah"]));
// Выведет новый массив: ['Jhon', 'Mikel', 'Sarah']
```
