# JavaScript

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
