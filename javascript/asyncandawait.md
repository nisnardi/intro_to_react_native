# JavaScript

## Async & Await

- `async await` se agregó en el ES8 (2017) y nos permite escribir código JavaScript asyncrónico como si fuera sincrónico.
- Una función puede ser declarada como `async` y dentro de ella se utiliza `await` para esperar que una promesa se resuelva.
- Una función declarada como `async` siempre devuelve una promise.
- Aún retornando un valor va a estar envuelto dentro de una promise.

```javascript
function obtenerDatos(numero) {
  return new Promise((onSuccess) => {
    const onSuccessHandler = () => {
      let datos = [];

      switch (numero) {
        case 2:
          datos = ["Marta", "elefante", "Chau"];
          break;
        case 3:
          datos = ["Javier", "mono", "Hello"];
          break;
        default:
          datos = ["Nico", "perro", "Hola"];
          break;
      }

      onSuccess(datos);
    };

    setTimeout(onSuccessHandler, 1000);
  });
}

async function mostrarDatosEnPantalla() {
  const datos = await obtenerDatos(1);
  const datos1 = await obtenerDatos(2);
  const datos2 = await obtenerDatos(3);

  return [datos, datos1, datos2];
}

// Esta función retorna una promesa.
mostrarDatosEnPantalla().then((datos) => console.log(datos));
```

- En este ejemplo tenemos 2 funciones.
- La función `obtenerDatos` simula un `fetch` donde va a buscar datos a algún lado con un timer y retorna una promise.
- La segunda función `mostrarDatosEnPantalla` es una función `async` que utiliza `await` dentro de ella.
- Ejecutamos la función `mostrarDatosEnPantalla` y sabemos que retorna una promise.
- Dentro de `mostrarDatosEnPantalla` llamamos 3 veces a `obtenerDatos` y usando `await` podemos esperar a cada una de esas promesas hasta que se resuelva.
- Para manejar errores podemos utilizar `try and catch`

```javascript
function obtenerDatos(numero) {
  return new Promise((onSuccess, onError) => {
    const onSuccessHandler = () => {
      let datos = [];

      switch (numero) {
        case 2:
          datos = ["Marta", "elefante", "Chau"];
          break;
        case 3:
          datos = ["Javier", "mono", "Hello"];
          break;
        default:
          datos = ["Nico", "perro", "Hola"];
          break;
      }

      if (numero === 4) {
        onError(new Error("Error en obtener datos 4"));
      } else {
        onSuccess(datos);
      }
    };

    setTimeout(onSuccessHandler, 1000);
  });
}

async function mostrarDatosEnPantalla() {
  try {
    const datos = await obtenerDatos(1);
    const datos1 = await obtenerDatos(2);
    const datos2 = await obtenerDatos(3);
    const datos3 = await obtenerDatos(4);

    return [datos, datos1, datos2, datos3];
  } catch (error) {
    console.log(error);
  }
}

// Esta función retorna una promesa.
mostrarDatosEnPantalla().then((datos) => console.log(datos));
```

- Vemos en ests ejemplos como podemos utilizar `async await` para manejar promises de una mejor forma.
- Utilizamos `try and catch` para tratar de ejecutar nuestro código y manejar cualquier error que pueda ocurrir.
- Puedes aprender más sobre `async & await` en la [guia de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/async_function)
