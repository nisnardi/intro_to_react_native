# JavaScript

## Operadores aritméticos

- En ECMAScript existen operadores que nos van a permitir hacer operaciones ariméticas como pueden ser la suma, resta, multiplicación y división entre otros

### Suma

- Usando el operador `+` podemos sumar dos números o dos tipos de dato **number**

**Ejemplo:**

```js
2 + 2;
```

- En este ejemplo estamos sumando dos valores de number literales

**Ejemplo:**

```js
const miEdad = 20;
const edadDeMiHermano = 15;
console.log(miEdad + edadDeMiHermano);
```

- Podemos sumar el valor que tienen asignado 2 o más variables

**Ejemplo:**

```js
const miEdad = 20;
const edadDeMiHermano = 15;
const resultado = miEdad + edadDeMiHermano;
console.log(resultado);
```

- También podemos utilizar una variable para guardar el resultado de sumar los valores de otras variables

### Resta

- Usando el operador `-` podemos restar dos números o dos tipos de dato **number**

**Ejemplo:**

```js
2 - 2; // Obtenemos 0 como resultado

const miEdad = 20;
const edadDeMiHermano = 15;

// Mostramos en consola el resultado de restar los valores de estas dos variables
console.log(miEdad - edadDeMiHermano);

// Utilizamos una variable para guardar el resultado de la operación
const resultado = miEdad - edadDeMiHermano;
console.log(miEdad - edadDeMiHermano);
```

- Podemos usar más de un operador:

**Ejemplo:**

```js
10 + 2 - 2;

const miEdad = 20;
const edadDeMiHermano = 15;

// Podemos utilizar distintos operadores como también valores literales
console.log(miEdad - edadDeMiHermano + 10);

const resultado = miEdad - edadDeMiHermano + 10;

console.log("El resultado es: " + resultado);
```

### Multiplicación

- Usando el operador `*` podemos multiplicar dos números o dos tipos de dato **number**

**Ejemplo:**

```js
2 * 2; // Obtenemos 4 como resultado

const numero1 = 10;
const numero2 = 5;

console.log(numero1 * numero2);

const resultado = numero1 * numero2;
console.log(resultado);
```

- Podemos utilizar paréntesis para establecer que operación queremos que se resuelva primero, esto tiene que ver con la precendecia de operadores. Es como volver al colegio pero ahora tiene sentido!

**Ejemplo:**

```js
2 + 2 * 4; // 10
(2 + 2) * 4; // 16
```

- En este caso vemos que al utilizar paréntesis estabamos definiendo como queremos que se hagan las operaciones
- En el segundo ejemplo vemos que primero se va a resolver la suma de 2 + 2 y luego se va a multiplicar el resultado
- Este concepto también funciona con variables como es de esperar

**Ejemplo:**

```js
const dos = 2;
const cuatro = 4;

console.log(dos + dos * cuatro); // 10
console.log((dos + dos) * cuatro); // 16
```

### División

- Usando el operador `/` podemos dividir dos números o dos tipos de dato **number**

**Ejemplo:**

```js
20 / 2; // 10

const numero1 = 20;
const numero2 = 2;

console.log(numero1 / numero2); // 10

const resultado = numero1 / numero2;
console.log(resultado); // 10
```

- Dado que este código es una representación de una operación matemática tenemos que tener cuidado a la hora de dividir por 0
- ECMAScript obtenemos un valor del tipo **Infinity** al intentar dividir por 0
- Para saber más sobre este valor podes visitar el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Infinity)

### Módulo o resto

- Usando el operador `%` podemos obtener el resto de dividir dos números o dos tipos de dato **number**

**Ejemplo:**

```js
20 % 2; // 0

const numero1 = 20;
const numero2 = 2;

console.log(numero1 % numero2); // 0

const resultado = numero1 % numero2;
console.log(resultado); // 0
```

- Este operador nos es útil por ejemplo si queremos saber si un número es par o no.

#### Prácticas

- [Ejercicio 27](../ejercicios/consignas/js/ej27.md)
- [Ejercicio 28](../ejercicios/consignas/js/ej28.md)
- [Ejercicio 29](../ejercicios/consignas/js/ej29.md)
- [Ejercicio 30](../ejercicios/consignas/js/ej30.md)
- [Ejercicio 31](../ejercicios/consignas/js/ej31.md)
- [Ejercicio 32](../ejercicios/consignas/js/ej32.md)

### Incremento y decremento

- Por medio de distintos operadores podemos hacer operaciones de una forma más simple a nivel código

#### Incrementar en 1

- Utilizando el operador `++` podemos incrementar un valor en 1

**Ejemeplo:**

```js
let numero = 0;
numero++;
console.log(numero); // 1
```

- También podemos establecer que primero queremos incrementar la variable para luego utilizarla cambiando el lugar del operador

**Ejemplo:**

```js
let numero = 0;
++numero;
console.log(numero); // 1
```

- En este caso parece ser lo mismo pero se pueden dar situaciones donde no lo sea

#### Restar un número

- Utilizando el operador `--` podemos reducir un valor en 1
- Al igual que en el incremento el operador puede ir delante o después del valor según el resultado esperado

**Ejemplo:**

```js
let numero = 10;

--numero;
console.log(numero); // 9

numero--;
console.log(numero); // 8
```

#### Hacer una operación sobre un mismo valor

- Al definir una variable podemos asignarle un valor como ya vimos
- Podemos reutilizar esa variable para asignarle otro valor
- También podemos utilizar la variable para usar el valor y luego asignarlo de nuevo a la misma variable
- Vamos a ver un ejemplo:

**Ejemplo:**

```js
let numero = 1;
numero = numero + 1;
```

- Como vimos podemos usar el operador `++` para conseguir el mismo resultado
  **Ejemplo:**

```js
let numero = 1;
numero++;
```

- Es decir que en este caso se incrementa y asigna el valor de la variable numero
- Este operador es súper útil pero sólo nos permite operar con la suma y con un valor de 1
- Existen distintos operadores que nos permiten hacer operaciones sobre un valor y asignar el resultado a la misma variable escribiendo menos código
- Los operadores son:
  - `+=` para la suma
  - `-=` para la resta
  - `*=` para la multiplicación
  - `/=` para la división
- Este concepto se entiende mejor desde código

**Ejemplo:**

```js
let numero = 1;

numero += console.log(numero); // 2
```

**Ejemplo:**

```js
let numero = 1;

numero = numero + 10;
console.log(numero); // 11
```

- También puedo hacer esta operación de la siguiente forma

**Ejemplo:**

```js
let numero = 1;

numero += 10;
console.log(numero); // 11
```

- Vemos que podemos sumar el valor 10 al valor que tiene la variable numero y asignar el resultado a la misma variable utilizando sólo el operador `+=`
- Podemos hacer esto con el resto de los operadores

**Ejemplo:**

```js
let numero = 10;

numero -= 2;
console.log(numero); // 8
```

**Ejemplo:**

```js
let numero = 10;

numero *= 2;
console.log(numero); // 20
```

**Ejemplo:**

```js
let numero = 20;

numero /= 2;
console.log(numero); // 10
```

- El concepto es siempre el mismo y lo que cambia es la operación realizada

#### Práctica

[Ejercicio 33](../ejercicios/consignas/js/ej33.md)
