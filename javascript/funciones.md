# JavaScript

## Funciones

- En ECMAScript las **funciones son un tipo de dato**
- Las utilizamos para agrupar funcionalidad para utilizarlo todas las veces que necesite
- Utilizamos la palabra reservada **function** para declarar una función
- Para **ejecutar** una función primero la tengo que declarar
- Podemos **ejecutar** las funciones utilizando el **nombre de la función y paréntesis**

**Ejemplo:**

```js
function saludar() {
  console.log("hola");
}

saludar(); // Muestra en consola hola
saludar(); // Muestra en consola hola
```

- En este ejemplo vemos que podemos definir una función con el nombre **saludar** y luego la utilizamos llamandola con el **nombre y los paréntesis**
- Podemos utilizar una función tantas veces como lo necesitemos
- Cuando vemos que estamos repitiendo código es un caso común donde podemos refactorizar y abstraer ese código en una función
- También el uso de funciones nos hace más fácil testear nuestro código

#### Prácticas

- [Ejercicio 100](../ejercicios/consignas/js/ej100.md)
- [Ejercicio 101](../ejercicios/consignas/js/ej101.md)

- Dado que las funciones en ECMASCript son un tipo de dato lo podemos asignar a una variable
- Al asignar una función a una variable no necesitamos darle un nombre ya que para eso podemos utilizar la variable
- Las **funciones** que no tienen nombre se denominan **anónimas**

**Ejemplo:**

```js
// Al asignar una función a una variable no hace falta ponerle nombre a la función
const saludar = function () {
  console.log("hola");
};

saludar(); // Muestra en consola hola
saludar(); // Muestra en consola hola
```

- En este ejemplo declaramos la variable **saludar** y le asignamos un tipo de dato **function**
- La asignación funciona de la misma forma que si fuera cualquier otro tipo de dato (string, number, boolean y ahora function)

#### Prácticas

- [Ejercicio 102](../ejercicios/consignas/js/ej102.md)
- [Ejercicio 103](../ejercicios/consignas/js/ej103.md)
- [Ejercicio 104](../ejercicios/consignas/js/ej104.md)

- Una función puede o no retornar un valor
- Cuando una función no retorna un valor obtenemos **undefined** como se ve al ejecutar `console.log()` en la consola
- Para retornar un valor utilizamos la palabra reservada **return** dentro de la función

**Ejemplo:**

```js
function obtenerSaludo() {
  return "hola";
}

// obtenerSaludo retorna un tipo de dato string y lo podemos mostrar en console.log()
console.log(obtenerSaludo());

// Podemos guardar el valor retornado de una función en una variable y luego utilizarlo
const saludo = obtenerSaludo();
console.log(saludo);
```

- Una función puede retornar cualquier tipo de dato

**Ejemplo:**

```js
function conseguirLaEdadDelUsuario() {
  return 30;
}

function usuarioLoggeado() {
  return true;
}
```

- Dado que las funciones retornan un valor podemos utilizar estos valores en los condicionales de ser necesarios

**Ejemplo:**

```js
function conseguirLaEdadDelUsuario() {
  return 30;
}

function usuarioLoggeado() {
  return true;
}

if (conseguirLaEdadDelUsuario() >= 18) {
  console.log("El usuario es mayor de 18");
}

if (usuarioLoggeado()) {
  console.log("Bienvenido usuario a nuestro sitio");
}
```

- En el primer caso la función retorna un valor numérico por lo cual podemos compararlo y obtener un resultado booleand true/false según el valor retornado por la función
- En el segundo caso una función puede retornar un valor boolean directamente y lo podemos utilizar como condición. Si el usuario está loggeado podemos saludarlo

#### Prácticas

- [Ejercicio 105](../ejercicios/consignas/js/ej105.md)
- [Ejercicio 106](../ejercicios/consignas/js/ej106.md)

- Las funciones también aceptan uno o varios valores como parametros
- Utilizando parametros hacemos que nuestras funciones sean más flexibles y le podemos dar más funcionalidades
- Al declarar una función podemos establecer la cantidad de parámetros que acepta esa función y ponerles un nombre a cada uno
- Dentro de la función podemos interactuar con los parámetros

**Ejemplo:**

```js
function(parametro1, parametro2, parametro2) {
  console.log(parametro1, parametro2, parametro2)
}
```

- Por ejemplo podemos utilizar los parámetros de la siguiente forma

**Ejemplo:**

```js
function saludar(nombreDelUsuario) {
  console.log("Hola " + nombreDelUsuario + "!!!");
}

saludar("Marta"); // Muestra en consola: Hola: Marta!!!
saludar("Xime"); // Muestra en consola: Hola: Xime!!!
saludar("Raúl"); // Muestra en consola: Hola: Raúl!!!
```

- En este ejemplo vemos varias cosas
  - Declaramos una función saludar
  - La función saludar espera un parámetro que le pusimos el nombre de **nombreDelUsuario**
  - **nombreDelUsuario** en la función no es más que una variable que va a tomar un valor según lo que le pasen como parámetro a la función
  - Al ejecutar la función `saludar('Marta')` estamos pasando 'Marta' como parámetro
  - Dentro de la función **nombreDelUsuario** tiene asignado el nombre que le pasaron, ejemplo en el primer llamado tiene 'Marta', en el segundo 'Xime' y en el tercero 'Raúl'
  - Podemos cambiar los valores que le pasamos como parámetros a una función y eso es lo que le da tanta felxibilidad a las funciones

**Ejemplo:**

```js
const saludar = function (nombreDelUsuario) {
  console.log("Hola " + nombreDelUsuario + "!!!");
};

saludar("Marta"); // Muestra en consola: Hola: Marta!!!
saludar("Xime"); // Muestra en consola: Hola: Xime!!!
saludar("Raúl"); // Muestra en consola: Hola: Raúl!!!
```

- También podemos utilizar una variable para asignarle la función con el parámetro esperado y obtener el mismo resultado
- Otra forma similar de hacer esto es utilizando el valor de retorno

**Ejemplo:**

```js
const saludo = function (nombreDelUsuario) {
  return "Hola " + nombreDelUsuario + "!!!";
};

console.log(saludo("Marta")); // Muestra en consola: Hola: Marta!!!
console.log(saludo("Xime")); // Muestra en consola: Hola: Xime!!!
console.log(saludo("Raúl")); // Muestra en consola: Hola: Raúl!!!
```

- Este ejemplo es un poco más difícil de ver pero funciona de forma similar a la anterior
- En este caso declaramos la función y la asignamos a la variable saludo
- Ahora podemos pasar un nombre a saludo() y obtener un string como respuesta
- Al valor retornado por la función saludo lo mostramos en consola
- Una función puede aceptar más de un parámetro
- Es importante el orden en que ponemos los parámetros para utilizar una función

**Ejemplo:**

```js
const saludar = function(nombreDelUsuario, edad) {
  console.log('El usuario ' + nombreDelUsuario + ' tiene años' + edad + '!!!';
}

saludar('Nico', 38); // El usuario Nico tiene 38 años!!!
saludar(18, 'Marta'); // El usuario 18 tiene Marta años!!!
```

- En el primer llamado la función espera el nombre como primer parámetro y la edad como segundo por lo cual como se le pasaron los parámetros correctamente puede mostrar el mensaje bien
- En el segundo llamado se utilizan mal los parámetros por lo cual se muestra mal el mensaje

#### Prácticas

- [Ejercicio 107](../ejercicios/consignas/js/ej107.md)
- [Ejercicio 108](../ejercicios/consignas/js/ej108.md)
- [Ejercicio 109](../ejercicios/consignas/js/ej109.md)
- [Ejercicio 110](../ejercicios/consignas/js/ej110.md)
- [Ejercicio 111](../ejercicios/consignas/js/ej111.md)
- [Ejercicio 112](../ejercicios/consignas/js/ej112.md)
- [Ejercicio 113](../ejercicios/consignas/js/ej113.md)
- [Ejercicio 114](../ejercicios/consignas/js/ej114.md)
- [Ejercicio 115](../ejercicios/consignas/js/ej115.md)
- [Ejercicio 116](../ejercicios/consignas/js/ej116.md)
