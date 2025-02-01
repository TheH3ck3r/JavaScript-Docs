`Promise` (промис) в JavaScript — это объект, который представляет асинхронную операцию и её будущий результат. Он используется, чтобы избежать `callback hell` (чрезмерной вложенности коллбеков) и сделать код более читаемым и управляемым.

### Создание `Promise`

Создать промис можно с помощью конструктора `new Promise`, который принимает функцию-исполнитель (`resolve`, `reject`).

```js
const myPromise = new Promise((resolve, reject) => {
  let success = true; // Или любое условие

  if (success) {
    resolve("✅ Операция выполнена успешно!");
  } else {
    reject("❌ Произошла ошибка.");
  }
});
```

---

### Состояния `Promise`

Промис может находиться в одном из трёх состояний:

- `pending` (ожидание) — начальное состояние, промис ещё не завершён
- `fulfilled` (исполнен) — операция завершена успешно, вызывается `resolve()`
- `rejected` (отклонён) — операция завершилась с ошибкой, вызывается `reject()`

**1. Состояние `pending` (ожидание)**. При создании новый Promise по умолчанию находится в состоянии ожидания. Это означает, что он ещё не завершился.

```js
const promise = new Promise(() => {}); // Никогда не завершится
console.log(promise); // Promise { <pending> }
```

Пока не вызваны `resolve()` или `reject()`, промис остаётся в **ожидании** (`pending`).

**2. Состояние `fulfilled` (успешное выполнение)**. Когда вызывается `resolve(value)`, промис переходит в состояние исполнен (`fulfilled`), а `value` передаётся в `.then()`.

```js
const promise = new Promise((resolve) => {
  setTimeout(() => resolve("🎉 Успех!"), 2000);
});

console.log(promise); // Promise { <pending> }

promise.then((result) => console.log(result)); // 🎉 Успех! (через 2 секунды)
```

После `resolve("🎉 Успех!")` промис становится **исполненным**.

**3. Состояние `rejected` (отклонён)**. Когда вызывается `reject(error)`, промис переходит в состояние отклонён (`rejected`), а `error` передаётся в `.catch()`.

```js
const promise = new Promise((_, reject) => {
  setTimeout(() => reject("❌ Ошибка!"), 2000);
});

console.log(promise); // Promise { <pending> }

promise.catch((error) => console.log(error)); // ❌ Ошибка! (через 2 секунды)
```

После `reject("❌ Ошибка!")` промис становится **отклонённым**.

#### Как `Promise` меняет состояние?

Промис может **изменить своё состояние только один раз** – из `pending` в `fulfilled` или `rejected`. После этого его состояние уже не меняется.

**Пример с одновременным `resolve()` и `reject()`:**

```js
const promise = new Promise((resolve, reject) => {
  resolve("✅ Успешно!");
  reject("❌ Ошибка!"); // Игнорируется, так как уже вызван resolve
});

promise
  .then((result) => console.log(result)) // ✅ Успешно!
  .catch((error) => console.log(error)); // Не сработает
```

Как только промис переходит в `fulfilled`, `reject()` больше не срабатывает.

---

### Методы обработки `Promise`

**`.then()` — обработка успешного выполнения**

```js
myPromise.then((result) => {
  console.log(result); // "✅ Операция выполнена успешно!"
});
```

**`.catch()` — обработка ошибок**

```js
myPromise
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.error(error);
  });
```

**`.finally()` — выполняется всегда**. Этот метод вызывается всегда, независимо от результата (`resolve` или `reject`).

```js
myPromise
  .then((result) => console.log(result))
  .catch((error) => console.error(error))
  .finally(() => console.log("⏳ Операция завершена."));
```

---

### Цепочка `Promise` (`Chaining`)

Цепочка `Promise` (`chaining`) — это техника, позволяющая последовательно выполнять несколько **асинхронных** операций, передавая результат одной операции в следующую.

#### Как работает цепочка `Promise`?

Каждый вызов `then()`, `catch()` или `finally()` возвращает новый промис, что позволяет выстраивать последовательные вызовы друг за другом.

```js
new Promise((resolve) => {
  resolve(1);
})
  .then((result) => {
    console.log(result); // 1
    return result * 2; // Возвращаем 2
  })
  .then((result) => {
    console.log(result); // 2
    return result * 3; // Возвращаем 6
  })
  .then((result) => {
    console.log(result); // 6
  });
```

**Что здесь происходит?**

- Создаётся промис и разрешается со значением 1.
- Первый `then()` получает 1 и возвращает 2.
- Второй `then()` получает 2 и возвращает 6.
- Третий `then()` получает 6 и выводит его в консоль.

#### Обработка ошибок в цепочке

Если в цепочке возникает ошибка, она автоматически передаётся в следующий `catch()`:

```js
new Promise((resolve, reject) => {
  reject("Ошибка на первом шаге!");
})
  .then((result) => {
    console.log(result); // Не выполнится
    return result * 2;
  })
  .catch((error) => {
    console.error("Поймали:", error); // Поймали: Ошибка на первом шаге!
    return 1; // Возвращаем 1, чтобы продолжить цепочку
  })
  .then((result) => {
    console.log(result); // 1
  });
```

#### Использование `finally()` в цепочке

Метод `finally()` вызывается **всегда**, вне зависимости от того, успешно или с ошибкой завершился промис.

```js
new Promise((resolve, reject) => {
  resolve("Все хорошо!");
})
  .then((result) => {
    console.log(result); // Все хорошо!
    return result;
  })
  .catch((error) => {
    console.error("Ошибка:", error); // Не выполнится
  })
  .finally(() => {
    console.log("Всегда выполняется!"); // Всегда выполняется!
  });
```

#### Практический пример: Запрос данных с API

```js
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json())
  .then((data) => {
    console.log("Пост:", data);
    return fetch("https://jsonplaceholder.typicode.com/users/" + data.userId);
  })
  .then((response) => response.json())
  .then((user) => {
    console.log("Автор:", user);
  })
  .catch((error) => {
    console.error("Ошибка запроса:", error);
  })
  .finally(() => {
    console.log("Запрос завершён");
  });
```

**Что делает этот код?**

- Получает пост по ID.
- Затем получает данные пользователя, связанного с этим постом.
- Обрабатывает ошибки, если запросы не удались.

---

### Параллельное выполнение `Promise`

Когда нужно запустить **несколько асинхронных операций одновременно**, используются специальные методы:

#### `Promise.all()` — выполняет все промисы и возвращает массив результатов.

```js
const p1 = new Promise((resolve) =>
  setTimeout(() => resolve("🍎 Apple"), 1000)
);
const p2 = new Promise((resolve) =>
  setTimeout(() => resolve("🍌 Banana"), 2000)
);
const p3 = new Promise((resolve) =>
  setTimeout(() => resolve("🍒 Cherry"), 500)
);

Promise.all([p1, p2, p3]).then((results) => console.log(results));
// ["🍎 Apple", "🍌 Banana", "🍒 Cherry"] (через 2 сек)
```

_P.S: Если хоть один промис отклонится, то `Promise.all()` вернёт `reject`_

#### `Promise.race()` — возвращает первый успешно завершённый промис.

```js
Promise.race([p1, p2, p3]).then((firstResult) => console.log(firstResult));
// "🍒 Cherry" (через 0.5 сек)
```

#### `Promise.any()` — возвращает первый успешный промис, игнорируя ошибки.

```js
const p4 = new Promise((_, reject) =>
  setTimeout(() => reject("Ошибка 1"), 500)
);
const p5 = new Promise((resolve) =>
  setTimeout(() => resolve("🎉 Победа!"), 1000)
);
const p6 = new Promise((_, reject) =>
  setTimeout(() => reject("Ошибка 2"), 1500)
);

Promise.any([p4, p5, p6]).then((result) => console.log(result));
// "🎉 Победа!" (через 1 сек)
```

#### `Promise.allSettled()` — возвращает все промисы, даже если некоторые отклонились.

```js
Promise.allSettled([p1, p4, p5]).then((results) => console.log(results));

// Результат

[
  { status: "fulfilled", value: "🍎 Apple" },
  { status: "rejected", reason: "Ошибка 1" },
  { status: "fulfilled", value: "🎉 Победа!" },
];
```

---

### Заключение

`Promise` — это мощный инструмент для работы с асинхронными операциями в `JavaScript`, который позволяет избежать вложенности коллбеков (`callback hell`) и сделать код более читаемым и управляемым.

Основные преимущества `Promise`:

- Упрощает обработку асинхронных задач, таких как запросы к серверу или таймеры.
- Позволяет цепочечно выстраивать операции с помощью `.then()`.
- Обеспечивает централизованную обработку ошибок через `.catch()`.
- Позволяет выполнить завершающие действия с `.finally()`, независимо от успеха или ошибки.

Использование `Promise` делает код структурированным, гибким и масштабируемым. В сочетании с `async/await`, который основан на `Promise`, можно писать асинхронный код, который выглядит как синхронный, улучшая его читаемость.
