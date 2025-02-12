# Jest

## Testeando código async

- Hasta ahora vimos varias formas de comparar valores entre nuestro código y el resultado esperado.
- En general nos basamos en código que corre de manera sincrónica sin meternos con por ejemplo.. `Promises`... they are back!!
- Testear código asincrónico muchas veces es más complicado porque los valores no existen hasta que alguna condición ocurra o pase una cantidad de tiempo.
- Los tests tienen 5 segundos de ejecución como vimos y sino tiran un error por sobrepasar ese límite.
- Es por eso que `jest` tiene algunas formas de ayudarnos a testear código asincrónico.

```javascript
function fetchDatos() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("todo bien"), 4000);
  });
}

test("Test async", () => {
  return fetchDatos().then((mensaje) => {
    expect(mensaje).toBe("todo bien");
  });
});
```

- En este caso vemos como podemos demorar la ejecución de un test donde una `Promise` va a tomar un tiempo determinado en devolver un valor.
- Usando `then` podemos entonces hacer el `expect` para comparar el valor devuelto por la `Promise`.
- En `jest` también podemos utilizar el concepto de `async & await`.
- Si recordamos el concepto para poder utilizar `await` dentro de una función, debemos declarar a la función como `async`.
- En los tests podemos utilizar el `callback` del test como función `async` y luego usar `await` para esperar la resolución de la promesa de nuestro código y comparar valores.

```javascript
function fetchDatos() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("todo bien"), 4000);
  });
}

test("Test async", async () => {
  const mensaje = await fetchDatos();
  expect(mensaje).toBe("todo bien");
});
```

- Tambíen podemos testear casos de error de la siguiente manera:

```javascript
function fetchDatos() {
  return new Promise((resolve, reject) => {
    setTimeout(() => reject("Error"), 4000);
  });
}

test("Test async", () => {
  expect.assertions(1);
  return fetchDatos().catch((error) => {
    expect(error).toBe("Error");
  });
});
```

- En este caso utilizamos `expect.assertions(1)` para decirle a `jest` la cantidad de comparaciones que tiene el test para ser válido.
- Esto funciona mucho para testear código async ya que puede no pasar por el expect y mostrar el test como exitoso.

```javascript
function fetchDatos() {
  return new Promise((resolve, reject) => {
    setTimeout(() => reject("Error"), 4000);
  });
}

test("Test async", async () => {
  expect.assertions(1);

  try {
    await fetchDatos();
  } catch (error) {
    expect(error).toBe("Error");
  }
});
```

- También podemos utilizar `async & awaits` con `.resolves()` o `.rejects()`

```javascript
function fetchDatos() {
  return new Promise((resolve, reject) => {
    setTimeout(() => reject("Error"), 4000);
  });
}

test("Test async", async () => {
  expect.assertions(1);

  await expect(fetchDatos()).rejects.toBe("Error");
});
```

```javascript
function fetchDatos() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve("Todo Bien"), 4000);
  });
}

test("Test async", async () => {
  expect.assertions(1);

  await expect(fetchDatos()).resolves.toBe("Todo Bien");
});
```

- `jest` también tiene una función `done` que permite informar que un test terminó.
- El test corre y termina rápido pero por ahí el código no termino de ejecutarse como corresponde.
- Para informarle a `jest` que el test terminó podemos utilizar la palabra `done`.

```javascript
test("Test callbacks", () => {
  setTimeout(() => {
    expect(2).toBe(2);
  }, 2000);
});
```

- Este código tira el siguiente error `"Exceeded timeout of 5000 ms for a test while waiting for `done()` to be called.`.
- Podemos entonces informarle a `jest` el momento de terminar la ejecución usando `done`.

```javascript
test("Test callbacks", (done) => {
  setTimeout(() => {
    expect(2).toBe(2);
    done();
  }, 2000);
});
```

- Ahora llamando a la función `done()` le decimos a `jest` que la ejecución de este test finalizó.
- Done nos ayuda a testear código asincrónico que no utiliza promesas.
- `jest` espera que el callback `done` sea llamado para entender que debe pasar al próximo test.
- En caso de que no llamemos a `done`, Jest va a seguir esperando la resolución del test y tira un error de Timeout.
