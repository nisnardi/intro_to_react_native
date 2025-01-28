# JavaScript

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

- Este concepto es fundamental en ECMAScript y lo vamos a seguir viendo al utilizar el lenguaje
- Utilizando Callbacks es una de las varias formas que hay de hacer que nuestro código se ejecute domo si fuera sincrónico cuando no lo es

#### Prácticas

- [Ejercicio 163](../ejercicios/consignas/js/ej163.md)
- [Ejercicio 164](../ejercicios/consignas/js/ej164.md)
