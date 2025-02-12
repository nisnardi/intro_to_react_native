# Jest

## Crear tests

- Crear una carpeta con el nombre de `jest`.
- En esta carpeta vamos a poner los tests que creemos para testear nuestros ejercicios.
- En un projecto real generalmente los tests van donde están los ejercicios pero no tenemos configurado todo un projecto y para esta práctica así va a estar bien.
- Para poder testear los ejercicios vamos a necesitar exportar código de los ejercicios e importarlo en los tests.
- Podes hacer un repaso de lo visto en la sección módulos de JavaScript.
- Muchos tests no van a tener sentido o vamos a tener que modificar un poco para poder testearlos.
- La idea es practicar un poco y aprender como hacerlo. Lo más importante es practicar.
- Asegurate de tener instalado y configurado `jest` en esta carpeta para poder correr los tests como hicimos en la primer unidad de esta sección.
- Ahora a testear!!

```javascript
// ej1.js
// - Declarar una variable nombre
export var nombre;

// - Declarar una variable apellido
export var apellido;

// - Declarar una variable edad
export var edad;

// - Declarar una variable **fecha de nacimiento** utilizando camel case
export var fechaDeNacimiento;

// - Declarar una variable **direccion**
export var direccion;

// ej1.test.js
import {
  nombre,
  apellido,
  edad,
  fechaDeNacimiento,
  direccion,
} from "../js/ej1";

describe("Test Ej 1", () => {
  test("la variable nombre está declarada pero no tiene valor", () => {
    expect(nombre).toUndefined();
  });

  test("la variable apellido está declarada pero no tiene valor", () => {
    expect(apellido)toUndefined();
  });

  test("la variable edad está declarada pero no tiene valor", () => {
    expect(edad).toUndefined();
  });

  test("la variable fechaDeNacimiento está declarada pero no tiene valor", () => {
    expect(fechaDeNacimiento).toUndefined();
  });

  test("la variable direccion está declarada pero no tiene valor", () => {
    expect(direccion).toUndefined();
  });
});
```

- Para poder testear este código debemos usar `export` de las variables.
- Luego importamos las variables y verificamos que sean `undefined`.
- Está claro que no agrega mucho valor este test pero.. hicimos un test!
- Al correr el test con `npm test ej1.test.js` Deberíamos obtener el siguiente resultado:

```bash
> test
> jest ej1.test.js

 PASS  ./ej1.test.js
  Test Ej 1
    ✓ la variable nombre está declarada pero no tiene valor (1 ms)
    ✓ la variable apellido está declarada pero no tiene valor
    ✓ la variable edad está declarada pero no tiene valor
    ✓ la variable fechaDeNacimiento está declarada pero no tiene valor
    ✓ la variable direccion está declarada pero no tiene valor

Test Suites: 1 passed, 1 total
Tests:       5 passed, 5 total
Snapshots:   0 total
Time:        0.337 s
```

- Hagamos el ejercicio 2:

```javascript
// ej2.js

// * Declarar las siguientes variables de forma individual:
//   * nombre
var nombre;
//   * apellido
var apellido;
//   * edad
var edad;
//   * fecha de nacimiento
var fechaDeNacimiento;
//   * direccion
var direccion;

// * Asignar un valor a cada variable con tus datos personales:
//   * Tu nombre
nombre = "Leandro";
//   * Tu apellido
apellido = "Paredes";
//   * Tu edad
edad = 30;
//   * Tu fecha de nacimiento
fechaDeNacimiento = "29/06/1994";
//   * Tu direccion
direccion = "Roma 123";

export default {
  nombre,
  apellido,
  edad,
  fechaDeNacimiento,
  direccion,
};

// ej2.test.js
import Variables from "../js/ej2";

describe("Test Ej 2", () => {
  test("la variable nombre está declarada y tiene valor", () => {
    expect(Variables.nombre).toBe("Leandro");
  });

  test("la variable apellido está declarada y tiene valor", () => {
    expect(Variables.apellido).toBe("Paredes");
  });

  test("la variable edad está declarada y tiene valor", () => {
    expect(Variables.edad).toBe(30);
  });

  test("la variable fechaDeNacimiento está declarada y tiene valor", () => {
    expect(Variables.fechaDeNacimiento).toBe("29/06/1994");
  });

  test("la variable direccion está declarada y tiene valor", () => {
    expect(Variables.direccion).toBe("Roma 123");
  });
});
```

- En este caso utilizamos `export default {}` para exportar las variables y los valores asignados.
- Luego verificamos que el contenido de las variables sea el esperado.
- Cualquier valor que cambie en el código va a romper este test.
- Al ejecutarlo obtenemos el siguiente resultado:

```bash
> test
> jest ej2.test.js

 PASS  ./ej2.test.js
  Test Ej 1
    ✓ la variable nombre está declarada pero no tiene valor (1 ms)
    ✓ la variable apellido está declarada pero no tiene valor
    ✓ la variable edad está declarada pero no tiene valor
    ✓ la variable fechaDeNacimiento está declarada pero no tiene valor
    ✓ la variable direccion está declarada pero no tiene valor

Test Suites: 1 passed, 1 total
Tests:       5 passed, 5 total
Snapshots:   0 total
Time:        0.241 s, estimated 1 s
Ran all test suites matching /ej2.test.js/i.
```

- Ayuda: Ejercicios 3 y 4 son muy parecidos al 2.
- En el ejercicio 5 tenemos una nueva dificultad y es que utilizamos `console.log` para mostrar los valores.
- Necesitamos encontrar una forma de testear esto:

```javascript
// ej5test.js
// * Declarar las siguientes variables de forma individual y asignarle a cada una un valor para describirte:
//   * nombre
var nombre = "Leandro";
//   * apellido
var apellido = "Paredes";
//   * edad
var edad = 30;
//   * fecha de nacimiento
var fechaDeNacimiento = "29/06/1994";
//   * direccion
var direccion = "Roma 123";

// * Mostrar en consola el **valor** de cada una de las variables utilizando `console.log()`
export function mostrarValores() {
  console.log(nombre);
  console.log(apellido);
  console.log(edad);
  console.log(fechaDeNacimiento);
  console.log(direccion);
}

//ej5.test.js
import { mostrarValores } from "../js/ej5test";

const log = jest.spyOn(console, "log").mockImplementation(() => {});

describe("Test Ej 5", () => {
  test("se muestran los valores en pantalla", () => {
    mostrarValores();

    expect(log).toHaveBeenCalledTimes(5);
    expect(log).toHaveBeenCalledWith("Leandro");
    expect(log).toHaveBeenCalledWith("Paredes");
    expect(log).toHaveBeenCalledWith(30);
    expect(log).toHaveBeenCalledWith("29/06/1994");
    expect(log).toHaveBeenCalledWith("Roma 123");
  });
});
```

- Para este caso podemos utilizar otra forma para testear el código.
- Modifiqué la versión del ejercicio para utilizar una función en lugar de solo usar console.log().
- Exporto la función para poder importarla y ejecutarla en el test.
- Dado que el código usa console.log para mostrar los valores podemos `mockear` el objeto `console` y sobrecribir como funciona el método `log`.
- Cuando corremos este test `console.log` va a ser una función de `jest`.
- Con este `mock` podemos preguntarle a `jest` si console.log fué llamado una cantidad de veces esperadas.
- También si fué llamado pasandole los parámetros esperados.
- Ahora que ya tenemos varios tests podemos correrlos todos juntos utilizando el siguiente comando `npm test .`
- llamamos a `npm test` como siempre pero utilizamos el concepto de `.` para decirle que corra todos los tests que hay en esta carpeta.

```bash
npm test .

> test
> jest .

 PASS  ./ej2.test.js
 PASS  ./ej5.test.js
 PASS  ./ej1.test.js

Test Suites: 5 passed, 5 total
Tests:       13 passed, 13 total
Snapshots:   0 total
Time:        0.342 s, estimated 1 s
Ran all test suites matching /./i.
```

- También podemos utilizar `npm test -- --watch` para correr `jest` en modo `watch`.
- Dado que estamos corriendo un script de `package.json` tenemos que utilizar `--` para decirle que eso es un parámetro del comando `jest` que agregamos el script `npm test`.
- En este caso `jest` va a estar corriendo todo el tiempo y escuchando por cualquier cambio en los tests.

```bash
 PASS  ./ej2.test.js
 PASS  ./ej1.test.js
 PASS  ./ej5.test.js

Test Suites: 4 passed, 4 total
Tests:       12 passed, 12 total
Snapshots:   0 total
Time:        0.388 s, estimated 1 s
Ran all test suites related to changed files.

Watch Usage
 › Press a to run all tests.
 › Press f to run only failed tests.
 › Press p to filter by a filename regex pattern.
 › Press t to filter by a test name regex pattern.
 › Press q to quit watch mode.
 › Press Enter to trigger a test run.
```

- Al correr `jest` en modo `watch` corre todos los tests y nos da la opción de apretar algunas teclas para filtrar que tests correr.
- Usando `p` podemos poner le nombre del test que queremos ver.
- `jest` pregunta cual es el `pattern` porque espera una regular expression pero podemos poner el nombre del test.
- Por ejemplo ingresamos `ej2` y debería correr todos los tests de ese archivo.
- `jest` va a correr todos los tests que encuentre que hagan match con ese patrón.

```bash
 PASS  ./ej2.test.js
  Test Ej 2
    ✓ la variable nombre está declarada y tiene valor (2 ms)
    ✓ la variable apellido está declarada y tiene valor
    ✓ la variable edad está declarada y tiene valor
    ✓ la variable fechaDeNacimiento está declarada y tiene valor (1 ms)
    ✓ la variable direccion está declarada y tiene valor

Test Suites: 1 passed, 1 total
Tests:       5 passed, 5 total
Snapshots:   0 total
Time:        0.356 s, estimated 1 s
Ran all test suites matching /ej2/i.

Watch Usage: Press w to show more.
```

- Podemos presionar `w` para ver las opciones de nuevo.
- Podems presionar `q` para salir de la ejecución del `watch`.
- Con lo aprendido ya podemos hacer muchos tests de los ejercicios que hicimos pero seguro salgan algunas dudas.
- Preguntar al profe, a los compañeros, [leer la API](https://jestjs.io/docs/api) de Jest o consultar online sería el siguiente paso!
- Ahora a crear TESTS!!!

![Green tests](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExdXZ2b2xqMm92N3dhZzJnYmdnOHdpcmNlYjNwb2RiaHJ5a21qOGJ6OSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3og0IQsupJLxzqSbmM/giphy.gif)
