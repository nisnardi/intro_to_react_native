# JavaScript

## Hoisting

- JavaScript utiliza lo que se conoce como `JIT` que es `Just In Time` donde el código es traducido desde el lenguaje a lenguaje de máquina en lo que se conoce como `runtime` o ejecución.
- Este proceso no se hace previo a ejecutar el código.
- Esto tiene el beneficio de ser un lenguaje interpretado y compilación antes de ejecución o tiempo (AOT)
- Dado que el lenguaje funciona así hay algunas cosas que tenemos que entender

```javascript
// Error ReferenceError: nombre is not defined
console.log(nombre);
```

- Cuando ejecutamos este código obtenemos el mensaje `Error ReferenceError: nombre is not defined` y significa que la variable nombre no fue definida.
- Para solucionar este problema definimos la variable antes de utilizarla.
- Es una buena práctica en programación declarar las variables y funciones antes de utilizarlas pero JavaScript nos permite hacerlo de otra manera.

```javascript
console.log(nombre);
var nombre = "Nicolas";
```

- En este este ejemplo no obtenemos un error sino que la variable nombre contiene un valor `undefined`.
- Esto significa que la posción de memoria fué reservada pero se le asignó un valor de `undefined`.
- En el caso anterior la variable estaba definida.
- Esto sucede ya que el motor de JavaScript va a asignar un valor de undefined y declarar la variable `nombre` primero y por eso la puede utilizar aún si la llamamos antes de su declaración.
- De alguna forma es como si el motor hace esto:

```javascript
var nombre = undefined;
console.log(nombre);
nombre = = "Nicolas";
```

- Esto puede traer algunos errores por el simple echo de intentar que los programadores usaran variables de cualquier forma para hacerlo más fácil en un inicio.
- También pasa con funciones donde el motor prepara todo para que puedan ser utilizadas.
- Si bien como dijimos esto es una mala práctica es posible.

```javascript
saludar();

function saludar() {
  console.log("Hola");
}
```

- También pasa lo mismo dentro de las funciones.
- Si declaramos una variable utilizando var dentro de una función podemos obtener el mismo resultado.

```javascript
function saludar() {
  console.log(nombre);

  var nombre = "Nicolas";
}

saludar();
```

- Este código no tira error pero la variable `nombre` tiene asignado un valor `undefined`.
- Este problema no pasa si utilizamos funciones anónimas o como expresión.

```javascript
saludar();
console.log(saludarExpresion);
saludarExpresion();

// Hoisted
function saludar() {
  console.log("Hola");
}

// saludarExpresion is not a function
var saludarExpresion = function () {
  console.log("Hola");
};
```

- En este ejemplo la función `saludarExpresion` es declarada utilizando un valor undefined y después lo tratamos de ejecutar como si fuera una función y por eso obtenemos el error de `saludarExpresion` is not a function porque no lo es al momento de ser utilizada.
- En este ejemplo la consola muestra `undefined` cuando tratamos de ver el valor que tiene la variable `saludarExpresion`.
- Muchas veces el problema se da con usar `var` para declarar variables.
- Utilzar `let & const` nos ayuda a prevenir el error de obtener un valor inicial de undefined cuando las utilizamos antes de ser inicializadas.
- Esto pasa tanto en el ámbito global como dentro de una función o bloque.

```javascript
console.log(nombre);
// ReferenceError: Cannot access 'apellido' before initialization
console.log(apellido);

var nombre = "Nicolas";
let apellido = "Isnardi";
```

- Acá vemos que `let` no está inicializada, es decir, la variable fue declarada pero no se le asignó el valor `undefined` y no la podemos utilizar hasta que le asignemos algún valor;
- Esta mejora nos fuerza a declarar y asignar las variables antes de utilizarlas.
- Para evitar problemas la regla dice utilizar siempre `let o const` antes que `var`.
- También declarar las variables y preferentemente asignar un valor antes de ser utilizadas.
- Para aprender más sobre Hoisting podes leer la documentación sobre [Hoisting en MDN](https://developer.mozilla.org/es/docs/Glossary/Hoisting)
