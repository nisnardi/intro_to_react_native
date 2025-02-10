# Jest

## Creando Tests

- `jest` tiene una función con el nombre de `test`.
- Esta función también se puede llamar como `it`.
- `jest` necesita que exista un `test` en el archivo para poder correrlo.
- `test` acepta como primer parámetro el nombre o descripción del test y un `callback` como segundo parámetro.
- El segundo parámetro (`callback`) es la función que se va a ejecutar como test.
- Dentro del test podemos utilizar la palabra `expect` para testear un valor.
- `expect` se utiliza con un `matcher` para evaluar un valor.
- Por ejemplo podemos utilizar `expect(algo).toBe(algo)`, es decir espero que tal cosa sea el valor esperado.
- El valor que le pasamos a la función `expect` tiene que ser el nuestro código que queremos testear.
- El parámetro que le pasamos al matcher tiene que ser el valor esperado.
- Por convención podemos utilizar `archivo.spec|test.js` para nuestro test

```javascript
test("Testear que verdadero sea igual que verdadero", () => {
  expect(true).toBe(true);
});
```

- En este caso tenemos un test que va a probar que true sea true (no muy útil).
- Lo podemos pensar de la siguiente forma:

```javascript
test("Testear que verdadero sea igual que verdadero", () => {
  const valorQueQuieroTestear = true;
  const valorEsperado = true;

  expect(valorQueQuieroTestear).toBe(valorEsperado);
});
```

- Si el valor testeado devuelve el valor esperado entonces el test pasa o es correcto.
- Puede ser que el valor esperado no sea el mismo que el retornado por nuestro código.
- En este caso el test falla o es incorrecto.

```javascript
test("Testear que verdadero sea igual que verdadero", () => {
  const valorQueQuieroTestear = true;
  const valorEsperado = false;

  expect(valorQueQuieroTestear).toBe(valorEsperado);
});
```

- Cuando el test no pasa, `jest` nos muestra el nombre del test y la razón por la que no pasó.

```bash
 FAIL  ./ejemplo.spec.js
  ✕ Testear que verdadero sea igual que verdadero (2 ms)

  ● Testear que verdadero sea igual que verdadero

    expect(received).toBe(expected) // Object.is equality

    Expected: false
    Received: true

      29 |   const valorEsperado = false;
      30 |
    > 31 |   expect(valorQueQuieroTestear).toBe(valorEsperado);
         |                                 ^
      32 | });
      33 |

      at Object.toBe (ejemplo.spec.js:31:33)

Test Suites: 1 failed, 1 total
Tests:       1 failed, 1 total
Snapshots:   0 total
Time:        0.249 s
Ran all test suites matching /ejemplo.spec.js/i.
```

- Para arreglar este test debemos cambiar el valor valorEsperado a true

```javascript
test("Testear que verdadero sea igual que verdadero", () => {
  const valorQueQuieroTestear = true;
  const valorEsperado = true;

  expect(valorQueQuieroTestear).toBe(valorEsperado);
});
```

- Con este cambio nuestros test vuelve a pasar

```bash
> test
> jest ejemplo.spec.js

 PASS  ./ejemplo.spec.js
  ✓ Testear que verdadero sea igual que verdadero (1 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.273 s, estimated 1 s
Ran all test suites matching /ejemplo.spec.js/i.
```

- TDD (Test Driven Design) es una técnica que nos permite escribir un test para el código que vamos a escribir.
- El test inicialmente no pasa y tenemos que seguir escribiendo el código hasta que pase.
- Es lo que se conoce muchas veces como red, red, green donde red es que no pasa y green es que el test pasó.
- Seguimos iterando entre que los tests no pasen hasta que pase.
- En general solemos escribir varios tests para testear algún código.
- Muchas veces necesitamos agrupar los tests y ahí es donde entra en juego la función `describe` que nos provee `jest`.
- `describe` al igual que `test` obtiene como primer parámetro el nombre o descripción y como segundo parámetro un callback.
- Dentro del callback podemos agregar todos los `test o it` que necesitemos.
- Utilizamos `describe` para agrupar tests por algún concepto

```javascript
describe("Modulo Suma", () => {
  test("Sumar 2 + 2 siempre devuelve 4", () => {
    expect(2 + 2).toBe(4);
  });

  test("Sumar 2 como string y 2 como número devuelve 22", () => {
    expect(2 + "2").toBe("22");
  });
});

describe("Modulo Resta", () => {
  test("restar un número más grande a un número más chico da siempre un numero negativo", () => {
    expect(2 - 8).toBe(-6);
  });
});
```

```bash
> test
> jest ejemplo.test.js

 PASS  ./ejemplo.test.js
  Modulo Suma
    ✓ Sumar 2 + 2 siempre devuelve 4 (1 ms)
    ✓ Sumar 2 como string y 2 como número devuelve 22
  Modulo Resta
    ✓ restar un número más grande a un número más chico da siempre un numero negativo

Test Suites: 1 passed, 1 total
Tests:       3 passed, 3 total
Snapshots:   0 total
Time:        0.228 s, estimated 1 s
Ran all test suites matching /ejemplo.test.js/i
```

- En este ejemplo vemos como `describe` muestra un título como puede ser Modulo Suma y luego el resultado de cada `test`.
- En algunos casos vamos a querer saltear o `skip` un test y podemos hacer esto utilizando `test.skip`.

```javascript
describe("Modulo Suma", () => {
  test("Sumar 2 + 2 siempre devuelve 4", () => {
    expect(2 + 2).toBe(4);
  });

  test.skip("Sumar 2 como string y 2 como número devuelve 22", () => {
    expect(2 + "2").toBe("22");
  });
});

describe("Modulo Resta", () => {
  test("restar un número más grande a un número más chico da siempre un numero negativo", () => {
    expect(2 - 8).toBe(-6);
  });
});
```

```bash
> test
> jest ejemplo.test.js

 PASS  ./ejemplo.test.js
  Modulo Suma
    ✓ Sumar 2 + 2 siempre devuelve 4 (1 ms)
    ○ skipped Sumar 2 como string y 2 como número devuelve 22
  Modulo Resta
    ✓ restar un número más grande a un número más chico da siempre un numero negativo

Test Suites: 1 passed, 1 total
Tests:       1 skipped, 2 passed, 3 total
Snapshots:   0 total
Time:        0.218 s, estimated 1 s
Ran all test suites matching /ejemplo.test.js/i.
```

- `jest` utiliza `○` para decirnos que un test fue salteado.
- `jest` también nos muestra la cantidad de tests que fueron salteados: `Tests: 1 skipped, 2 passed, 3 total`.
- En algunos casos queremos saltear varios tests juntos y en lugar de agregar `.skip` a cada uno podemos agregarlo a `describe` y saltear todos los tests.

```javascript
describe.skip("Modulo Suma", () => {
  test("Sumar 2 + 2 siempre devuelve 4", () => {
    expect(2 + 2).toBe(4);
  });

  test("Sumar 2 como string y 2 como número devuelve 22", () => {
    expect(2 + "2").toBe("22");
  });
});

describe("Modulo Resta", () => {
  test("restar un número más grande a un número más chico da siempre un numero negativo", () => {
    expect(2 - 8).toBe(-6);
  });
});
```

```bash
> test
> jest ejemplo.test.js

 PASS  ./ejemplo.test.js
  Modulo Suma
    ○ skipped Sumar 2 + 2 siempre devuelve 4
    ○ skipped Sumar 2 como string y 2 como número devuelve 22
  Modulo Resta
    ✓ restar un número más grande a un número más chico da siempre un numero negativo (1 ms)

Test Suites: 1 passed, 1 total
Tests:       2 skipped, 1 passed, 3 total
Snapshots:   0 total
Time:        0.226 s, estimated 1 s
Ran all test suites matching /ejemplo.test.js/i.
```

- En este ejemplo vemos como los tests de `Modulo Suma` no fueron ejecutados.
- Otra opción es utilizar `.only` para establecer que sólo queremos correr un test.

```javascript
describe("Modulo Suma", () => {
  test("Sumar 2 + 2 siempre devuelve 4", () => {
    expect(2 + 2).toBe(4);
  });

  test.only("Sumar 2 como string y 2 como número devuelve 22", () => {
    expect(2 + "2").toBe("22");
  });
});

describe("Modulo Resta", () => {
  test("restar un número más grande a un número más chico da siempre un numero negativo", () => {
    expect(2 - 8).toBe(-6);
  });
});
```

```bash
> test
> jest ejemplo.test.js

 PASS  ./ejemplo.test.js
  Modulo Suma
    ✓ Sumar 2 como string y 2 como número devuelve 22 (1 ms)
    ○ skipped Sumar 2 + 2 siempre devuelve 4
  Modulo Resta
    ○ skipped restar un número más grande a un número más chico da siempre un numero negativo

Test Suites: 1 passed, 1 total
Tests:       2 skipped, 1 passed, 3 total
Snapshots:   0 total
Time:        0.335 s, estimated 1 s
Ran all test suites matching /ejemplo.test.js/i.
```

- Esto tambien funciona con `describe` y podemos utilizar `describe.only` para ejecutar solo los tests que estén dentro de ese discribe.

```javascript
describe("Modulo Suma", () => {
  test("Sumar 2 + 2 siempre devuelve 4", () => {
    expect(2 + 2).toBe(4);
  });

  test("Sumar 2 como string y 2 como número devuelve 22", () => {
    expect(2 + "2").toBe("22");
  });
});

describe.only("Modulo Resta", () => {
  test("restar un número más grande a un número más chico da siempre un numero negativo", () => {
    expect(2 - 8).toBe(-6);
  });
});
```

```bash
> test
> jest ejemplo.test.js

 PASS  ./ejemplo.test.js
  Modulo Suma
    ○ skipped Sumar 2 + 2 siempre devuelve 4
    ○ skipped Sumar 2 como string y 2 como número devuelve 22
  Modulo Resta
    ✓ restar un número más grande a un número más chico da siempre un numero negativo (1 ms)

Test Suites: 1 passed, 1 total
Tests:       2 skipped, 1 passed, 3 total
Snapshots:   0 total
Time:        0.224 s, estimated 1 s
Ran all test suites matching /ejemplo.test.js/i.
```

- Otra opción es utilizar `test.todo` para establecer que hay un test que queremos o necesitamos crear pero todavía no está listo para ser ejecutado.

```javascript
describe("Modulo Suma", () => {
  test("Sumar 2 + 2 siempre devuelve 4", () => {
    expect(2 + 2).toBe(4);
  });

  test("Sumar 2 como string y 2 como número devuelve 22", () => {
    expect(2 + "2").toBe("22");
  });
});

describe.only("Modulo Resta", () => {
  test("restar un número más grande a un número más chico da siempre un numero negativo", () => {
    expect(2 - 8).toBe(-6);
  });
  test.todo("Restar un string y un número para ver que pasa");
});
```

```bash
> test
> jest ejemplo.test.js

 PASS  ./ejemplo.test.js
  Modulo Suma
    ○ skipped Sumar 2 + 2 siempre devuelve 4
    ○ skipped Sumar 2 como string y 2 como número devuelve 22
  Modulo Resta
    ✓ restar un número más grande a un número más chico da siempre un numero negativo (1 ms)
    ✎ todo Restar un string y un número para ver que pasa

Test Suites: 1 passed, 1 total
Tests:       2 skipped, 1 todo, 1 passed, 4 total
Snapshots:   0 total
Time:        0.304 s, estimated 1 s
Ran all test suites matching /ejemplo.test.js/i.
```

- También en algunos casos podemos establecer un límite de tiempo de ejecución a un test.
- Si la ejecución del test supera al establecido entonces el test no pasa.
- `test(mensaje, callback, timeout)`
- Por defecto `jest` utiliza 5 segundos como default.
- Es importante a la hora de crear tests tener cuidado como es la ejecución del código.
- En algún momento les puede pasar que un test necesita más tiempo para ejecutarse y pueden cambiar el valor.
- No es recomendado hacer esto ya que sino los tests tardan muchísimo tiempo en correr y en algún momento se deja de correrlos.

```javascript
// Solo de ejemplo, este test se ejecuta super rápido
const timeout = 1;
const callback = () => {
  expect(2 + 2).toBe(4);
};

test("Sumar 2 + 2 siempre devuelve 4", callback, timeout);
```

- También podemos ejecutar algún código en las siguientes situaciones:
  - afterAll(callback) / Después de todos los tests
  - afterEach(callback) / Después de cada test
  - beforeAll(callback) / Antes de todos los tests
  - beforeEach(callback) / Antes de cada test
- Estas funciones se utilizan para cosas como setear el ambiente necesario para el test, cargar datos en la base de datos o alguna tarea similar.
- También se pueden utilizar para borrar datos de la base de datos o volver a establecer el entorno como estaba antes de la ejecución.
- La idea de los tests es que no dependan unos de otros y que todos se ejecuten un un ambiente establecido.

```javascript
beforeAll(() => {
  console.log("Se ejecuta antes que todos los tests y sólo una vez");
});

beforeEach(() => {
  console.log("Se ejecuta antes de cada test");
});

afterEach(() => {
  console.log("Se ejecuta después de cada test");
});

afterAll(() => {
  console.log("Se ejecuta después de todos los test");
});

describe("Modulo Suma", () => {
  test("Sumar 2 + 2 siempre devuelve 4", () => {
    expect(2 + 2).toBe(4);
  });

  test("Sumar 2 como string y 2 como número devuelve 22", () => {
    expect(2 + "2").toBe("22");
  });
});

describe("Modulo Resta", () => {
  test("restar un número más grande a un número más chico da siempre un numero negativo", () => {
    expect(2 - 8).toBe(-6);
  });
  test.todo("Restar un string y un número para ver que pasa");
});
```
