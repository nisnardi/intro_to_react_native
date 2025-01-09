# JavaScript

## Operadores de comparación simple y estricta

### Comparación Simple

- Podemos comparar dos valores utilizando el operador `==` y obtener un valor **boolean** como resultado.
- Este tipo de comparación se conoce como comparación simple ya que sólo compara si un valor es igual a otro
- Al comparar 2 valores de distintos tipos podemos obtener que son el mismo valor sin importar que sean diferente tipo (ejemplo: comparar un string con un número)
- Si los valores son iguales obtenemos **true**
- En caso de que los valores sean distintos obtenemos el valor **false**

**Ejemplo:**

```js
let numero1 = 20;
let numero2 = 20;
let numero3 = 10;

console.log(numero1 == numero2); //true
console.log(numero1 == numero3); //false
```

- Comparamos sólo valores:

**Ejemplo:**

```js
console.log(10 == "10"); //true
```

- Ya que podemos comparar dos valores y saber si son iguales también podemos saber si son distintos utilizando el operador `!=`

**Ejemplo:**

```js
let numero1 = 20;
let numero2 = 20;
let numero3 = 10;

console.log(numero1 != numero2); // false
console.log(numero1 != numero3); // true
```

- Otra forma de comparar valores es saber si un valor es más grande que otro
- Utilizamos el operador `>` para saber si el valor de la izquierda del operador es más grande que el valor de la derecha

**Ejemplo:**

```js
let numero1 = 20;
let numero2 = 10;

console.log(numero1 > numero2); // true
```

- También podemos saber si un valor es más chico que otro utilizando el operador <

**Ejemplo:**

```js
let numero1 = 20;
let numero2 = 10;

console.log(numero2 < numero1); // true
```

- En algunos casos necesitamos saber si un valor es más grande o igual que otro
- Es decir que esta condición se va a transformar en verdadera en caso de que el valor de la izquierda sea más grande o el mismo valor que el de la derecha

**Ejemplo:**

```js
let numero1 = 20;
let numero2 = 10;
let numero3 = 20;

console.log(numero1 >= numero2); // true
console.log(numero1 >= numero3); // true
```

- Podemos hacer lo mismo para saber si es menor

**Ejemplo:**

```js
let numero1 = 20;
let numero2 = 10;
let numero3 = 10;

console.log(numero2 <= numero1); // true
console.log(numero2 <= numero3); // true
```

### Comparación Estrícta

- La comparación estricta no solo compara el valor sino también el tipo de dato
- Utilizamos el operador `===` para comparar si son el mismo tipo de dato y valor
- Utilizamos el operador `!==` para comparar si son el distintos tipo de dato y valor

**Ejemplo:**

```js
console.log(10 === "10"); // false
console.log(10 !== "10"); // true
console.log(10 !== "10"); // true
```

- Los dos últimos casos da **true** ya que no importa el valor que tengan ambos valores son distintos tipo de dato

#### Práctica

- [Ejercicio 34](../ejercicios/consignas/js/ej34.md)
- [Ejercicio 35](../ejercicios/consignas/js/ej35.md)
