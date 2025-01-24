# JavaScript

## Promises

- `JavaScript es un lenguaje asyncrono`, lo que significa que puede ejecutar tareas que tarden más tiempo con la posibilidad de no bloquear la ejecución del código y seguir respondiendo.
- Llamados que bloquean la ejecución del código hacen que el programa no pueda seguir ejecutandose hasta que termine el proceso bloquante.
- En procesos normales esperamos el siguiente resultado.

```javascript
console.log("primer llamado");
console.log("segundo llamado");
console.log("tercero llamado");

// En este caso veremos en pantalla los mensajes en el orden que fueron codificados
```

```javascript
// Ejemplo no real
funcionQueTardaMuchoTiempoEnResolver(); // Esto bloquea la ejecución del programa
console.log("fin del proceso largo");
```

- En este caso vemos como la llamada `funcionQueTardaMuchoTiempoEnResolver` tarda mucho y bloquea la ejecución del código.
- La linea final se va a ejecutar recién cuando termine el llamado de la función anterior.
- En JavaScript tenemos la opción de manejar que vamos a hacer cuando un llamado tarde mucho sin bloquear el código.

```javascript
funcionQueTardaMuchoTiempoEnResolver(() => {
  console.log("fin del proceso largo");
});
console.log("El código sigue ejecutando");
```

- Si ejecutamos este código definiendo bien que hace la función `funcionQueTardaMuchoTiempoEnResolver` se ve primero la frase `El código sigue ejecutando` y luego `fin del proceso largo` ya que JavaScript no bloquea la ejecución.
- JavaScript permite pasar una función como `callback` a otra función para que en algún momento pueda llamar a la función que fué pasda por parámetro

```javascript
function usandoCallbacks() {
  console.log("Antes del for");
  for (let index = 0; index <= 10000000000; index++) {}
  console.log("Fin del for");
}

usandoCallbacks();
console.log("El código sigue funcionando");
```

- Aún en JavaScript yo puedo escribir código bloqueante sin quererlo.
- En este caso ejecuta un for que tarda mucho y mientras eso pasa JavaScript no puede seguir adelante.
- Usando callbacks yo puedo establecer que tiene que hacer el código cuando termine esa función.

```javascript
function usandoCallbacks(callback) {
  console.log("Antes del for");
  for (let index = 0; index <= 10000000000; index++) {}
  callback();
}

usandoCallbacks(() => {
  console.log("Fin del for");
});

console.log("El código sigue funcionando");
```

- Muchas veces se puede dar lo que se conoce como `callback hell` dónde hay muchas funciones anidadas que llaman callbacks cuando terminan una ejecución.

```javascript
// Ejemplo - No es código real
function useCallback1(callback1) {
  function useCallback2(callback2) {
    function useCallback3(callback) {
      callback();
    }
    useCallback3(callback2);
  }
  useCallback2(callback1);
}

useCallback1(callback1);
```

- JavaScript tiene una forma de no bloquar el código y manejar el callback hell llamado `Promise`.
- Promises en JavaScript es una manera de manejar operaciones asyncrónicas.
- Promises representan un valor que puede estar disponible ahora, en el futuro o nunca.
- Una Promise es un objeto que representa un operación asyncrona que tiene 3 estados:
  - Pending: pendiente, que significa que no fue completada aún.
  - Fullfiled: resuelta, que significa que la operación fue completada y sin error.
  - Rejected: rechazada, que significa que la promise encontró algún error y no se resolvió con éxito.

```javascript
const promesa = new Promise(() => {});
console.log(promesa);
// Promise { <pending> }
```

- Por medio de `new Promise()` podemos crear una nueva promesa.
- El estado inicial de una promesa es que no está `pending`.

```javascript
const promesa = new Promise(() => {});
console.log(promesa);
// Promise { <pending> }
```

- Promise acepta una función como parámetro con un callback al que llamar cuando se resuelva de manera exitosa.
- Una promise tiene le método `then` que nos permite establecer que debe pasar o que código debe ejecutarse cuando la promesa se resuelva con éxito.
- Then acepta también un callback que se va a ejecutar cuando la promesa se resuelva.

```javascript
const promesa = new Promise((resolve) => {
  resolve("Se resolvió con éxito la promesa");
});

promesa.then((mensaje) => {
  console.log(mensaje);
  console.log(promesa);
});

// Se resolvió con éxito la promesa
// Promise { 'Se resolvió con éxito la promesa' }
```

- Promise acepta como segundo parámetro una segunda función como parámetro que se puede ejecutar cuando la promesa encuentre algún error.
- Promise tiene un método `catch` que se puede utilizar para definir que queremos que haga el código en caso de que ocurra algún error en la ejecución.

```javascript
const promesa = new Promise((resolve) => {
  const error = true;

  if (error) {
    reject(new Error("Algo salió mal"));
  } else {
    resolve("Se resolvió con éxito la promesa");
  }
});

promesa
  .then((mensaje) => {
    console.log(mensaje);
  })
  .catch((error) => {
    console.log(error);
    console.log(promesa);
  });
```

```bash
Error: Algo salió mal
    at /Users/nicolasisnardi/Projects/content/intro_to_react_native_code/contenido/promise.js:49:12
    at new Promise (<anonymous>)
    at Object.<anonymous> (/Users/nicolasisnardi/Projects/content/intro_to_react_native_code/contenido/promise.js:45:17)
    at Module._compile (node:internal/modules/cjs/loader:1562:14)
    at Object..js (node:internal/modules/cjs/loader:1699:10)
    at Module.load (node:internal/modules/cjs/loader:1313:32)
    at Function._load (node:internal/modules/cjs/loader:1123:12)
    at TracingChannel.traceSync (node:diagnostics_channel:322:14)
    at wrapModuleLoad (node:internal/modules/cjs/loader:217:24)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:170:5)
Promise {
  <rejected> Error: Algo salió mal
      at /Users/nicolasisnardi/Projects/content/intro_to_react_native_code/contenido/promise.js:49:12
      at new Promise (<anonymous>)
      at Object.<anonymous> (/Users/nicolasisnardi/Projects/content/intro_to_react_native_code/contenido/promise.js:45:17)
      at Module._compile (node:internal/modules/cjs/loader:1562:14)
      at Object..js (node:internal/modules/cjs/loader:1699:10)
      at Module.load (node:internal/modules/cjs/loader:1313:32)
      at Function._load (node:internal/modules/cjs/loader:1123:12)
      at TracingChannel.traceSync (node:diagnostics_channel:322:14)
      at wrapModuleLoad (node:internal/modules/cjs/loader:217:24)
      at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:170:5)
}
```

- Las Promises pueden ser anidadas

```javascript
const promesa = new Promise((resolve, reject) => {
  const error = false;

  if (error) {
    reject(new Error("Algo salió mal"));
  } else {
    resolve("Se resolvió con éxito la promesa");
  }
});

promesa
  .then((mensaje) => {
    console.log(mensaje);

    return new Promise((resolve) => {
      resolve("mensaje 2");
    });
  })
  .then((mensaje) => {
    console.log(mensaje);

    return new Promise((resolve) => {
      resolve("mensaje 3");
    });
  })
  .then((mensaje) => {
    console.log(mensaje);
  })
  .catch((error) => {
    console.log(error);
    console.log(promesa);
  });
```

- Las promises también tienen un método llamado `finally` que se ejecuta luego que se resolvió.

```javascript
const promesa = new Promise((resolve, reject) => {
  const error = false;

  if (error) {
    reject(new Error("Algo salió mal"));
  } else {
    resolve("Se resolvió con éxito la promesa");
  }
});

promesa
  .then((mensaje) => {
    console.log(mensaje);

    return new Promise((resolve) => {
      resolve("mensaje 2");
    });
  })
  .then((mensaje) => {
    console.log(mensaje);

    return new Promise((resolve) => {
      resolve("mensaje 3");
    });
  })
  .then((mensaje) => {
    console.log(mensaje);
  })
  .catch((error) => {
    console.log(error);
    console.log(promesa);
  })
  .finally(() => {
    console.log("terminó todo amigos!");
  });
```

- `finally` se ejecuta sin importar que la Promise se resuleva con éxito o con error

```javascript
const promesa = new Promise((resolve, reject) => {
  const error = true;

  if (error) {
    reject(new Error("Algo salió mal"));
  } else {
    resolve("Se resolvió con éxito la promesa");
  }
});

promesa
  .then((mensaje) => {
    console.log(mensaje);

    return new Promise((resolve) => {
      resolve("mensaje 2");
    });
  })
  .then((mensaje) => {
    console.log(mensaje);

    return new Promise((resolve) => {
      resolve("mensaje 3");
    });
  })
  .then((mensaje) => {
    console.log(mensaje);
  })
  .catch((error) => {
    console.log("Error, repito.. Error");
  })
  .finally(() => {
    console.log("terminó todo amigos!");
  });
```

- En algunas oportunidades necesitamos saber cuando varias `promises` terminaron.
- Promise tiene un método llamado `all` que recibe una colleción de promesas y ejecuta el método `then` cuando se resuelven.
- El método `then` recibe un array con todos los valores devueltos por las promises utilizadas en `.all`
- Para saber más sobre `all` podes leer la [guía de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

```javascript
const promise1 = new Promise((onSuccess) => {
  console.log("Promise 1");
  setTimeout(onSuccess(10), 2000);
});

const promise2 = new Promise((onSuccess) => {
  console.log("Promise 2");
  setTimeout(onSuccess, 10000);
});

const promise3 = new Promise((onSuccess) => {
  console.log("Promise 3");
  setTimeout(onSuccess, 5000);
});

const promises = [promise1, promise2, promise3];

Promise.all(promises).then((values) => {
  console.log(values);
  console.log("terminaron");
});
```

-
- Si queremos saber que todas las promises se resolvieron exitosamente podemos utilizar `allSettled`.
- `allSettled` devuelve un array de objetos que tiene dos propiedades `status` y `value o reason`

```javascript
const promise1 = new Promise((onSuccess) => {
  console.log("Promise 1");
  setTimeout(onSuccess(10), 2000);
});

const promise2 = new Promise((onSuccess, onError) => {
  console.log("Promise 2");
  onError(new Error("Error que llega de la promise 2"));
});

const promise3 = new Promise((onSuccess) => {
  console.log("Promise 3");
  setTimeout(onSuccess, 5000);
});

const promises = [promise1, promise2, promise3];

Promise.allSettled(promises).then((results) => {
  console.log(results);
  console.log("All settled");
});
```

```bash
Promise 1
Promise 2
Promise 3
[
  { status: 'fulfilled', value: 10 },
  {
    status: 'rejected',
    reason: Error: Error que llega de la promise 2
        at /Users/nicolasisnardi/Projects/content/intro_to_react_native_code/contenido/promise.js:109:11
        at new Promise (<anonymous>)
        at Object.<anonymous> (/Users/nicolasisnardi/Projects/content/intro_to_react_native_code/contenido/promise.js:107:18)
        at Module._compile (node:internal/modules/cjs/loader:1562:14)
        at Object..js (node:internal/modules/cjs/loader:1699:10)
        at Module.load (node:internal/modules/cjs/loader:1313:32)
        at Function._load (node:internal/modules/cjs/loader:1123:12)
        at TracingChannel.traceSync (node:diagnostics_channel:322:14)
        at wrapModuleLoad (node:internal/modules/cjs/loader:217:24)
        at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:170:5)
  },
  { status: 'fulfilled', value: undefined }
]
All settled
```

- Para saber más sobre `allSettled` podes leer la [guía de MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled)

### Guías

- [Promise en MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [Usando promesas en MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Using_promises)
