Объекты (`Objects`) — одна из ключевых структур данных в JavaScript. Они позволяют хранить данные в формате ключ-значение и широко используются во всех аспектах языка.

Объект в JavaScript — это коллекция свойств, где каждое свойство имеет уникальный ключ (имя) и значение. Ключами могут быть только строки и символы, а значениями — любые данные (включая другие объекты и функции).

### Создание `Object`

**1. Самый распространенный способ создания объекта — использование фигурных скобок `{}`:**

```js
const person = {
  name: "Alice",
  age: 25,
  isStudent: false,
};
console.log(person.name); // "Alice"
```

**2. `Object.create()` позволяет создать объект с указанным прототипом:**

```js
const prototypePerson = {
  greet() {
    console.log("Hello!");
  },
};
const newPerson = Object.create(prototypePerson);
newPerson.greet(); // "Hello!"
```

_P.S: Если передать `null`, объект создастся без прототипа:_

```js
const emptyObject = Object.create(null);
```

**3. Можно создать объект с помощью функции-конструктора:**

```js
function User(name, age) {
  this.name = name;
  this.age = age;
}

const user1 = new User("Alice", 25);
console.log(user1.name); // "Alice"
```

**4. Более современный способ, аналогичный конструкторам, а именно, классы:**

```js
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const user2 = new User("Bob", 30);
console.log(user2.age); // 30
```

---

### Копирование объектов

При копировании объекта важно понимать, что в JavaScript объекты передаются по ссылке. Это означает, что если мы просто присвоим объект в другую переменную, то изменится сам объект, а не его копия.

#### Поверхностное копирование (shallow copy)

**1. `Object.assign()`**

```js
const obj1 = { name: "Alice", age: 25 };
const copy1 = Object.assign({}, obj1);

copy1.name = "Bob";
console.log(obj1.name); // "Alice" (не изменилось)
```

**2. Оператор [!badge variant="contrast" text="spread"](../../Методы_и_операторы/S/Spread.md)**

```js
const copy2 = { ...obj1 };
copy2.age = 30;

console.log(obj1.age); // 25 (оригинальный объект не изменился)
```

**Однако оба метода копируют ссылки на вложенные объекты:**

```js
const obj3 = { name: "Alice", details: { city: "NY" } };
const copy3 = { ...obj3 };

copy3.details.city = "LA";
console.log(obj3.details.city); // "LA" (изменилось в обоих объектах)
```

#### Глубокое копирование (deep copy)

Глубокое копирование создает полностью независимую копию, включая вложенные объекты.

**Использование `structuredClone()`**

```js
const deepCopy = structuredClone(obj3);
deepCopy.details.city = "Paris";

console.log(obj3.details.city); // "NY" (не изменилось)
```

Этот метод копирует вложенные объекты, массивы и даже [!badge variant="contrast" text="Map"](Map.md) и [!badge variant="contrast" text="Set"](Set.md).

---

### Методы объектов

Методы — это функции, которые находятся внутри объекта и могут работать с его данными через `this`.

**Определение метода**

```js
const person = {
  name: "Alice",
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  },
};

person.greet(); // "Hello, my name is Alice"
```

`this` ссылается на сам объект, внутри которого вызывается метод.

**Потеря контекста `this`**

Если вызвать метод отдельно, `this` может стать `undefined`:

```js
const fn = user.show;
fn(); // Ошибка в strict mode
```

Решение: привязать `this` с помощью [!badge variant="contrast" text="bind"](../Методы_и_операторы/B/Bind.md):

```js
const boundFn = user.show.bind(user);
boundFn(); // "Bob"
```

---

### Прототипы и наследование

JavaScript использует прототипное наследование [!badge variant="contrast" text="Prototype"](../Встроенные_объекты/Prototype.md). Каждый объект может наследовать свойства и методы другого объекта.

#### Прототип объекта

Все объекты в JavaScript имеют прототип, который можно получить с помощью `Object.getPrototypeOf()`:

```js
const obj = {};
console.log(Object.getPrototypeOf(obj) === Object.prototype); // true
```

#### Классы и `extends`

Современный способ создавать объекты с наследованием:

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(`${this.name} издает звук`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} лает`);
  }
}

const dog = new Dog("Бобик");
dog.speak(); // "Бобик лает"
```

_P.S: Ключевое слово `super` позволяет вызвать метод родительского класса:_

```js
class Cat extends Animal {
  speak() {
    super.speak(); // Вызов метода родителя
    console.log(`${this.name} мурлычет`);
  }
}

const cat = new Cat("Мурка");
cat.speak();
// "Мурка издает звук"
// "Мурка мурлычет"
```

---

### Замораживание объектов

Иногда нужно сделать объект неизменяемым.

**1. `Object.freeze()` (Полная защита)**

```js
const obj = { name: "Alice" };
Object.freeze(obj);

obj.name = "Bob"; // Изменение не произойдет
delete obj.name; // Удаление не произойдет

console.log(obj.name); // "Alice"
```

_P.S: Прототип тоже становится неизменяемым_

**2. `Object.seal()` (Запрещает добавление и удаление)**

```js
const obj2 = { age: 30 };
Object.seal(obj2);

obj2.age = 31; // Можно изменить
delete obj2.age; // ❌ Нельзя удалить
obj2.newProp = 42; // ❌ Нельзя добавить

console.log(obj2.age); // 31
```

#### Заключение

Объекты (`Object`) в JavaScript — это фундаментальная структура данных, которая позволяет хранить и организовывать данные в виде пар ключ-значение. Они широко используются в программировании для представления сущностей, хранения конфигураций, работы с API и создания сложных структур.
