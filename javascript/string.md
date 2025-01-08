# JavaScript

## String

- Los string representan un valor de texto, lo podemos utilizar para guardar valores como nombre, apellido, dirección, etc.
- Los valores del tipo string se escriben entre comillas dobles "" o simples ''
- Si bien es lo mismo utilizar cualquier tipo de comillas por una cuestión de convensión vamos a utilizar comillas simple ('') a lo largo del curso

**Ejemplo:**

```js
let nombre = "Juan";
let apellido = "Perez";

console.log(nombre);
console.log(apellido);
```

- En este ejemplo declaramos dos variables (nombre y apellido) y le asignamos dos **valores del tipo string ('Juan', 'Perez')**
- Podemos utilizar este tipo de dato para un mensaje

**Ejemplo:**

```js
let mensaje = "Bienvenidos a ECMAScript!!!";
console.log(mensaje);
```

- No hace falta asignar los tipos de datos a una variable, podemos utilizarlos como literales de la siguiente forma

**Ejemplo:**

```js
console.log("Bienvenidos a ECMAScript!!!");
```

- En este ejemplo utilizamos un **string o cadena de caracteres** en `console.log()` directamente

#### Prácticas

[Ejercicio 10](../ejercicios/consignas/js/ej10.md)
[Ejercicio 11](../ejercicios/consignas/js/ej11.md)

### Concatenar textos

- Utilizando el operador `+` podemos unir dos o más **strings**

**Ejemplo:**

```js
let nombre = "Juan";
let espacio = " ";
let apellido = "Perez";

console.log(nombre + espacio + apellido);
```

- En este ejemplo vemos como podemos concatener o unir 3 variables del tipo string
- Podemos escribir este mismo ejemplo de la siguiente forma sin utilizar una variable para el espacio

**Ejemplo:**

```js
let nombre = "Juan";
let apellido = "Perez";

console.log(nombre + " " + apellido);
```

- Podemos ver en este ejemplo como utilizamos un valor literal para el espacio sin asignarlo a una variable

#### Prácticas

[Ejercicio 12](../ejercicios/consignas/js/ej12.md)
[Ejercicio 13](../ejercicios/consignas/js/ej13.md)
[Ejercicio 14](../ejercicios/consignas/js/ej14.md)

### Interpolación de textos

- En ES6 podemos utilizar una sintaxis para interpolar valores dentro de los strings
- Utilizamos las comillas **``** para establecer que es un texto donde vamos a interpolar un valor
- Por medio de `${variable}` establecemos cuál es el valor que queremos interpolar
- Para que se entienda mejor el concepto vamos a ver un ejemplo:

**Ejemplo:**

```js
var nombre = "Pedro";
var template = `Bienvenido ${nombre} a este sitio`;

console.log(template);
```

- En este caso definimos la variable nombre con el valor de Pedro
- Creamos un template con el siguiente valor:
  - Texto Bienvenido
  - Un placeholder para el contenido de la variable nombre (**${variable}**)
  - Otro texto: a este sitio
- Cuando ECMAScript interpola los valores obtenemos el siguiente valor: `Bienvenido Pedro a este sitio`
- Es decir que podemos crear un texto intercambiando uno o varios valores utilizando la función de interpolar textos de ES6

**Ejemplo:**

```js
let mama = "Marta";
let papa = "Martín";
let template = `Mi mamá se llama ${mama} y mi papá ${papa}`;

console.log(template);
```

- En este caso obtenemos el texto: Mi mamá se llama Marta y mi papá Martín
- Podemos obtener este mismo resultado utilizando concatenación de strings de la siguiente forma

**Ejemplo:**

```js
let mama = "Marta";
let papa = "Martín";
let mensaje = "Mi mamá se llama " + mama + " y mi papá " + papa;

console.log(mensaje);
```

- Utilizando ambas técnicas obtenemos el mismo resultado
- La interpolación de textos nos permiten hacerlo de una forma más simple y en formato de template

#### Prácticas

[Ejercicio 15](../ejercicios/consignas/js/ej15.md)
[Ejercicio 16](../ejercicios/consignas/js/ej16.md)
[Ejercicio 17](../ejercicios/consignas/js/ej17.md)

### ¿Comillas dobles o simples?

- Como sabemos podemos utilizar comillas dobles o simples para definir un tipo de dato **string**
- En algunos casos vamos a necesitar utilizar estos símbolos como parte del valor

**Ejemplo:**

```js
let texto = 'Este texto tiene "comillas dobles"';
let otroTexto = "Este texto tiene 'comillas simples'";

console.log(texto);
console.log(otroTexto);
```

- Si necesitamos utilizar un tipo de comillas como parte de nuestro **string** podemos establecer el valor utilizando el otro tipo de comillas:
  - Si necesito utilizar comilla simple como contenido podemos definir el string utilizando comillas dobles
  - En caso de utilizar comilla doble como contenido definimos el string utilizando comillas simples

#### Prácticas

[Ejercicio 18](../ejercicios/consignas/js/ej18.md)
[Ejercicio 19](../ejercicios/consignas/js/ej19.md)
