`Map` — это структура данных в JavaScript, представляющая собой коллекцию пар ключ-значение, в которой ключи могут быть любого типа (включая объекты, функции и примитивы). В отличие от обычных объектов [!badge variant="contrast" text="Object"](Object.md), в `Map` порядок вставки элементов сохраняется.

### Создание `Map`

**1. Создание пустого `Map`**

```js
const map = new Map();

console.log(map); // Map(0) {}
```

**2. Создание `Map` с начальными значениями**

```js
const map = new Map([
  ["name", "Alice"],
  ["age", 25],
  ["job", "developer"],
]);

console.log(map);
// Map(3) { 'name' => 'Alice', 'age' => 25, 'job' => 'developer' }
```

---

### Основные методы `Map`

- `set(key, value)`: Добавляет пару ключ-значение
- `get(key)`: Возвращает значение по ключу
- `has(key)`: Проверяет, есть ли ключ в `Map`
- `delete(key)`: Удаляет пару ключ-значение
- `clear()`: Очищает всю коллекцию
- `size`: Возвращает количество элементов

#### Примеры работы с методами `Map`

**Добавление элементов (`set`)**

```js
const map = new Map();
map.set("name", "Alice");
map.set("age", 25);
map.set("job", "developer");

console.log(map);
// Map(3) { 'name' => 'Alice', 'age' => 25, 'job' => 'developer' }
```

**Получение значения (`get`)**

```js
console.log(map.get("name")); // Alice
console.log(map.get("age")); // 25
console.log(map.get("job")); // developer
console.log(map.get("salary")); // undefined
```

**Проверка наличия ключа (`has`)**

```js
console.log(map.has("age")); // true
console.log(map.has("salary")); // false
```

**Удаление элемента (`delete`)**

```js
map.delete("age");

console.log(map.has("age")); // false
console.log(map.size); // 2
```

**Очистка `Map` (`clear`)**

```js
map.clear();

console.log(map.size); // 0
```

---

### Особенности `Map`

**`Map` поддерживает любые типы ключей**

```js
const map = new Map();

const objKey = { id: 1 };
const funcKey = function () {};
const symbolKey = Symbol("key");

map.set(objKey, "Object Value");
map.set(funcKey, "Function Value");
map.set(symbolKey, "Symbol Value");

console.log(map.get(objKey)); // Object Value
console.log(map.get(funcKey)); // Function Value
console.log(map.get(symbolKey)); // Symbol Value
```

_P.S: В `Object` ключи могут быть только строками или `Symbol`, а в `Map` — любым типом._

**`Map` сохраняет порядок вставки**

```js
const map = new Map();
map.set(3, "three");
map.set(1, "one");
map.set(2, "two");

console.log([...map]);
// [[3, 'three'], [1, 'one'], [2, 'two']] (порядок сохраняется)
```

**Сравнение ключей по значению**

```js
const map = new Map();
map.set(1, "one");

console.log(map.get(1)); // one
console.log(map.get("1")); // undefined (разные типы)
```

#### Заключение

`Map` — это мощная структура данных, позволяющая эффективно хранить пары ключ-значение. Она обладает преимуществами над `Object`, такими как поддержка любых типов ключей, сохранение порядка и высокая производительность при частых изменениях данных.
