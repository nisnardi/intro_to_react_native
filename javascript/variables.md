# JavaScript - Declaración de variables y operador de asignación

## Declaración de variables

- Al programar necesitamos almacenar valores en la memoria de la computadora para poder interactuar con ellos
- Para poder identificar estos valores le asignamos un nombre descriptivo
- Es posible que a lo largo de un programa pisemos un valor guardado en una posición de memoria, es decir que este valor puede ser **variable**
- Podemos decir que una **variable** es algo que nos permite almacenar un valor en memoria de la computadora y que por medio de un nombre descriptivo podemos acceder e interactuar con él.

### ES5

- En JavaScript existe la palabra reservada **var** que nos permite declarar una **variable**

**Ejemplo:**

```js
var variable;
```

- Si en nuestro programa vamos a necesitar el nombre y edad del usuario podemos declarar las siguientes variables:

**Ejemplo:**

```js
var nombre;
var edad;
```

- En ES5 podemos no utilizar **var** para declarar nuestras variables
- Esto se considera una mala práctica por más que el lenguaje lo permita
- Para evitar problemas siempre que declaren una variable utilicen **var**

- Los nombres de las variables tienen que empezar con una letra
- Para evitar problemas usemos nombres descriptivos que reflejen el valor que queremos asignar a cada variable
- En programación existen distintos tipos de forma de escribir los nombres de las variables, en EcmaScript es común utilizar una forma que se denomina camelCase donde la primer letra de la primer palabra va en minúscula y luego cada palabra comienza con mayúscula
- La primer letra del nombre de las variables va a ser siempre en minúscula
- Evitamos utilizar acentos o simbolos en los nombres de las variables

**Ejemplo:**

```js
var nombreDeMiVariable;
```

- En el ejemplo anterior vemos que declaramos una variable con el nombre de **nombre de mi variable** dado que los nombres de las variables no aceptan espacios utilizamos la denominación camel case para escribirlo: **nombreDeMiVariable**

#### Prácticas

[Ejercicio 1](../ejercicios/consignas/js/ej1.md)

## Operador de asignación

- Una vez declarado el nombre de una variable podemos asignarle un valor. Esto se da ya que tenemos asignado un espacio en memoria donde podemos guardar un valor
- Por medio del operador de asignación **=** podemos asignar un valor a una variable

**Ejemplo:**

```js
var nombre;
nombre = "Martín";
```

- Podemos declarar todas las variables que necesitemos utilizar

**Ejemplo:**

```js
var nombre;
var edad;
nombre = "Martín";
edad = 20;
```

#### Prácticas

[Ejercicio 2](../ejercicios/consignas/js/ej2.md)

- También podemos declarar todas las variables en una línea y luego asignarle valores

**Ejemplo:**

```js
var nombre, edad;
nombre = "Martín";
edad = 20;
```

#### Prácticas

[Ejercicio 3](../ejercicios/consignas/js/ej3.md)

- También podemos declarar una variable y asignar un valor en la misma sentencia

**Ejemplo:**

```js
var nombre = "Martín";
var edad = 20;
```

#### Prácticas

[Ejercicio 4](../ejercicios/consignas/js/ej4.md)

- Utilizando `console.log()` podemos mostrar el valor de una variable en la consola

**Ejemplo:** Archivo **datos.js**

```js
var nombre = "Martín";
var edad = 20;
console.log(nombre);
console.log(edad);
```

**Ejecutamos el programa datos.js utilizando Node.js**

```bash
node datos.js
```

#### Prácticas

[Ejercicio 5](../ejercicios/consignas/js/ej5.md)

- Vemos como salida los valores Martín y 20
- `console.log()` acepta varios valores separados por como para mostrar más de un valor en consola
- Podemos mostrar algo más significativo si escribimos lo mismo de la siguiente manera

**Ejemplo:** Archivo **datos.js**

```js
var nombre = "Martín";
var edad = 20;
console.log("nombre: ", nombre);
console.log("edad: ", edad);
```

**Ejecutamos el programa datos.js utilizando Node.js**

```bash
node datos.js
```

- Al ejecutar este programa vemos una salida que nos explica mejor que es cada valor ya que vemos **nombre: Martín** y **edad: 20**
- Esta es una forma fácil de ver los valores de las variables y saber de donde viene

#### Prácticas

[Ejercicio 6](../ejercicios/consignas/js/ej6.md)

### ES6

- En la nueva versión del lenguaje podemos declarar variables utilizando **let**

```js
let variable = valor;
```

#### Prácticas

[Ejercicio 7](../ejercicios/consignas/js/ej7.md)

- En programación existe un concepto de **constante** que significa que es una variable a la cual le asignamos un valor y no va a cambiar durante la ejecución del programa y de ahí su nombre.
- En ES6 podemos declarar una variable como **constante** utilizando la palabra reservada **const**

```js
const constante = valor;
```

#### Prácticas

[Ejercicio 8](../ejercicios/consignas/js/ej8.md)

- Obtenemos un error si cambiamos el valor asignado de una variable constante.

```js
const constante = valor;
constante = otroValor;
// Obtenemos un error de asignación: Assignment to constant variable.
```

#### Prácticas

[Ejercicio 9](../ejercicios/consignas/js/ej9.md)

## Tipos base

- Como vimos en los ejemplos anteriores existen distintos tipos de datos para representar distintos valores

**Ejemplo:**

```js
var nombre = "Martín";
var edad = 20;

console.log("nombre: ", nombre);
console.log("edad: ", edad);
```

- En este ejemplo vemos que para el nombre estamos utilizando un valor entre `''` y para la edad estamos utilizando un número
- ECMAScript tiene los siguientes tipos base:
  - **string:** Los **string** también son conocidos como cadena de caracteres y no son más que un texto
  - **number:** El tipo de dato **number** son números y nos permiten hacer operaciones matemáticas
  - **boolean:** Este tipo **boolean** acepta valores del tipo **true** o **false**, es decir que podemos utilizarlo cuando necesitamos un valor **verdadero (true)** o **falso (false)**
  - **undefined:** Define que un valor es indefinido
  - **null:** Define que un valor es nulo, parece que es similar a undefined pero ya vamos a ver algunas diferencias
- A la hora de definir y asignar valores en nuestros programas vamos a tener que definir de que tipo de dato van a ser para saber que tipo de operaciones podemos hacer con ellos
- Existen más tipos en ECMAScript y los vamos a ir viendo a lo largo del curso pero por ahora podemos arrancar con estos
