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

[Ejercicio 27](../ejercicios/consignas/js/ej27.md)
[Ejercicio 28](../ejercicios/consignas/js/ej28.md)
[Ejercicio 29](../ejercicios/consignas/js/ej29.md)
[Ejercicio 30](../ejercicios/consignas/js/ej30.md)
[Ejercicio 31](../ejercicios/consignas/js/ej31.md)
[Ejercicio 32](../ejercicios/consignas/js/ej32.md)

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

[Ejercicio 34](../ejercicios/consignas/js/ej34.md)
[Ejercicio 35](../ejercicios/consignas/js/ej35.md)

## Operadores lógicos

- Existen operadores lógicos que nos permiten anidar condicionales
- Puedo saber si dos conciones son **true** utilizando el operador `&&` conocido como **and** o en español como **Y**
- Por ejemplo si queremos saber si el la edad del usuario es mayor de 18 años y si el password es el esperado lo podemos hacer de la siguiente manera
- Para que este operador retorne **true** ambas condiciones deben ser verdaderas

**Ejemplo**

```js
let edad = 20;
let password = "js1234";
let resultado = edad >= 18 && password === "js1234";
console.log("resultado: ", resultado); // true
```

- En este ejemplo obtenemos un valor de true ya que ambas condiciones (edad >= 18 y password === 'js1234') son verdaderas
- Existe el operador `||` conocido como **or** u **O** en español que nos permite preguntar si al menos una de 2 condiciones es verdadera.
- Si la primer condición es verdadera ya no evalúa la segunda ya que al menos una de las dos condiciones es verdadera
- Caso de que la primer condición no sea verdadera va a comprobar si la segunda lo es
- Si ninguna de las dos condiciones es verdadera retorna falso
- Este operador retorna **true** si al menos una de las condiciones es verdadera

**Ejemplo**

```js
let edad = 20;
let password = "js12345";
let resultado = edad >= 18 || password === "js1234";
console.log("resultado: ", resultado); // true
```

- En este caso la condición es verdadera ya que la edad del usuario es mayor a 18 y no importa si el password es igual o no

**Ejemplo**

```js
let edad = 10;
let password = "js1234";
let resultado = edad >= 18 || password === "js1234";
console.log("resultado: ", resultado); // true
```

- En este caso el resultado es **true** ya que el usuario no es mayor de 18 pero el password es correcto

**Ejemplo**

```js
let edad = 10;
let password = "js12345";
let resultado = edad >= 18 || password === "js1234";
console.log("resultado: ", resultado); // false
```

- En este caso la condición es **false** ya que ambas condiciones son falsas

## Negación

- Por medio del operador `!` podemos negar una condición
- Si tenemos un valor **true** negado obtenemos un valor **false**
- Si tenemos un valor **false** negado obtenemos un valor **true**

**Ejemplo**

```js
console.log(!true); // false
console.log(!false); // true
```

- Por ejemplo podemos utilizar la negación en el siguiente caso:

**Ejemplo**

```js
let edad = 21;
let resultado = edad < 18;
console.log("El usuario es mayor de edad?: ", !resultado); // la condición es false pero al negarla pasa a ser verdadera
```

#### Práctica

[Ejercicio 36](../ejercicios/consignas/js/ej36.md)
[Ejercicio 37](../ejercicios/consignas/js/ej37.md)

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

[Ejercicio 38](../ejercicios/consignas/js/ej38.md)
[Ejercicio 39](../ejercicios/consignas/js/ej39.md)

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

[Ejercicio 40](../ejercicios/consignas/js/ej40.md)

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

[Ejercicio 41](../ejercicios/consignas/js/ej41.md)
[Ejercicio 42](../ejercicios/consignas/js/ej42.md)

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

[Ejercicio 43](../ejercicios/consignas/js/ej43.md)
[Ejercicio 44](../ejercicios/consignas/js/ej44.md)

### Recortando strings

- Utilizando el método **slice** podemos obtener una parte de un string
- Este método acepta dos parámetros slice(inicio, fin)
- Utilizamos indice desde 0 para obtener desde el inicio de la cadena

**\*Ejemplo:**

```js
let texto = "Me encanta JavaScript!!";
let resultado = texto.slice(11, 21);
console.log(resultado); // JavaScript
```

- Si contamos desde la primer letra tenemos 11 caracteres hasta llegar a la **J** como primer letra
- Recortamos desde la posición 11 hasta la 21, es decir que obtenemos como resultado la palabra JavaScript
- También podemos no establecer el segundo parámetro (**fin**) y obtener desde la posición especificada como inicio hasta el final del texto

**\*Ejemplo:**

```js
let texto = "Me encanta JavaScript!!";
let resultado = texto.slice(11);
console.log(resultado); // JavaScript!!
```

- Este método acepta como **fin** un número negativo
- Al utilizar un parámetro negativo lo que hace este método es posicionarse en el final de la cadena y volver tantos caracteres como nosotros especificamos en nuestro valor negativo

**\*Ejemplo:**

```js
let texto = "Me encanta JavaScript!!";
let resultado = texto.slice(11, -8);
console.log("JavaScript no es lo mismo que", resultado); // JavaScript no es lo mismo que Java
```

#### Prácticas

[Ejercicio 45](../ejercicios/consignas/js/ej45.md)

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

[Ejercicio 46](../ejercicios/consignas/js/ej46.md)

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

[Ejercicio 47](../ejercicios/consignas/js/ej47.md)

## Métodos de Number

- Los tipos de datos **number** también tienen métodos que nos permiten obtener funcionalidades

### parseInt

- La función **parseInt** nos permite convertir un **string** a un tipo de dato **number** como número entero
- Retorna un número entero
- Podes saber más sobre esta función en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/parseInt)

**Ejemplo:**

```js
const numeroComoTexto = "3";
const numero = parseInt(numeroComoTexto);
console.log(numero); // 3
```

**Ejemplo:**

```js
const numeroComoTexto = "3.20";
const numero = parseInt(numeroComoTexto);
console.log(numero); // 3
```

- Como podemos ver en este ejemplo podemos transformar un **string** a un **number** utilizando la función **parseInt** en caso de querer un número entero
- En caso de que el **string** tenga un número decimal al utilizar la función **parseInt** obtenemos un número entero (se pierde la parte decimal)

### parseFloat

- La función **parseFloat** nos permite cambiar de tipo de dato de un **string** a number
- Retorna un número decimal
- Podes saber más sobre esta función en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/parseFloat)

**Ejemplo:**

```js
const piEnTexto = "3.14";
const pi = parseFloat(piEnTexto);
console.log(pi);
```

- Como podemos ver en este ejemplo podemos transformar un **string** a un **number** utilizando el método **parseFloat** en caso de querer un número decimal

### Convertir un número a string

- Podemos convertir un tipo de dato **number** a **string** utilizando el método **toString()**
- Retorna un string con el valor del número
- Podes saber más sobre este método en el [sitio de MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toString)

**Ejemplo:**

```js
let numero = 4;
let mensaje = numero.toString() + "2";
console.log(mensaje); // 42
```

- Podemos ver en este ejemplo como podemos transformar un tipo de dato **number** a **string**
- Obtenemos el resultado 42 ya que estamos concatenando 2 tipos de datos string

#### Prácticas

[Ejercicio 48](../ejercicios/consignas/js/ej48.md)

## Estructuras de control

- Por medio de las estructuras de control podemos controlar el flujo de nuestro código y como queremos que se ejecute según se cumplan o no algunas condiciones
- Una de las estructuras más conocidas es el **if** y en español podemos reconocerlos como **si entonces**
- Esta estructura espera una condición **true** para que ingrese y ejecute el código que tiene dentro de su bloque

![if](../assets/js/if.png)

- Como vemos en esta imágen tenemos una condición que se va a resolver en true o false
- En caso de que la condición sea verdadera (true) se va a ejecutar las distintas instrucciones
- En caso de que la condición sea negativa (false) no se ejecutan las instrucciones declaradas dentro de esta estructura y el código sigue su flujo

**Ejemplo:**

```js
// Estructura básica de un if
if (condicion) {
  // Se ejecuta el código que se escriba en esta sección si la condición es verdadera.
}
```

```js
if (true) {
  console.log("Se muestra este texto ya que la condición es true");
}
```

- Como podemos ver en el ejemplo anterior siempre se va a mostrar el mensaje ya que la condición siempre va a ser **true**
- Podemos escribir distintas condiciones que nos permitan elegir si vamos a ejecutar el código dentro de la estructura o no
- Por ejemplo podemos preguntar **SI** el **numero** es mayor o igual que 2 **Entonces** mostrar un mensaje en consola

**Ejemplo:**

```js
const numero = 2;

// SI numero >= 2 ENTONCES mostrar en consola
if (numero >= 2) {
  console.log("El numero es mayor o igual a 2");
}
```

- El flujo del código se sigue ejecutando sin importar el resultado del if

**Ejemplo:**

```js
const numero = 1;

if (numero >= 2) {
  console.log("Este mensaje no se ve");
}

console.log("Este mensaje se ve siempre se cumpla o no la condición del if");
```

#### Prácticas

[Ejercicio 49](../ejercicios/consignas/js/ej49.md)
[Ejercicio 50](../ejercicios/consignas/js/ej50.md)
[Ejercicio 51](../ejercicios/consignas/js/ej51.md)

- También existe la estructura if/else que nos permite controlar que pasa si la condición es falsa
- Es decir que en caso de que la condición sea verdadera entra en una parte de la estructura
- En caso de ser falsa la condición entonces entra en la otra sección
- Utilizamos la palabra **SI NO** para el **else**

![if/else](../assets/js/if-else.png)

**Ejemplo:**

```js
if (condicion) {
  // Entra en esta sección si se cumple la condición
} else {
  // Entra en esta sección si no se cumple la condición
}
```

```js
const numero = 2;

if (numero === 2) {
  console.log("El número es 2");
} else {
  console.log("El número no es 2");
}
```

- Podemos leer este código de la siguiente manera: SI el número es igual a 2 entonces mostrar el mensaje 'El número es 2' SINO mostrar el mensaje 'El número no es 2'

#### Prácticas

[Ejercicio 52](../ejercicios/consignas/js/ej52.md)
[Ejercicio 53](../ejercicios/consignas/js/ej53.md)
[Ejercicio 54](../ejercicios/consignas/js/ej54.md)

### Operador Ternario

- Existe una manera más corta de escribir un if/else y es por medio del operador ternario
- Se escribe de la siguiente manera: `(condicion) ? true : false`
- Es decir que dada una condición se ejecuta una parte o la otra

**Ejemplo:**

```js
let numero = 2;
let mensaje = numero === 2 ? "El numero es 2" : "El numero no es 2";
console.log(mensaje);
```

#### Prácticas

[Ejercicio 55](../ejercicios/consignas/js/ej55.md)
[Ejercicio 56](../ejercicios/consignas/js/ej56.md)
[Ejercicio 57](../ejercicios/consignas/js/ej57.md)

### If Anidados

- Podemos anidar estructuras if/else/if para validar distintas condiciones

**Ejemplo:**

```js
if (condicion) {
  // primer condicion
} else if (otraCondicion) {
  // segunda condicion
} else {
  // Si no se cumplio ninguna de las anteriores ingresa acá
}
```

```js
const nombre = "Marta";

if (nombre === "Miriam") {
  console.log("El nombre de la usuaria es Miriam");
} else if (nombre === "Felipa") {
  console.log("El nombre de la usuaria es Felipa");
} else {
  console.log("El nombre de la usuaria no es Marta ni Felipa");
}
```

- Podemos ver en este ejemplo que podemos preguntar por distintas condiciones

#### Prácticas

[Ejercicio 58](../ejercicios/consignas/js/ej58.md)
[Ejercicio 59](../ejercicios/consignas/js/ej59.md)
[Ejercicio 60](../ejercicios/consignas/js/ej60.md)

- Utilizar muchos if's anidados no es una buena práctica

### Switch

- En uno de los ejemplos anteriores necesitabamos mostrar un mensaje según el nombre del usuario

```js
const nombre = "Marta";

if (nombre === "Miriam") {
  console.log("El nombre de la usuaria es Miriam");
} else if (nombre === "Felipa") {
  console.log("El nombre de la usuaria es Felipa");
} else {
  console.log("El nombre de la usuaria no es Marta ni Felipa");
}
```

- En caso de querer seguir agregando condiciones para más nombres se nos puede volver medio caos el código

```js
const nombre = "Marta";

if (nombre === "Miriam") {
  console.log("El nombre de la usuaria es Miriam");
} else if (nombre === "Felipa") {
  console.log("El nombre de la usuaria es Felipa");
} else if (nombre === "Xime") {
  console.log("El nombre de la usuaria es Xime");
} else if (nombre === "Belu") {
  console.log("El nombre de la usuaria es Belu");
} else {
  console.log("El nombre de la usuaria no es Marta, Felipa, Xime o Belu");
}
```

- Existe otra forma de escribir esta estructura y que hace que sea más fácil leer e interpretar este código
- Esta estructura se conoce como **switch** y nos permite evaluar un valor con diferentes opciones
- Decimos SEGUN tal condicion ENTONCES hacemos tal o cual cosa

**Ejemplo:**

```js
const nombre = "marta";
let mensaje = null;

switch (nombre) {
  case "Miriam":
    mensaje = "El nombre de la usuaria es Miriam";
    break;
  case "Felipa":
    mensaje = "El nombre de la usuaria es Felipa";
    break;
  case "Xime":
    mensaje = "El nombre de la usuaria es Xime";
    break;
  case "Belu":
    mensaje = "El nombre de la usuaria es Belu";
    break;
  default:
    mensaje = "El nombre de la usuaria no es Marta, Felipa, Xime o Belu";
}

console.log(mensaje);
```

- Utilizamos **break** para decirle al **switch** que ya puede dejar de validar el resto de las condiciones y que su trabajo terminó.
- En este ejemplo podemos decir SEGUN el nombre ENTONCES mostra un mensaje personalizado SINO mostrar un mensaje que ninguno de los nombres es el correcto.

#### Prácticas

[Ejercicio 61](../ejercicios/consignas/js/ej61.md)
[Ejercicio 62](../ejercicios/consignas/js/ej62.md)
[Ejercicio 63](../ejercicios/consignas/js/ej63.md)

## Truthy and Falsy (valores verdaderos y falsos)

- En ECMAScript existen valores que se pueden transformar como **true** o **false** en una condición
- Los siguientes valores se transformar en falso:
  - false
  - null
  - undefined
  - 0
  - NaN
  - ''
- Cualquier otro valor se transforma en verdadero

**Ejemplo:**

```js
if ("") {
  // no entra en esta sección
} else {
  // entra en esta sección ya que un string vacio se transforma en falso
}
```

- Podemos ver en este ejemplo que al ECMASCript interpretar el string vacío como un valor falsy o falso no entra en la condición del if verdadero sino por el lado del falso. Es por esto que tenemos que validar nuestros datos.

**Ejemplo:**

```js
const nombre = "";
if (nombre === "") {
  console.log("por favor ingrese su nombre");
} else {
  console.log("Bienvenido/a: " + nombre);
}
```

- Por medio de condicionales podemos hacer una mejor validación
- Utilizando valores truthy y falsy podemos escribir el mismo código de la siguiente manera:

**Ejemplo:**

```js
const nombre = "";
if (nombre) {
  console.log("Bienvenido/a: " + nombre);
} else {
  console.log("por favor ingrese su nombre");
}
```

#### Prácticas

[Ejercicio 64](../ejercicios/consignas/js/ej64.md)
[Ejercicio 65](../ejercicios/consignas/js/ej65.md)

#### Estructuras de repetición

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

[Ejercicio 66](../ejercicios/consignas/js/ej66.md)
[Ejercicio 67](../ejercicios/consignas/js/ej67.md)
[Ejercicio 68](../ejercicios/consignas/js/ej68.md)
[Ejercicio 69](../ejercicios/consignas/js/ej69.md)
[Ejercicio 70](../ejercicios/consignas/js/ej70.md)
[Ejercicio 71](../ejercicios/consignas/js/ej71.md)
[Ejercicio 72](../ejercicios/consignas/js/ej72.md)
[Ejercicio 73](../ejercicios/consignas/js/ej73.md)
[Ejercicio 74](../ejercicios/consignas/js/ej74.md)
[Ejercicio 75](../ejercicios/consignas/js/ej75.md) (avanzado)

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
  console.log('número: ', numero);
  numero++;
} while (numero < 10) {
```

- En este ejemplo sólo se muestra el número 1000 y luego no se vuelve a repetir la condición.

#### Prácticas

[Ejercicio 76](../ejercicios/consignas/js/ej76.md)
[Ejercicio 77](../ejercicios/consignas/js/ej77.md)
[Ejercicio 78](../ejercicios/consignas/js/ej78.md)
[Ejercicio 79](../ejercicios/consignas/js/ej79.md)
[Ejercicio 80](../ejercicios/consignas/js/ej80.md)
[Ejercicio 81](../ejercicios/consignas/js/ej81.md)
[Ejercicio 82](../ejercicios/consignas/js/ej82.md)
[Ejercicio 83](../ejercicios/consignas/js/ej83.md)
[Ejercicio 84](../ejercicios/consignas/js/ej84.md)
[Ejercicio 85](../ejercicios/consignas/js/ej85.md)

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

[Ejercicio 86](../ejercicios/consignas/js/ej86.md)
[Ejercicio 87](../ejercicios/consignas/js/ej87.md)
[Ejercicio 88](../ejercicios/consignas/js/ej88.md)
[Ejercicio 89](../ejercicios/consignas/js/ej89.md)
[Ejercicio 90](../ejercicios/consignas/js/ej90.md)
[Ejercicio 91](../ejercicios/consignas/js/ej91.md)
[Ejercicio 92](../ejercicios/consignas/js/ej92.md)
[Ejercicio 93](../ejercicios/consignas/js/ej93.md)
[Ejercicio 94](../ejercicios/consignas/js/ej94.md)
[Ejercicio 95](../ejercicios/consignas/js/ej95.md)
[Ejercicio 96](../ejercicios/consignas/js/ej96.md)
[Ejercicio 97](../ejercicios/consignas/js/ej97.md)

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

[Ejercicio 98](../ejercicios/consignas/js/ej98.md)
[Ejercicio 99](../ejercicios/consignas/js/ej99.md)

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

[Ejercicio 100](../ejercicios/consignas/js/ej100.md)
[Ejercicio 101](../ejercicios/consignas/js/ej101.md)

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

[Ejercicio 102](../ejercicios/consignas/js/ej102.md)
[Ejercicio 103](../ejercicios/consignas/js/ej103.md)
[Ejercicio 104](../ejercicios/consignas/js/ej104.md)

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

[Ejercicio 105](../ejercicios/consignas/js/ej105.md)
[Ejercicio 106](../ejercicios/consignas/js/ej106.md)

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

[Ejercicio 107](../ejercicios/consignas/js/ej107.md)
[Ejercicio 108](../ejercicios/consignas/js/ej108.md)
[Ejercicio 109](../ejercicios/consignas/js/ej109.md)
[Ejercicio 110](../ejercicios/consignas/js/ej110.md)
[Ejercicio 111](../ejercicios/consignas/js/ej111.md)
[Ejercicio 112](../ejercicios/consignas/js/ej112.md)
[Ejercicio 113](../ejercicios/consignas/js/ej113.md)
[Ejercicio 114](../ejercicios/consignas/js/ej114.md)
[Ejercicio 115](../ejercicios/consignas/js/ej115.md)
[Ejercicio 116](../ejercicios/consignas/js/ej116.md)

#### Array

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

[Ejercicio 117](../ejercicios/consignas/js/ej117.md)
[Ejercicio 118](../ejercicios/consignas/js/ej118.md)
[Ejercicio 119](../ejercicios/consignas/js/ej119.md)

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

[Ejercicio 120](../ejercicios/consignas/js/ej120.md)
[Ejercicio 121](../ejercicios/consignas/js/ej121.md)
[Ejercicio 122](../ejercicios/consignas/js/ej122.md)

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

[Ejercicio 123](../ejercicios/consignas/js/ej123.md)
[Ejercicio 124](../ejercicios/consignas/js/ej124.md)

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

[Ejercicio 125](../ejercicios/consignas/js/ej125.md)
[Ejercicio 126](../ejercicios/consignas/js/ej126.md)
[Ejercicio 127](../ejercicios/consignas/js/ej127.md)
[Ejercicio 128](../ejercicios/consignas/js/ej128.md)
[Ejercicio 129](../ejercicios/consignas/js/ej129.md)
[Ejercicio 130](../ejercicios/consignas/js/ej130.md)
[Ejercicio 131](../ejercicios/consignas/js/ej131.md)
[Ejercicio 132](../ejercicios/consignas/js/ej132.md)
[Ejercicio 133](../ejercicios/consignas/js/ej133.md)
[Ejercicio 134](../ejercicios/consignas/js/ej134.md)

### ForEach

- Podemos iterar o recorrer un array utilizando el método forEach()
- Este método acepta una función como parámetro
- La función que le pasamos a este método recibe como parámetro cada uno de los elementos del array

**Ejemplo:**

```js
const alumnos = ["nico", "pedro", "marta", "belen", "emilia"];

alumnos.forEach(function (alumno) {
  console.log(alumno);
});
```

- En este ejemplo vemos que podemos utilizar el método forEach en el array alumnos
- Le pasamos un function como parámetro como si fuera cualquier otro tipo de parámetro (number, string, etc)
- El parámetro que recibe esta función en este caso le pusimos alumno ya que estamos recorriendo una colección de alumnos
- Le podemos poner el nombre que queremos al parámetro

**Ejemplo:**

```js
const mascotas = ["Amelia", "Ciro", "Ulises", "Carlos"];

mascotas.forEach(function (mascota) {
  console.log(mascota);
});
```

- En este caso la colección es de mascotas por lo cual utilizamos el nombre mascota para que tenga sentido que cada elemento de la colección es una mascota. Podríamos utilizar otros como item, elemento o lo que a nosotros nos guste. Siempre es mejor poner un nombre con contexto que explique de forma fácil de que es la colección que estamos iterando y los elementos que estamos utilizando

- Podemos obtener otro parámetro más en la función que se ejecuta por cada elemento que es el índice del elemento

**Ejemplo:**

```js
const mascotas = ["Amelia", "Ciro", "Ulises", "Carlos"];

mascotas.forEach(function (mascota, indice) {
  console.log("indice", indice);
  console.log(mascota);
});
/*
indice 0
Amelia
indice 1
Ciro
indice 2
Ulises
indice 3
Carlos
*/
```

- Vemos en este ejemplo que agregando un segundo parámetro podemos obtener el índice de los elementos y como primer valor el elemento en sí.

#### Prácticas

[Ejercicio 135](../ejercicios/consignas/js/ej135.md)
[Ejercicio 136](../ejercicios/consignas/js/ej136.md)

### Map

- El método **map** crea un nuevo **array** con el resultado de la función que le pasamos como parámetros
- Podemos utilizar este método para cambiar los valores que tenemos en un array
- En la función que pasamos como parámetro tenemos que retornar el elemento que queremos en el nuevo array

**Ejemplo:**

```js
const mascotas = ["Amelia", "Ciro", "Ulises", "Carlos"];
const mascotasMayuscula = mascotas.map(function (mascota) {
  return mascota.toUpperCase();
});

console.log(mascotasMayuscula); // [ 'AMELIA', 'CIRO', 'ULISES', 'CARLOS' ] Todos en mayúscula
console.log(mascotas); // ['Amelia', 'Ciro', 'Ulises', 'Carlos'] Este array quedó igual que antes
```

- En este ejemplo vemos como podemos utilizar **map** para crear un nuevo array modificando los valores de otro array
- El array original queda intacto

#### Prácticas

[Ejercicio 137](../ejercicios/consignas/js/ej137.md)
[Ejercicio 138](../ejercicios/consignas/js/ej138.md)

### Filter

- El método **filter** retorna un nuevo **array** utilizando un filtro
- Pasamos una función que retorna verdadero o falso para saber si debemos añadir el nuevo elemento al nuevo array o no

**Ejemplo:**

```js
const notas = [1, 2, 3, 4, 10, 5];
const notasGrosas = notas.filter(function (nota) {
  return nota === 10;
});

console.log(notasGrosas); // [10] array con una sola nota grosa
console.log(notas); // [1, 2, 3, 4, 10, 5] array original
```

#### Prácticas

[Ejercicio 139](../ejercicios/consignas/js/ej139.md)
[Ejercicio 140](../ejercicios/consignas/js/ej140.md)

### Reduce

- El método **reduce** nos permite recorrer un array y obtener un sólo dato como resultado final
- Acepta una función con dos parámetro
  - Primer parámetro es el acumulador
  - El segundo valor es cada item en el array
- Podemos utilizar el acumulador para ir sumando valores, por ejemplo:

**Ejemplo:**

```js
const notas = [1, 2, 3, 4, 10, 5];
const sumaDeNotas = notas.reduce(function (total, nota) {
  return total + nota;
});

console.log(sumaDeNotas); // 25 resultado final de sumar todas las notas
```

#### Prácticas

[Ejercicio 141](../ejercicios/consignas/js/ej141.md)
[Ejercicio 142](../ejercicios/consignas/js/ej142.md)

- Podes ver más métodos de array en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array)

## Objectos

- Otro de los tipos base que tenemos en ECMAScript son los **object**, es decir que tenemos objetos
- Los objetos nos ayudan a representar valores de una manera más fácil y agrupada
- Los objetos literales se escriben entre {}

**Ejemplo:**

```js
{
} // objeto literal
const miObjeto = {}; // objeto asignado a una variable
```

#### Prácticas

[Ejercicio 143](../ejercicios/consignas/js/ej143.md)

### Propiedades

- Un objeto puede tener propiedades
- Las propiedades se definen con un nombre como si fueran variables
- A las propiedades se les puede asignar un valor utilizando dos puntos
- Las propiedades se separan con comas

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

console.log(persona);
```

- Podemos acceder a la propiedad de un objeto utilizando el nombre del objeto, punto y el nombre de la propiedad

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

console.log(persona.nombre);
console.log(persona.edad);
```

#### Prácticas

[Ejercicio 144](../ejercicios/consignas/js/ej144.md)
[Ejercicio 145](../ejercicios/consignas/js/ej145.md)
[Ejercicio 146](../ejercicios/consignas/js/ej146.md)
[Ejercicio 147](../ejercicios/consignas/js/ej147.md)

- Si accedemos a una propiedad que no existe vamos a obtener undefined

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

console.log(persona.dni); // undefined
```

- Para asignar un valor a una propiedad lo hacemos de la misma forma que lo hacemos con una variable

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

persona.nombre = "Martín";
persona.edad = 20;

console.log(persona);
// { nombre: 'Martín', edad: 20 }
```

- Las propiedades de un objeto terminan siendo variables de las cuales podemos obtener o asignar valores
- Un tema importante con los objetos de ECMAScript es que son dinámicos
- Podemos crear propiedades que no fueron definidas en el objeto
- Si bien es un gran beneficio tener esta flexibilidad nos puede dar un dolor de cabeza si no tenemos cuidado

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

console.log(persona.dni); // undefined

persona.nombre = "Martín";
persona.edad = 20;
persona.dni = 20202123;

console.log(persona);
// { nombre: 'Martín', edad: 20, dni: 20202123 }

console.log(persona.dni); // 20202123
```

- Podemos caer en el error de escribir mal una propiedad o por ahí utilizar mayúscula y no encontrar la propiedad buscada o eventualmente terminar creando nuevas propiedades
- De nuevo, por las dudas... tener cuidado con las propiedades de los objetos de ECMAScript

#### Prácticas

[Ejercicio 148](../ejercicios/consignas/js/ej148.md)
[Ejercicio 149](../ejercicios/consignas/js/ej149.md)

### Métodos

- Los objetos pueden tener métodos
- Un método es una propiedad que tiene una función

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  saludar: function () {
    console.log("Hola, cómo estan?");
  },
};
```

- Como podemos ver nombre y saludar son dos propiedades iguales
- Nombre tiene asinado un string
- Saludar tiene asignado una función como vimos antes

**Ejemplo:**

```js
const saludar = function () {
  console.log("Hola, cómo estan?");
};

saludar();
```

- Para ejecutar un método de un objeto lo hacemos de la misma forma casi:

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  saludar: function () {
    console.log("Hola, cómo estan?");
  },
};

persona.saludar(); // Hola, cómo estan?
```

#### Prácticas

[Ejercicio 150](../ejercicios/consignas/js/ej150.md)
[Ejercicio 151](../ejercicios/consignas/js/ej151.md)

- Cuando utilizamos métodos de string, number o arrays estabamos utilizando funciones propias de cada uno de estos tipos.
- **ECMAScript transforma los strings, numbers y arrays a objetos para poder utilizar métodos sobre estos tipos de datos**

- Un método también puede aceptar parámetros:

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  saludar: function (nombre) {
    console.log("Hola, " + nombre + " cómo estas?");
  },
};

persona.saludar("Marta"); // Hola, Marta cómo estas?
```

- Vemos que utilizar un método es muy similar a simplemente utilizar una función
- Esto se da porque un método es una función dentro de un objeto
- Dentro de los métodos también podemos acceder a las propiedades del objeto por medio de la palabra reservada **this**
- Por ahora podemos decir que **this** es una referencia al objeto que creamos

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  saludar: function () {
    console.log("Hola, mi nombre es " + this.nombre);
  },
};

persona.saludar(); // Hola, mi nombre es Nico
```

#### Prácticas

[Ejercicio 152](../ejercicios/consignas/js/ej152.md)
[Ejercicio 153](../ejercicios/consignas/js/ej153.md)
[Ejercicio 154](../ejercicios/consignas/js/ej154.md)
[Ejercicio 155](../ejercicios/consignas/js/ej155.md)
[Ejercicio 156](../ejercicios/consignas/js/ej156.md)
[Ejercicio 157](../ejercicios/consignas/js/ej157.md)
[Ejercicio 158](../ejercicios/consignas/js/ej158.md)

- También dentro de un método podemos modificar una propiedad de un objeto

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
  saludar: function () {
    console.log("Hola, mi nombre es " + this.nombre);
  },
  cumpleanios: function () {
    this.edad++;
  },
};

console.log(persona.edad); // 38
persona.cumpleanios();
console.log(persona.edad); // 39
```

### Propiedades dinámicas de un objeto

- Puede pasar que no sabemos el nombre de una propiedad y necesitemos acceder de forma dinámica
- Podemos acceder a las propiedades utilizando los corchetes como si fueran array pero en lugar de pasarle un ídince numérico le pasamos el nombre de la propiedad

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
  saludar: function () {
    console.log("Hola, mi nombre es " + this.nombre);
  },
  cumpleanios: function () {
    this.edad++;
  },
};

console.log(persona["nombre"]); // nico
console.log(persona["edad"]); // 38
```

- Podemos hacer esto utilizando variables

**Ejemplo:**

```js
const nombre = "nombre";
const edad = "edad";

const persona = {
  nombre: "Nico",
  edad: 38,
  saludar: function () {
    console.log("Hola, mi nombre es " + this.nombre);
  },
  cumpleanios: function () {
    this.edad++;
  },
};

console.log(persona[nombre]); // nico
console.log(persona[edad]); // 38
```

#### Prácticas

[Ejercicio 159](../ejercicios/consignas/js/ej159.md)
[Ejercicio 160](../ejercicios/consignas/js/ej160.md)

- De esta forma podemos acceder a propiedades de un objeto de forma dinámica
- Esto es útil si lo usamos con `Object.keys`
- `Object.keys` retorna todas las propiedades de un objeto
- El método keys acepta un objeto como parámetro

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

const propiedades = Object.keys(persona);

propiedades.forEach(function (propiedad) {
  console.log(persona[propiedad]);
});
```

- Si agregamos más propiedades el código sigue pudiendo acceder a las propiedades de forma dinámica

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

persona.dni = 20202138;
persona.calle = "arcos 220";

const propiedades = Object.keys(persona);

propiedades.forEach(function (propiedad) {
  console.log(persona[propiedad]);
});
/*
  Nico
  38
  20202138
  arcos 220
*/
```

- Podes leer más sobre `Object.keys` en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Object/keys)

#### Prácticas

[Ejercicio 161](../ejercicios/consignas/js/ej161.md)
[Ejercicio 162](../ejercicios/consignas/js/ej162.md)

## Callback

- Se conoce como **callback** cuando pasamos una función como parámetro a otra función
- Dado que ECMAScript es asyncrónico necesitamos una forma de saber si algo se termino de ejecutar o no

**Ejemplos:**

```js
function hacerAlgo(funcionComoParametro) {
  console.log("hacer algo");
  funcionComoParametro();
}

let termino = function () {
  console.log("termino");
};

hacerAlgo(termino);
```

- En este ejemplo declaramos una función **hacerAlgo** que espera otra función como parámetro
- La función **hacerAlgo** muestra en pantalla el mensaje 'hacer algo' y luego ejecuta la función que le pasaron como parámetro
- Como la función que le pasamos es la declarada en la variable **termino** al finalizar la ejecución de la función **hacerAlgo** muestra el mensaje 'termino'
- Una forma más simple de entender esto puede ser dividir los llamados de la siguiente forma:

**Ejemplos:**

```js
let termino = function () {
  console.log("termino");
};

function hacerAlgo() {
  console.log("hacer algo");
  termino();
}

hacerAlgo();
```

- Si bien estos dos ejemplos hacen la misma tarea en el primero estamos utilizando una función como parámetro
- En el segundo estamos utilizando una función global para hacer algo similar a lo que hacemos con un callback
- Los conceptos importantes de callback son:
  - Un callback es una función que se pasa como parámetro
  - Una función termina llamando a otra función que le pasaron como parámetro

**Ejemplos:**

```js
let numero = 0;

function sumar(n, callback) {
  n++;
  callback(n);
}

sumar(numero, function (resultado) {
  console.log(resultado); // 1
});

console.log(numero); // 0
```

- Un callback puede recibir uno o muchos parámetros también
- En este ejemplo vemos como le pasamos un valor numérico a la funcion sumar
- Luego de realizar la operación la función sumar llama al callback pasando el número incrementado
- También podemos ver este ejemplo de la siguiente manera:

**Ejemplos:**

```js
let numero = 0;

let resultadoSuma = function (resultado) {
  console.log(resultado);
};

function sumar(n, callback) {
  n++;
  callback(n);
}

sumar(numero, resultadoSuma);

console.log(numero); // 0
```

- Utilizamos este concepto sin saberlo al aprender iteradores de arrays:

**Ejemplos:**

```js
let numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Callback
numeros.forEach(function (numero) {
  console.log(numero);
});

// Callback
let numerosPares = numeros.filter(function (numero) {
  return numero % 2 === 0;
});

// Callback
let resultado = numeros.reduce(function (resultado, numero) {
  return resultado + numero;
});

// Callback
let numerosModificados = numeros.map(function (numero) {
  return numero + 10;
});
```

- Podemos ver que estos iteradores reciben una función como parámetro que utilizan para ejecutar una acción definida según cada caso
- En el forEach le pasamos un callback para que muestre o haga algo con cada número
- En el filter le pasamos una función como callback que filtra los números retornando true o false según el criterio esperado
- En el reducer le pasamos un callback que toma 2 parámetros, el primero es el número anterior y el segundo es el número que se está iterando
- En el map pasamos un callback para que modifique o haga algo con cada elemento del array números

**Ejemplos:**

```js
$(function () {
  console.log("ready!");
});
```

- Si usaste jQuery en algún momento podes haber copiado este código varias veces para controlar si la librería se cargó o no
- Podemos ver que al $() de jQuery le pasamos ni más ni menos que una función como parámetro
- Si, le estamos pasando un callback
- La idea es que de esta forma jQuery controla que este cargado y listo para ser utilizado y luego ejecuta los callbacks que le pasaron
- Este concepto es fundamental en ECMAScript y lo vamos a seguir viendo al utilizar el lenguaje tanto en el browser como en Node
- Utilizando Callbacks es una de las varias formas que hay de hacer que nuestro código se ejecute domo si fuera sincrónico cuando no lo es

## Hoisting

- **Hoisting** significa elevación en inglés
- ECMASCript fué creado con la idea que sea un lenguaje fácil de usar y aprender

**Ejemplo:**

```js
saludar(); // Hola, estoy mostrando un mensaje sin estar declarado

function saludar() {
  console.log("Hola, estoy mostrando un mensaje sin estar declarado");
}
```

- En ECMASCript podemos hacer esto gracias al concepto de **Hoisting**
- Al correr un script el motor lee 2 veces el código
- En la primer pasada se fija las declaraciones de las variables, funciones y las lleva a la parte superior del código
- En la segunda pasada ejecuta las asignaciones y el resto del código

**Ejemplo:**

```js
function saludar() {
  console.log("Hola, estoy mostrando un mensaje sin estar declarado");
}

saludar(); // Hola, estoy mostrando un mensaje sin estar declarado
```

- Esta es la forma correcta de escribir este código
- Primero declaramos las variables y funciones que necesitamos y luego las utilizamos
- Si bien el lenguaje no lo fuerza nos podemos ahorrar muchos problemas y utilizar una buena práctica
- Podes leer más sobre hoisting en el [sitio de MDN](https://developer.mozilla.org/es/docs/Glossary/Hoisting)

## Scope

- Se llama **scope** al alcance de un valor o expresión
- Dicho de una forma más fácil por medio del scope puedo saber si puedo o no acceder por ejemplo a una variable
- En ECMAScript tenemos variables que son globales y se pueden acceder desde cualquier parte del código

**Ejemplo:**

```js
var nombre = "Pedro";

function mostrarNombre() {
  console.log(nombre);
}

mostrarNombre(); // Pedro
console.log(nombre); // Pedro
```

- En este ejemplo declaramos la variable **nombre** como global ya que está declarada en el cuerpo de nuestro programa
- Dado que es una variable global la podemos acceder desde cualquier lado
- Dado que **nombre** es una variable global la podemos modificar desde adentro de una función
- Esto no es una buena práctica dado que las funciones tiene que recibir todos los valores que necesiten como parámetros para evitar problemas

**Ejemplo:**

```js
var nombre = "Pedro";

function mostrarNombre() {
  nombre = "Marta";
  console.log(nombre);
}

console.log(nombre); // Pedro

mostrarNombre();
console.log(nombre); // Marta
```

- También existen las variables locales que sólo pueden ser accedidas desde el mismo lugar donde fueron declaradas

**Ejemplo:**

```js
function mostrarNombre() {
  var nombre = "Marta";
  console.log(nombre);
}

mostrarNombre();
console.log(nombre); // nombre is not defined
```

- En este ejemplo la variable **nombre** es local ya que solo puede ser accedida desde adentro de la función mostrarNombre donde fué declarada
- La regla de oro acá es que se pueden ver las variables desde adentro para afuera (les juro que ya va a tomar sentido esta frase)
- ECMASCript no tenía scope a nivel bloque hasta que salieron let y const

**Ejemplo:**

```js
{
  var nombre = "Marta";
  console.log(nombre); // Marta
}

console.log(nombre); // Marta

{
  let otroNombre = "Pepe";
  console.log(otroNombre); // Pepe
}

console.log(otroNombre); // otroNombre is not defined
```

- Al utilizar **var** la variable es declarada como global por más que está en un bloque
- Cuando se incorpora **let** y **const** esto cambio ya que ahora las variables tienen scope de bloque
- Gracias a esta funcionalidad nos ahorramos varios dolores de cabeza y usamos **let** en lugar de var

### Funciones anidadas

- Dentro de una función podemos tener otras funciones
- Al tener una función dentro de otra la función hija no es accesible desde afuera de la función padre

**Ejemplo:**

```js
function bienvenido() {
  function saludar() {
    console.log("Hola Coquito!!!");
  }
  saludar();
}

bienvenido(); // Hola Coquito!!!
saludar(); // saludar is not defined
```

- Podemos ver en este ejemplo que la función bienvenido es global y la puedo llamar desde cualquier parte del código
- La función saludar es de ámbito local y sólo puede ser accedida desde dentro de la función bienvenido donde fue declarada

**Ejemplo:**

```js
let nombre = "Coco";

function bienvenido() {
  console.log(nombre);

  function saludar() {
    console.log(nombre);
  }

  saludar();
}

bienvenido(); // muestra Coco 2 veces
console.log(nombre); // Coco
```

- Al declarar la variable **nombre** como global la podemos acceder desde las dos funciones sin importar si están una dentro de la otra

**Ejemplo:**

```js
let nombre = "Coco";

function bienvenido() {
  let saludo = "Hola ";
  console.log(saludo);

  function saludar() {
    console.log(saludo);
  }

  saludar();
}

bienvenido(); // muestra Hola 2 veces
console.log(nombre); // Coco
console.log(saludo); // saludo is not defined
```

- La variable **saludo** esta declarada como local en la función **bienvenido**
- Dado que es una variable local no la podemos acceder desde afuera del lugar donde fué declarada
- Por otro lado si la podemos acceder desde la función **saludar** que está dentro de la función **bienvenido**
- Podemos decir que las funciones hijas tienen acceso al scope de las funciones padres

**Ejemplo:**

```js
let nombre = "Coco";

function bienvenido() {
  let saludo = "Hola ";

  function saludar() {
    let mensaje = saludo + nombre;
    console.log(mensaje);
  }

  saludar();
  console.log(mensaje); // mensaje is not defined
}

bienvenido(); // muestra Hola 2 veces
console.log(nombre); // Coco
console.log(saludo); // saludo is not defined
console.log(mensaje); // mensaje is not defined
```

- La variable **mensaje** está declarada como local de la función **saludar**
- Es por esto que no la podemos acceder ni desde la función **bienvenido** como tampoco desde el scope global

**Ejemplo:**

```js
function bienvenido(nombre) {
  let mensaje = "Bienvenido";

  function saludar(valor) {
    return mensaje + " " + valor;
  }

  return saludar(nombre);
}

console.log(bienvenido("Coco")); // Bienvenido Coco
```

- Las funciones hijos tienen llegada hasta a los parámetros que se le pasan a la función padre
- Este concepto se conoce como Clojure
- Podes leer más sobre este concepto en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Closures)

## Más sobre funciones

### Arguments

- Dentro de las funciones podemos acceder a un valor parecido a un array que se conoce como **arguments**
- Este valor contiene todos los parámetros que le pasaron a la función
- Arguments tiene la propiedad length para saber la cantidad de parámetros que fueron pasados
- El valor retornado por arguments es un objeto

**Ejemplo:**

```js
function saludar() {
  console.log(arguments); // { '0': 'Jarry', '1': 'Coco', '2': 'Nico' }
  console.log(arguments.length); // 3
  console.log(arguments[0]);
}

saludar("Jarry", "Coco", "Nico");
```

- Dado que es similar a un array podemos acceder a sus valores utilizando índices que comienzan en 0

**Ejemplo:**

```js
function saludar() {
  console.log(arguments[0]); // Jarry
  console.log(arguments[1]); // Coco
  console.log(arguments[2]); // Nico
}

saludar("Jarry", "Coco", "Nico");
```

#### Prácticas

[Ejercicio](../ejercicios/consignas/js/ej.md)

### Recursividad

- En ECMAScript podemos hacer que una función se llame a si misma
- Este concepto se conoce como **recursividad**
- Al igual que en las estructuras de repeteción es importante recordar que necesitamos cortar la recursividad en algún momento

**Ejemplo:**

```js
function mostrarNumero(numero) {
  if (numero <= 10) {
    console.log(numero);
    numero++;
    mostrarNumero(numero);
  }
}

mostrarNumero(0);
```

- La función **mostrarNumero** es recursiva ya que se llama así misma
- Si el número es mayor que 10 la función se deja de autollamar

### Función que retorna otra función

- Como ya vimos una función puede retornar un valor
- Las funciones son un valor
- Por lo cual las funciones pueden retornar un valor que es una función

**Ejemplo:**

```js
function saludar() {
  let otraFuncion = function () {
    console.log("hola, esto me vuela la peluca");
  };
  return otraFuncion;
}

let miFuncion = saludar(); // Este llamado retorna una función
console.log(typeof miFuncion); // function

miFuncion(); // ejecuto la función y se muestra en consola: hola, esto me vuela la peluca
```

- Dado esta ventaja que tiene ECMAScript podemos hacer uso del scope y las variables locales para hacer cosas como estas:

**Ejemplo:**

```js
function sumar(numero) {
  let sumarLosDosNumeros = function (otroNumero) {
    return numero + otroNumero;
  };
  return sumarLosDosNumeros;
}

let sumando = sumar(10);
let resultado = sumando(20);
console.log(resultado); // 30
```

- En este caso ejecutamos la función sumar y le pasamos un valor de 10
- La función sumar retorna una nueva función que es la de sumarLosDosNumeros
- Esta nueva función que obtenemos como resultado acepta un parámetro
- Guardamos la nueva función en la variable sumando
- Al ejecutar la función que tenemos guardada en la variable sumando le podemos pasar un parámetro nuevo (otro número), en este caso 20
- Al ejecutar la función guardada en la variable sumando retorna la suma de los 2 números y retorna el resultado (30)
- Es decir que al ejecutar la función suma y pasarle un parámetro nos retorna una función que guarda el contexto (el parámetro 10)
- Al ejecutar la función retornada... sigue teniendo el valor 10 y utiliza el nuevo valor para obtener la suma de los 2
- BUMMMMM nos explota el cerebro!! Oficialmente BIENVENIDOS A ECMAScript!!

## Modo estricto

- ECMAScript 5 tiene un modo considerado estricto que nos permite tener menos errores
- Para establecer este modo tenemos que agregar la siguiente sentencia en la parte superior de nuestro código `"use strict";`

**Ejemplo:**

```js
nombre = "Marta";
console.log(nombre);
```

- En ECMAScript5 este código funciona sin problema y no nos notifica que estamos declarando la variable **nombre** como global al no utilizar **var**

**Ejemplo:**

```js
"use strict";
var nombre;
nombre = "Marta";
console.log(nombre); // Marta
```

- Al utilizar el modo estricto nos va a tirar un error ya que espera que declaremos primero la variable y luego le asignemos un valor
- Como podemos ver el modo estricto nos ayuda a cometer menos errores
- Existen varios casos más donde este modo nos puede ayudar
- Podes leer más sobre este concepto en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Modo_estricto)

## Parámetros por copia o referencia

- En programación existen los valores por copia o referencia
- Al pasar o asignar un valor por copia literalmente se genera un nuevo valor dado el valor inicial

**Ejemplo:**

```js
var numero1 = 10;
var numero2 = numero1;

console.log(numero1); // 10
console.log(numero2); // 10
console.log(numero1 === numero2); // true

numero1 = 20;
console.log(numero1); // 20
console.log(numero2); // 10
console.log(numero1 === numero2); // false
```

- En este caso vemos que la variable numero2 tiene asignado el valor de la variable numero1
- Al cambiar el valor de la variable numero1 no se ve afectado el valor de la variable numero2
- En este caso ECMAScript está copiando el valor que tiene guardado en memoria la variable numero1 y asignando la copia a la variable numero2, es decir que son valores individuales y por eso los podemos modificar sin problema

**Ejemplo:**

```js
var persona1 = { nombre: "Marta" };
var persona2 = persona1;

console.log(persona1.nombre); // Marta
console.log(persona2.nombre); // Marta
console.log(persona2 === persona1); // true

persona1.nombre = "Pedro";
console.log(persona1.nombre); // Pedro
console.log(persona2.nombre); // Pedro
console.log(persona2 === persona1); // true
```

- En este ejemplo podemos ver que se da un efecto totalmente distinto al anterior
- Al utilizar arrays u objetos, ECMAScript asigna una referencia en lugar de un valor
- Cuando asignamos la variable **persona1** a **persona2** estamos asignando la referencia y no el valor, es decir que al cambiar el objeto **persona1** cambia también **persona2**
- Esto se da ya que un objeto o array pueden ser muy grande y copiarlo nos puede consumir mucha memoria
- Para poder clonar un objeto y hacer que sean instancias individuales tenemos que utilizar el método `Object.assign`
- Este método es de ECMAScript6

**Ejemplo:**

```js
var persona1 = { nombre: "Marta" };
var persona2 = Object.assign({}, persona1);

console.log(persona1.nombre); // Marta
console.log(persona2.nombre); // Marta
console.log(persona2 === persona1); // false

persona1.nombre = "Pedro";
console.log(persona1.nombre); // Pedro
console.log(persona2.nombre); // Marta
console.log(persona2 === persona1); // false
```

- Tenemos que tener en cuenta que el método assign copia por referencia los objetos anidados
- Podes leer más sobre este método en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Object/assign)

**Ejemplo:**

```js
function pusheame(coleccion, valor) {
  coleccion.push(valor);
}

var nombres = [];
pusheame(nombres, "Marta");
pusheame(nombres, "Pedro");
pusheame(nombres, "Juan");
pusheame(nombres, "Karen");

console.log(nombres); // ['Marta', 'Pedro', 'Juan', 'Karen']
```

- En este ejemplo vemos que al pasar un array como parámetro no estamos pasando una copia del mismo sino realmente el array original
- Es por esto que podemos agregarles valores casi como si usamos la variable nombres como una variable global
- Este tipo de mutaciones nos pueden traer problemas ya que podemos no darnos cuentas que estamos modificando algo que no queríamos modificar

**Ejemplo:**

```js
function pusheame(coleccion, valor) {
  // slice genera un nuevo array desde el anterior
  let nuevoArray = coleccion.slice(0);
  nuevoArray.push(valor);
  return nuevoArray;
}

var nombres = [];
nombres = pusheame(nombres, "Pedro");
nombres = pusheame(nombres, "Marta");
console.log(nombres); // ['Pedro', 'Marta']
```

- En este caso vemos como la función retorna un nuevo array que es una copia del anterior pero con el cambio que necesitamos
- La función siempre retorna un array nuevo modificado
- De esta forma nos evitamos un problema
- Tenemos que tener cuidado si los arrays son muy grandes ya que eso puede consumir mucha memoria

## Objectos avanzado

- Métodos de un objeto
- Prototype
- Funciones constructoras
- Clases
