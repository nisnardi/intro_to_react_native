# JavaScript

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

- [Ejercicio 48](../ejercicios/consignas/js/ej48.md)
