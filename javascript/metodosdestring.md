# JavaScript

## Caracteres especiales en strings

- Existen caracteres especiales en los **strings** que agregan un valor extra
- \n Nueva Línea
- \t Tabulador
- \r Retorno de Línea

**Ejemplo:**

```js
let mensaje = "este texto \n es multilinea";
console.log(mensaje); // texto en 2 líneas

mensaje = "\t \t texto tabulado";
console.log(mensaje); // texto tabulado
```

- Por medio de los siguientes caracteres podemos escapar algunos caracteres:
- \' Apóstrofe o comilla sencilla
- \" Comilla doble
- \\ Carácter Backslash

**Ejemplo:**

```js
let mensaje = "este texto \\no es multilinea";
console.log(mensaje); // muestra el caracter \ como parte del texto

// si no escapamos el caracter \ el texto es multiliena en lugar de tener \ como parte del contenido
mensaje = "este texto \no es multilinea";
console.log(mensaje);
```

- Vemos que por medio de estos caracteres especiales podemos jugar con nuestros strings y prevenir errores o comportamientos inesperados!!

#### Práctica

- Abrir la consola de node o browser y probar estos ejemplos

## Propiedades y métodos de string

### Propiedad length

- Por medio de la propiedad length podemos saber cuántos caracteres tiene un **string**
- La propiedad **length** retorna o devuelve un número con la cantidad de caracteres que tiene el texto
- Lo utilizamos de la siguiente manera:

**Ejemplo:**

```js
let texto = "Bienvenidos a ECMAScript!!";
let cantidadDeCaracteres = texto.length;

console.log(cantidadDeCaracteres);
```

- En este ejemplo declaramos una variable `texto` con el valor `Bienvenidos a ECMAScript!!` y otra variable `cantidadDeCaracteres` donde guardamos la cantidad de caracteres que tiene la variable `texto`
- También podemos obtener el mismo resultado sin utilizar la variable `cantidadDeCaracteres`

**Ejemplo:**

```js
let texto = "Bienvenidos a ECMAScript!!";
console.log(texto.length);
```

#### Práctica

- [Ejercicio 38](../ejercicios/consignas/js/ej38.md)
- [Ejercicio 39](../ejercicios/consignas/js/ej39.md)

### Métodos de String

- Los métodos nos permiten obtener funcionalidad para los distintos tipos de datos
- Este método retorna un nuevo string con el texto concatenado
- Podemos ver una lista de métodos del tipo String en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/String)
- Vamos a ver algunos de los métodos más conocidos y jugar un poco con ellos

**Ejemeplo:**

```js
let variableString = "valor de nuestro string";

// Al tener un valor del tipo string podemos llamar a un método utilizando un punto (como con la propiedad length) y paréntesis ()
variableString.metodo();

// También podemos pasar un valor a los métodos para lograr una funcionalidad específica
variableString.metodo(valor);
```

## Concat

- Hasta ahora vimos que podemos utilizar el símbolo + para concatenar 2 valores
- Los strings tienen un método llamado **concat** que nos permite concatenar valores
- Podes saber más sobre este método en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/String/concat)

**Ejemplo:**

```js
let texto = "Hola ";
let nombre = "Marta";

// Concatenamos los strings usando el método concat
let mensaje = texto.concat(nombre);

console.log(mensaje);
```

- En este ejemplo se imprime el texto **Hola Marta**
- También se pueden pasar múltiples valores a ser concatenados

**Ejemplo:**

```js
let texto = "ECMA";
console.log(
  texto.concat("Script", " es lo mejor", " del mundo de la programación")
);
```

- en este ejemplo concatenemos varios strings al contenido de la variable texto
- Se muestra en pantalla el mensaje: **ECMAScript es lo mejor del mundo de la programación**;

#### Prácticas

- [Ejercicio 40](../ejercicios/consignas/js/ej40.md)

### Mayúsculas y minúsculas

- Podemos transformar un texto a mayúscula o minúscula utilizando los métodos **toUpperCase** y **toLowerCase** respectivamente

**Ejemplo:**

```js
let textoEnMayuscula = "HOLA";
let textoEnMinuscula = "amigos";

console.log(textoEnMayuscula.toLowerCase()); // muestra el texto hola
console.log(textoEnMinuscula.toUpperCase()); // muestra el texto AMIGOS

console.log(textoEnMayuscula); // muestra el texto HOLA
console.log(textoEnMinuscula); // muestra el texto amigos
```

#### Prácticas

- [Ejercicio 41](../ejercicios/consignas/js/ej41.md)
- [Ejercicio 42](../ejercicios/consignas/js/ej42.md)

### Caracteres y posiciones

- Por medio del método **charAt** podemos saber que caracter se encuentra en una determinada posición de un string
- Este método acepta un valor numérico como parámetro
- El primer caracter esta ubicado en la posición 0
- Para saber cual es el último caracter podemos utilizar la propiedad **length**
- Dado que el primer elemento arranca en 0 a la logitud del string debemos restarle uno

**Ejemplo:**

```js
let textoSuperLargo =
  "Este texto es bien largo así podemos saber varias cosas de él.";
let primerCaracter = textoSuperLargo.charAt(0);
let posicionDelUltimoCaracter = textoSuperLargo.length - 1;
let ultimoCaracter = textoSuperLargo.charAt(posicionDelUltimoCaracter);

// Accedemos al primer caracter E
console.log(primerCaracter);
console.log(ultimoCaracter);
```

#### Prácticas

- [Ejercicio 43](../ejercicios/consignas/js/ej43.md)
- [Ejercicio 44](../ejercicios/consignas/js/ej44.md)

### Recortando strings

- Utilizando el método **slice** podemos obtener una parte de un string
- Este método acepta dos parámetros slice(inicio, fin)
- Utilizamos indice desde 0 para obtener desde el inicio de la cadena

**Ejemplo:**

```js
let texto = "Me encanta JavaScript!!";
let resultado = texto.slice(11, 21);
console.log(resultado); // JavaScript
```

- Si contamos desde la primer letra tenemos 11 caracteres hasta llegar a la **J** como primer letra
- Recortamos desde la posición 11 hasta la 21, es decir que obtenemos como resultado la palabra JavaScript
- También podemos no establecer el segundo parámetro (**fin**) y obtener desde la posición especificada como inicio hasta el final del texto

**Ejemplo:**

```js
let texto = "Me encanta JavaScript!!";
let resultado = texto.slice(11);
console.log(resultado); // JavaScript!!
```

- Este método acepta como **fin** un número negativo
- Al utilizar un parámetro negativo lo que hace este método es posicionarse en el final de la cadena y volver tantos caracteres como nosotros especificamos en nuestro valor negativo

**Ejemplo:**

```js
let texto = "Me encanta JavaScript!!";
let resultado = texto.slice(11, -8);
console.log("JavaScript no es lo mismo que", resultado); // JavaScript no es lo mismo que Java
```

#### Prácticas

- [Ejercicio 45](../ejercicios/consignas/js/ej45.md)

- Otro método que podemos utilizar de forma similar es el método **substr**
- También podemos establecer 2 parámetros numéricos para obtener una porsión de una cadena de texto
- El primer parámetro establece el **inicio**
- El segundo parámetro establece la cantidad de caracteres que queremos recortar

**\*Ejemplo:**

```js
let texto = "Me encanta JavaScript!!";
let resultado = texto.substr(11, 10);
console.log(resultado); // JavaScript
```

#### Prácticas

- [Ejercicio 46](../ejercicios/consignas/js/ej46.md)

- Podes aprender más sobre estos métodos en el sitio de MDN de [slice](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/String/slice) y [substr](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/String/substr)

### Obtener un array o colección desde un String

- Por medio del método **split** podemos obtener un **array** donde cada letra ocupa un espacio dentro de esta colección
- Acepta como primer parámetro un **string** que funcione como **separador**, es decir que necesitamos ayudar al método para que sepa donde cortar.
- Nos vamos a quedar con este concepto por ahora ya que no vimos **arrays** pero los vamos a ver más adelante
- En este momento nos alcanza con saber que un **array** es un tipo base de ECMAScript y que puede almacenar distintos valores al mismo tiempo y por eso se los conoce también como colección
- Podes leer más sobre este método en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/String/split)

**\*Ejemplo:**

```js
let amigos = "tute, mati, pepe, raul, juan, marta, agus, loli";
let listaDeAmigos = amigos.split(",");
console.log(listaDeAmigos);
/* Resultado
[ 
  'tute',
  ' mati',
  ' pepe',
  ' raul',
  ' juan',
  ' marta',
  ' agus',
  ' loli' 
]
*/
```

#### Prácticas

- [Ejercicio 47](../ejercicios/consignas/js/ej47.md)
