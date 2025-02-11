В JavaScript каждый объект имеет свойство `prototype`, которое является ссылкой на другой объект, называемый прототипом. Прототип объекта используется для наследования свойств и методов от этого прототипа.

Когда вы обращаетесь к свойству или методу объекта, JavaScript сначала ищет это свойство или метод непосредственно в самом объекте. Если свойство или метод не найдены, JavaScript будет искать их в прототипе объекта. Если свойство или метод также не найдены в прототипе, поиск будет продолжаться по цепочке прототипов до тех пор, пока либо не будет найдено нужное свойство или метод, либо не будет достигнут глобальный объект `Object.prototype`.

`prototype` - это свойство функции, которое указывает на прототип объекта, созданного этой функцией через оператор new. Когда функция вызывается с оператором new, создается новый объект, и prototype этой функции становится прототипом такого нового объекта. При этом каждый новый объект наследует свойства и методы прототипа функции.

#### Вот как это работает:

**Создание функции-конструктора:** Вы создаете функцию, которая будет использоваться для создания объектов определенного типа. Например:

```js
  function Person(name, age) {
    this.name = name;
    this.age = age;
```

**Использование `.prototype`:**

Вы добавляете методы и свойства к объекту `.prototype` функции-конструктора. Например:

```js
Person.prototype.sayHello = function () {
  console.log(`Привет, меня зовут ${this.name} и мне ${this.age} лет.`);
};
```

Этот метод будет доступен для всех объектов, созданных с использованием `Person`, так как все они будут наследовать `.prototype`.

**Создание объектов:** Теперь вы можете создавать объекты с помощью вашей функции-конструктора:

```js
const person1 = new Person("Анна", 30);
const person2 = new Person("Иван", 25);
```

**Использование унаследованных методов:** Вы можете вызывать методы, определенные в `.prototype`, на созданных объектах:

```js
person1.sayHello(); // Выводит: Привет, меня зовут Анна и мне 30 лет.
person2.sayHello(); // Выводит: Привет, меня зовут Иван и мне 25 лет.
```

`.prototype` позволяет сэкономить память, так как методы и свойства не дублируются для каждого объекта, а только ссылку на `.prototype`. Это также позволяет добавлять новые методы и свойства к существующим объектам этого типа, и эти изменения будут отражены во всех объектах этого типа.

Запись `.prototype` используется в старом синтаксисе для создания классов и наследования в JavaScript.

Таким же образом, с помощью `.prototype` вы можете создавать методы для структур данных (т-к они тоже объекты). Например:

```js
Array.prototype.last = function () {
  return this.length ? this.at(-1) : -1;
};

const arr = [1, 2, 3];
console.log(arr.last()); // Выводит: 3
```

_P.S: В современном JavaScript есть более удобные способы создания классов и наследования с использованием ключевых слов `class`, `extends` и `super`._
