# JavaScript

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

- [Ejercicio 64](../ejercicios/consignas/js/ej64.md)
- [Ejercicio 65](../ejercicios/consignas/js/ej65.md)
