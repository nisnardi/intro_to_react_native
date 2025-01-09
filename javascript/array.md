# JavaScript

## Array

- Otro de los tipos que tenemos en ECMASCript es el **array**
- Este tipo de dato nos permite guardar múltiples valores en una sola variable
- Podemos ver este tipo de datos como una colección
- La forma de crear un **array** es utilizando los corchetes y separar los valores utilzando comas

**Ejemplo:**

```js
["nico", "pedro", "juan", "marta", "belen", "emilia", "xime"];
```

- En este caso tenemos un **array** que tiene 7 elementos que parecen ser personas

**Ejemplo:**

```js
const alumnos = ["nico", "pedro", "juan", "marta", "belen", "emilia", "xime"];

// otra forma de escribir esto puede ser:
const alumnos = ["nico", "pedro", "juan", "marta", "belen", "emilia", "xime"];
```

- También podemos crear un array vacío ya que no siempre sabemos que elementos va a tener

**Ejemplo:**

```js
const alumnos = [];
```

- Un array puede guardar cualquier tipo de dato

**Ejemplo:**

```js
const datos = [
  "hola",
  42,
  false,
  null,
  function () {
    console.log("hola");
  },
];
```

- Para obtener los datos de un array podemos utilizar el índice
- Los índices en ECMAScript comienzan en 0
- Es decir que el primer item lo podemos obtener con el índice 0

**Ejemplo:**

```js
const datos = [
  "hola",
  42,
  false,
  null,
  function () {
    console.log("hola");
  },
];

const saludo = datos[0];
const significadoDeLaVida = datos[1];
const casada = datos[2];
let miVariable = datos[3];
const saludar = datos[4];

console.log(saludo);
console.log(significadoDeLaVida);
console.log("casada?:", casada);
console.log(miVariable);

// Acá se viene el gran momento de tu vida:
saludar(); // muestra en consola hola
```

- En este ejemplo vemos que podemos acceder a los distintos elementos de un **array** utilizando un índice numérico
- Podemos almacenar todos los datos en otras variables
- En el caso de la función estamos simplemente asignando una función a la variable saludar como cualquier otro valor (ECMAScript nos deja hacer esto y es genial) y luego ejecutamos esta función (todo muy normal)

#### Prácticas

- [Ejercicio 117](../ejercicios/consignas/js/ej117.md)
- [Ejercicio 118](../ejercicios/consignas/js/ej118.md)
- [Ejercicio 119](../ejercicios/consignas/js/ej119.md)

- También podemos asignar un valor a una posición de un array utilizando el índice

**Ejemplo:**

```js
const alumnos = ["nico", "pedro", "juan", "marta", "belen", "emilia", "xime"];
alumnos[0] = "Pana";
alumnos[3] = "Jorge";

console.log(alumnos);
// ['Pana', 'pedro', 'juan', 'Jorge', 'belen', 'emilia', 'xime']
```

- Tenemos que tener cuidado al asignar un item de un array

**Ejemplo:**

```js
const alumnos = ["nico", "pedro", "marta", "belen", "emilia"];
alumnos[8] = "Paola";
console.log(alumnos);
// [ 'nico', 'pedro', 'marta', 'belen', 'emilia', , , , 'Paola' ]
```

- ECMAScript al manejar la memoria de forma dinámica asigna espacios vacíos en las posiciones donde no existen valores

**Ejemplo:**

```js
const alumnos = ["nico", "pedro", "marta", "belen", "emilia"];
alumnos[8] = "Paola";
alumnos[5] = "Lucas";
alumnos[6] = "Lucy";
alumnos[7] = "Andy";
console.log(alumnos);
/*
[ 
  'nico',
  'pedro',
  'marta',
  'belen',
  'emilia',
  'Lucas',
  'Lucy',
  'Andy',
  'Paola' 
]
*/
```

- En este caso completamos los datos que nos faltaban utilizando índices

#### Prácticas

- [Ejercicio 120](../ejercicios/consignas/js/ej120.md)
- [Ejercicio 121](../ejercicios/consignas/js/ej121.md)
- [Ejercicio 122](../ejercicios/consignas/js/ej122.md)

## Métodos y Propiedades más utilizados del Array

### Longitud

- Por medio de la propiedad **length** podemos obtener la cantidad de elementos que tiene un **array**
- Funciona de la misma forma que la propiedad **length** de los **strings**

**Ejemplo:**

```js
const alumnos = ["nico", "pedro", "marta", "belen", "emilia"];
console.log(alumnos.length); // 5
```

- Podemos utilizar esta propiedad para obtener el último elemento de un array
- Si a la longitud de un array le restamos 1 obtenemos el último índice del último elemento

**Ejemplo:**

```js
const alumnos = ["nico", "pedro", "marta", "belen", "emilia"];
const cantidadDeElementos = alumnos.length;
const ultimoIndice = cantidadDeElementos - 1;
console.log(alumnos[ultimoIndice]); // emilia
```

- Otra forma de escribir esto es:
  **Ejemplo:**

```js
const alumnos = ["nico", "pedro", "marta", "belen", "emilia"];
console.log(alumnos[alumnos.length - 1]); // emilia
```

- Vemos que podemos utilizar la propiedad length - 1 para obtener el último índice y luego obtener el último elemento

#### Prácticas

- [Ejercicio 123](../ejercicios/consignas/js/ej123.md)
- [Ejercicio 124](../ejercicios/consignas/js/ej124.md)

### Push, unshift, shift y pop

- Utilizando los métodos **push, unshift, shift y pop** podemos alterar los elementos de un array

#### Push

- El método **push** permite agregar uno o más elementos al final de un array
- Retorna la nueva longitud que tiene el array
- Podes leer más sobre push en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/push)

**Ejemplo:**

```js
const animales = ["perro", "pato", "vaca"];
let cantidadDeAnimales = animales.push("gato");

console.log(animales);
// [ 'perro', 'pato', 'vaca', 'gato' ]
console.log(cantidadDeAnimales); // 4

cantidadDeAnimales = animales.push("elefante", "delfin");

console.log(animales);
// [ 'perro', 'pato', 'vaca', 'gato', 'elefante', 'delfin' ]
console.log(cantidadDeAnimales); // 6
```

- En este ejemplo vemos varias cosas interesantes
- Por un lado con el método **push** podemos agregar un elemento a un array como en el caso de **gato** o varios como en el caso de **elefante y delfin**
- Estamos modificando el array original **animales**, es decir que estamos mutando su valor
- Al declarar una array utilizando **const** nos permite tener una constante pero podemos cambiar los elementos que tiene esta colección.
- En caso de asignar otro valor a la variable obtenemos el mismo error de siempre

#### Unshift

- El método **unshift** agrega uno o más elementos al inicio de un array
- Retorna la nueva longitud que tiene el array
- Podes leer más sobre **unshift** en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/unshift)

**Ejemplo:**

```js
const animales = ["perro", "pato", "vaca"];
let cantidadDeAnimales = animales.unshift("gato");

console.log(animales);
// [ 'gato', 'perro', 'pato', 'vaca' ]
console.log(cantidadDeAnimales); // 4

cantidadDeAnimales = animales.unshift("elefante", "delfin");

console.log(animales);
// [ 'elefante', 'delfin', 'gato', 'perro', 'pato', 'vaca' ]
console.log(cantidadDeAnimales); // 6
```

- Podemos decir que funciona como push pero en lugar de insertar los elementos al final lo hace al principio

#### Shift

- El método **shift** elimina el primer elemento de un array
- Retorna el elemento eliminado
- Este método modifica la propiedad **length** del array
- Podes leer más sobre **shift** en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/shift)

**Ejemplo:**

```js
const animales = ["perro", "pato", "vaca"];
const perro = animales.shift();
console.log(animales);
// ['pato', 'vaca']
console.log(animales.length);
// 2

const pato = animales.shift();
console.log(animales);
// ['vaca']
console.log(animales.length);
// 1

const vaca = animales.shift();
console.log(animales);
// []
console.log(animales.length);
// 0

console.log(perro); // perro
console.log(pato); // pato
console.log(vaca); // vaca
```

- Podemos ver como utilizando el método **shift** podemos obtener el primer elemento y eliminarlo del array
- Al sacar un elemento se modifica la propiedad **length** del array

#### Pop

- El método **pop** elimina el último elemento de un array
- Retorna el elemento eliminado
- Este método modifica la propiedad **length** del array
- Podes leer más sobre **pop** en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/pop)

**Ejemplo:**

```js
const animales = ["perro", "pato", "vaca"];
const vaca = animales.pop();
console.log(animales);
// ['perro', 'pato']
console.log(animales.length);
// 2

const pato = animales.shift();
console.log(animales);
// ['perro']
console.log(animales.length);
// 1

const perro = animales.shift();
console.log(animales);
// []
console.log(animales.length);
// 0

console.log(vaca); // vaca
console.log(pato); // pato
console.log(perro); // perro
```

- Vemos que el método pop funciona de manera similar que shift

### Sort y reverse

#### Sort

- Utilizando el método **sort** podemos ordenar un array
- Retorna el array ordenado
- Los elementos son ordenados convirtiéndolos a strings y comparando la posición del valor Unicode de dichos strings
- Podes leer más sobre **sort** en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/sort)

**Ejemplo:**

```js
let numeros = [1, 4, 2, 5, 3, 8, 9];
numeros = numeros.sort();

console.log(numeros);
// [ 1, 2, 3, 4, 5, 8, 9 ]
```

- Al ordenar utilizando los elementos usando strings y la posición en la tabal de Unicode se pueden dar resultados que no son los esperados
- También tenemos la opción de pasar una función de ordenado para establecer la forma que queremos ordenarlo

#### Reverse

- El método **reverse** nos permite revertir el orden que tiene un array
- Retorna el array modificado
- Podes leer más sobre **reverse** en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/reverse)

**Ejemplo:**

```js
let numeros = [1, 4, 2, 5, 3, 8, 9];
numeros = numeros.reverse();

console.log(numeros);
[9, 8, 3, 5, 2, 4, 1];
```

### Concat y join

- Con los métodos **concat** y **join** podemos unir arrays de distintas formas

#### Join

- El método **join** permite unir los valores de un array en un string
- Acepta como valor un string para unir los elementos
- Podes leer más sobre **join** en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/join)

**Ejemplo:**

```js
const numeros = [1, 4, 2, 5, 3, 8, 9];
let resultado = numeros.join(" - ");

console.log(resultado);
// 1 - 4 - 2 - 5 - 3 - 8 - 9

resultado = numeros.join(", ");

console.log(resultado);
// 1, 4, 2, 5, 3, 8, 9
```

- Podemos unir los valores del array utilizando un concepto que queremos como por ejemplo el '-' o ','

#### Concat

- El método **concat** nos permite unir 2 arrays y obtener un nuevo array con los elementos de ambos
- Podes leer más sobre **concat** en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/concat)

**Ejemplo:**

```js
const animales = ["perro", "vaca", "gato"];
const mutantes = ["Charles Francis Xavier", "Cíclope", "Bestia", "Jean Grey"];
const animalesMutantes = animales.concat(mutantes);

console.log(animalesMutantes);
/*
[ 
  'perro',
  'vaca',
  'gato',
  'Charles Francis Xavier',
  'Cíclope',
  'Bestia',
  'Jean Grey' 
]
*/
```

### IndexOf

- El método **indexOf** retorna el primer índice donde se encuentra un elemento
- Si no encuentra el elemento buscado **retorna -1**
- Podes leer más sobre **indexOf** en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/indexOf)

**Ejemplo:**

```js
const mutantes = ["Charles Francis Xavier", "Cíclope", "Bestia", "Jean Grey"];

if (mutantes.indexOf("Bestia") > -1) {
  console.log("Bestia es parte de los mutantes");
}

// Bestia es parte de los mutantes

if (mutantes.indexOf("Logan") > -1) {
  console.log("Logan es parte de los mutantes");
} else {
  console.log("Logan no es parte de los mutantes");
}
// Logan no es parte de los mutantes
```

- En la primer condición se cumple ya que indexOf retorna la posición 2 donde se encuentra el elemento Bestia
- En la segunda condición no se cumple ya que indexOf retorna -1 ya que Logan no es parte del array mutantes en este momento (sólo para este ejemplo, te queremos Logan! ❤️)

### toString

- El método **toString** nos retorna la representación del contenido de un array en string
- Es similar a **join** pero no sabemos como une los elementos ya que no lo especificamos
- Podes leer más sobre **toString** en el [sitio del MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toString)

**Ejemplo:**

```js
const mutantes = ["Charles Francis Xavier", "Cíclope", "Bestia", "Jean Grey"];
console.log(mutantes.toString());
// 'Charles Francis Xavier', 'Cíclope', 'Bestia', 'Jean Grey'
```

#### Prácticas

- [Ejercicio 125](../ejercicios/consignas/js/ej125.md)
- [Ejercicio 126](../ejercicios/consignas/js/ej126.md)
- [Ejercicio 127](../ejercicios/consignas/js/ej127.md)
- [Ejercicio 128](../ejercicios/consignas/js/ej128.md)
- [Ejercicio 129](../ejercicios/consignas/js/ej129.md)
- [Ejercicio 130](../ejercicios/consignas/js/ej130.md)
- [Ejercicio 131](../ejercicios/consignas/js/ej131.md)
- [Ejercicio 132](../ejercicios/consignas/js/ej132.md)
- [Ejercicio 133](../ejercicios/consignas/js/ej133.md)
- [Ejercicio 134](../ejercicios/consignas/js/ej134.md)
