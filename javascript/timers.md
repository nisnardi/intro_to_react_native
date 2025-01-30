# JavaScript

## Timers

- Existen las funciones `setTimeout` y `setInterval` que nos permiten retrasar la ejecución de un código que nosotros elegimos.

### setTimeout / clearTimeout

- Esta función se utiliza cuando queremos que nuestro código se ejecute **una sola vez** en un tiempo establecido.
- Acepta como primer parámetro la función que queremos que se ejecute.
- El segundo parámetro acepta un valor numérico con la cantidad de milisegundos que queremos esperar para ejecutar la función pasada como primer parámetro.

**Ejemplo:**

```js
const saludar = function () {
  console.log("hola");
};

setTimeout(saludar, 5000);
```

- En este ejemplo establecemos que queremos ejecutar la función saludar dentro de 5 segundos una sola vez.
- Si queremos podemos no utilizar la variable saludar y pasar la función anónima directamente.

**Ejemplo:**

```js
setTimeout(function () {
  console.log("hola");
}, 5000);
```

- Esta función retorna un valor numérico que es el ID.
- Podemos cortar la ejecución de este `setTimeout` utilizando la función `clearTimeout`.
- Esta función espera un valor numérico como parámetro.

**Ejemplo:**

```js
var idTimeOut = setTimeout(function () {
  console.log("hola");
}, 5000);

// Cortamos la ejecución
clearTimeout(idTimeOut);
```

- En algunos casos podemos necesitar tener que pasarle parámetros a la función que se va a ejecutar.
- Esta función acepta todos los parámetros que queremos de la segunda posición en adelante y los pasa como parámetros de la función que se ejecuta.

**Ejemplo:**

```js
const saludar = function (nombre, apodo) {
  console.log(`hola ${nombre} ${apodo}`);
};

setTimeout(saludar, 5000, "Marta", "Martita");
```

- En este ejemplo vemos que podemos pasarle más de un parámetro a la función saludar desde la función `setTimeout`.

### setInterval / clearInterval

- Existe otra función que se llama `setInterval` que nos permite ejecutar una función múltiples veces cada una cantidad establecida de tiempo.
- Es similar a `setTimeout` con la diferencia que se ejecuta múltiples veces.
- Retorna un valor numérico que se utiliza como ID.

**Ejemplo:**

```js
const saludar = function () {
  console.log("hola");
};

const id = setInterval(saludar, 1000);
```

- En este caso se va a llamar a la función **saludar** cada 1 segundo.
- Este llamado se hace hasta que cortemos la ejecución.
- Podemos utilizar la función `clearInterval` para anular el llamado de `setInterval`.

**Ejemplo:**

```js
const saludar = function () {
  console.log("hola");
};

const id = setInterval(saludar, 1000);

// se corta la ejecución
clearInterval(id);
```

- También podemos pasarle parámetros de la misma forma que a `setTimeout`.

**Ejemplo:**

```js
const saludar = function (nombre, apodo) {
  console.log(`hola ${nombre} ${apodo}`);
};

setInterval(saludar, 1000, "Marta", "Martita");
```

#### Practica

- [Ejercicio 186](../ejercicios/consignas/js/ej186.md)
- [Ejercicio 187](../ejercicios/consignas/js/ej187.md)
- [Ejercicio 188](../ejercicios/consignas/js/ej188.md)
