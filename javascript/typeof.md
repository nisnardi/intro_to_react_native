### typeof

- Por medio del operador **typeof** podemos saber de que tipo es una variable

**Ejemplo:**

```js
let nombre = "Marta";
let edad = 30;
let casado = false;
let indefinido = undefined;
let nulo = null;

console.log(typeof nombre); // string
console.log(typeof edad); // number
console.log(typeof casado); // boolean
console.log(typeof indefinido); // undefined
console.log(typeof nulo); // object
```

- En este ejemplo vemos que cada tipo de dato retorna un tipo distinto
- En el caso de **null** retorna object en lugar de null como uno espera
- Object es otro tipo de dato de ECMAScript y lo vamos a ver más adelante

#### Prácticas

[Ejercicio 25](../ejercicios/consignas/js/ej25.md)
[Ejercicio 26](../ejercicios/consignas/js/ej26.md)
