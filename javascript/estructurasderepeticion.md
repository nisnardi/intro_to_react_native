# JavaScript

## Estructuras de repetición

- Es común en la programación tener que ejecutar un mismo código varias veces
- Por ejemplo si quiero imprimir en pantalla los números del 0 al 10 lo puedo hacer de la siguiente manera

**Ejemplo:**

```js
console.log(0);
console.log(1);
console.log(2);
console.log(3);
console.log(4);
console.log(5);
console.log(6);
console.log(7);
console.log(8);
console.log(9);
console.log(10);
```

- Si bien de esta forma logramos el objetivo es poco práctico si necesito cambiar por ejemplo el mensaje que quiero mostrar ya que tengo que modificar muchas lineas de código, imaginemos que tengo que mostrar del 0 al 100 o al 1000!! NOS VOLVEMOS LOCOS!!!

**Ejemplo:**

```js
console.log("número: ", 0);
console.log("número: ", 1);
console.log("número: ", 2);
console.log("número: ", 3);
console.log("número: ", 4);
console.log("número: ", 5);
console.log("número: ", 6);
console.log("número: ", 7);
console.log("número: ", 8);
console.log("número: ", 9);
console.log("número: ", 10);
```

- Para nuestra sanidad mental existen las estructuras de repetición que nos hacen la vida más fácil

### While

- Existe una estructura de repetición que se llama **while** y se ejecuta mientras la condición sea verdadera
- En español podemos pensar esta estructura como **MIENTRAS** condición **HACER** tal cosa

**Ejemplo:**

```js
while (condicion) {
  console.log("Imprimo este mensaje mientras la condición sea verdadera");
}
```

- Vamos a refactorizar el código que muestra números del 0 al 10 utilizando la estructura **while**

**Ejemplo:**

```js
let numero = 0;

while (numero < 11) {
  console.log(numero);
  numero++;
}
```

- Con tan solo un par de lineas de código podemos mostrar todos los números del 0 al 10 y si queremos mostrar más tan solo hacemos un cambio

**Ejemplo:**

```js
let numero = 0;

while (numero < 10000) {
  console.log(numero);
  numero++;
}
```

- En caso de querer cambiar el mensaje tan solo modificamos una línea de código

**Ejemplo:**

```js
let numero = 0;

while (numero < 10000) {
  console.log("número: ", numero);
  numero++;
}
```

- Vemos que de esta forma las estructura de repetición nos hacen la vida mucho más fácil y controlable
- Un tema que tenemos que tener en cuenta es que al utilizar las estructuras de repetición podemos caer en lo que se denomina un loop infinito, es decir que es un código que se va a repetir por siempre ya que la condición no cambia. Esto puede colgar un servidor o el ambiente donde estemos ejecutando esta repetición. IMPORTANTE: recordar cambiar la condicón en algún momento.

**Ejemplo:**

```js
while (true) {
  console.log("colgamos esta rutina");
}

let numero = 0;

while (numero < 10000) {
  console.log("número: ", numero);
}
```

- En cualquiera de estos ejemplos podemos colgar todo ya que en ningún momento se modifica la condición y siempre va a ser verdadera.
- Otra de las características que tiene el **while** es que si la condición es negativa no se ejecuta

**Ejemplo:**

```js
while (false) {
  console.log("nunca se ejecuta este código");
}

let numero = 1000;

while (numero < 10) {
  console.log("número: ", numero);
  numero++;
}
```

#### Prácticas

- [Ejercicio 66](../ejercicios/consignas/js/ej66.md)
- [Ejercicio 67](../ejercicios/consignas/js/ej67.md)
- [Ejercicio 68](../ejercicios/consignas/js/ej68.md)
- [Ejercicio 69](../ejercicios/consignas/js/ej69.md)
- [Ejercicio 70](../ejercicios/consignas/js/ej70.md)
- [Ejercicio 71](../ejercicios/consignas/js/ej71.md)
- [Ejercicio 72](../ejercicios/consignas/js/ej72.md)
- [Ejercicio 73](../ejercicios/consignas/js/ej73.md)
- [Ejercicio 74](../ejercicios/consignas/js/ej74.md)
- [Ejercicio 75](../ejercicios/consignas/js/ej75.md) (avanzado)

### do/while

- Otra de las estructuras de repetición que podemos encontrar es el **do/while**
- En español podemos leer esta estructura como **HACER MIENTRAS**
- La diferencia que tiene esta estructura con el **while** es que **siempre se ejecuta al menos una vez** y luego pregunta por la condición

**Ejemplo:**

```js
do {
  // esto se ejecuta al menos una vez
} while (condicion);
```

- Si la condición siempre es true también podemos colgar el proceso

**Ejemplo:**

```js
do {
  // colgamos todo
} while (true);
```

- Podemos escribir uno de los ejemplos anteriores de la siguiente manera:

**Ejemplo:**

```js
let numero = 0;

do {
  console.log('número: ', numero);
  numero++;
} while (numero < 10000) {
```

- En este ejemplo mostramos el mensaje e incrementamos la variable al menos una vez y luego podemos seguir mostrando el resto de los números

**Ejemplo:**

```js
let numero = 1000;

do {
  console.log("número: ", numero);
  numero++;
} while (numero < 10);
```

- En este ejemplo sólo se muestra el número 1000 y luego no se vuelve a repetir la condición.

#### Prácticas

- [Ejercicio 76](../ejercicios/consignas/js/ej76.md)
- [Ejercicio 77](../ejercicios/consignas/js/ej77.md)
- [Ejercicio 78](../ejercicios/consignas/js/ej78.md)
- [Ejercicio 79](../ejercicios/consignas/js/ej79.md)
- [Ejercicio 80](../ejercicios/consignas/js/ej80.md)
- [Ejercicio 81](../ejercicios/consignas/js/ej81.md)
- [Ejercicio 82](../ejercicios/consignas/js/ej82.md)
- [Ejercicio 83](../ejercicios/consignas/js/ej83.md)
- [Ejercicio 84](../ejercicios/consignas/js/ej84.md)
- [Ejercicio 85](../ejercicios/consignas/js/ej85.md)

## For

- Otra estructura de repetición que podemos utilizar es **for**
- Esta estructura en español se la denomina **PARA**
- Consiste en 3 partes delimitadas por un **;**

**Ejemplo:**

```js
for (iniciarVariable; condicion; alteración) {
  // se ejecuta siempre y cuando se cumpla la condición
}
```

- Por ejemplo para mostrar números de 0 a 10 podemos escribri el siguiente for:

**Ejemplo:**

```js
// Primero: declaramos la variable numero y le asignamos el valor 0
// Segundo: escribimos la condición que queremos validar
// Terceo: incrementamos el valor de la variable numero en 1

for (let numero = 0; numero <= 10; numero++) {
  console.log(numero);
}
```

- Siguiendo con los ejemplos anteriores si queremos modificar esta estructura lo podemos hacer de forma simple

**Ejemplo:**

```js
for (let numero = 0; numero <= 1000; numero++) {
  console.log("número: ", numero);
}
```

#### Prácticas

- [Ejercicio 86](../ejercicios/consignas/js/ej86.md)
- [Ejercicio 87](../ejercicios/consignas/js/ej87.md)
- [Ejercicio 88](../ejercicios/consignas/js/ej88.md)
- [Ejercicio 89](../ejercicios/consignas/js/ej89.md)
- [Ejercicio 90](../ejercicios/consignas/js/ej90.md)
- [Ejercicio 91](../ejercicios/consignas/js/ej91.md)
- [Ejercicio 92](../ejercicios/consignas/js/ej92.md)
- [Ejercicio 93](../ejercicios/consignas/js/ej93.md)
- [Ejercicio 94](../ejercicios/consignas/js/ej94.md)
- [Ejercicio 95](../ejercicios/consignas/js/ej95.md)
- [Ejercicio 96](../ejercicios/consignas/js/ej96.md)
- [Ejercicio 97](../ejercicios/consignas/js/ej97.md)

### Cortar la ejecución de una estructura de repetición

- Utilizando la sentencia **break** podemos cortar la ejecución de una estructura de repetición

**Ejemplo:**

```js
for (let i = 0; i < 1000; i++) {
  break;
}
```

- En este ejemplo se va a intentar correr el for, va a declarar la variable i, se le va a asignar el valor y luego se va a cortar la ejecución por el break.

**Ejemplo:**

```js
for (let i = 0; i < 1000; i++) {
  if (i < 10) {
    console.log(i);
  } else {
    break;
  }
}
```

- En este ejemplo si la variable i es 10 o más se va a cortar la ejecución del for y va a seguir el flujo normal del código

#### Prácticas

- [Ejercicio 98](../ejercicios/consignas/js/ej98.md)
- [Ejercicio 99](../ejercicios/consignas/js/ej99.md)
