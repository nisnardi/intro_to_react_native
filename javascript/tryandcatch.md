# JavaScript

## Try & Catch

- JavaScript permite utilizar `try / catch` para manejo de errores
- Cuando nuestro código se ejecuta puede eventualmente lanzar un error y está en nosotros los programadores en como queremos manejar o no ese error.
- Los errores no manejados pueden hacer crash de nuestra aplicacion mientras que si los manejamos podemos decidir como queremos que la aplicación reaccione ante los mismos

```javascript
function funcionQueTiraError() {
  throw new Error("Prueba que podemos tirar un error en JavaScript");
}

funcionQueTiraError();

console.log("Linea luego del error");
```

- En este ejemplo vemos como una función puede forzar a tirar un error utilizando el objeto Error y pasando un mensaje al construirlo
- La linea que muestra en pantalla el mensaje "linea luego del error" no se ejecuta dado que la ejecución del programa se ve interrumpida por el error ocurrido al llamar la funcion `funcionQueTiraError`
- Para evitar este problema podemos utilizar `try / catch` donde establecemos que queremos intentar correr un código y que vamos a estar atrapando los errores que puedan surgir.

```javascript
function funcionQueTiraError() {
  throw new Error("Prueba que podemos tirar un error en JavaScript");
}

try {
  funcionQueTiraError();
} catch (error) {
  console.log(`Mostramos el error: ${error}`);
}

console.log("Linea luego del error");
```

- Try / Catch tiene la siguiente estructura

```javascript
try {
  // Código que queremos ejecutar que puede tirar un error
  // Código que queremos ejecutar que puede tirar un error
  // Código que queremos ejecutar que puede tirar un error
} catch (error) {
  // Establecemos el error que queremos manejar
  // manejamos el error
}

// El código puede seguir su ejecución sin alterar la aplicación
```

- En algunos casos se puede dar que necesitamos ejecutar algo siempre después de que se ejecutó el código en el try/catch sin importar si tuvo error o no.
- Para lograr este objetivo podemos utilizar la palabra reservada `finally`.

```javascript
let loading = false;

function funcionQueTiraError() {
  throw new Error("Prueba que podemos tirar un error en JavaScript");
}

try {
  loading = true;
  funcionQueTiraError();
} catch (error) {
  console.log(`Mostramos el error: ${error}`);
} finally {
  loading = false;
}

console.log("Linea luego del error");
console.log(loading);
```

- En este caso podemos simular como si el código está cargando algún valor utilizando la variable loading.
- Lo definimos como false al declararlo porque no hay ninguna carga.
- Al entrar al try / catch podemos establecer que vamos a cargar algo y esa función falla
- Manejamos el error de carga en el catch.
- Finalmente la carga sea con error o con éxito podemos establecer que ya no se está cargando.
- De esta forma volvemos el estado a su forma original antes del error y manejamos el error para que la aplicación no se ve alterada.
- [Try & catch MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/try...catch)

#### Practica

- [Ejercicio 173](../ejercicios/consignas/js/ej173.md)
