# JavaScript

## Numbers

- Otro de los tipos de datos que tenemos en ECMAScript es **numbers** y nos permite utilizar números
- Este tipo de datos no va entre comillas ni dobles ni simples
- Para saber más sobre este tipo de datos pueden entrar en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Number)

**Ejemplo:**

```js
let edad = 38;
let volumen = 50;

console.log(edad);
console.log(volumen);
```

#### Prácticas

[Ejercicio 20](../ejercicios/consignas/js/ej20.md)
[Ejercicio 21](../ejercicios/consignas/js/ej21.md)

- Un error común que podemos hacer cuando arrancamos a programar o aprender ECMAScript es cofundirnos al encontrar algún código similar al siguiente ejemplo

**Ejemplo:**

```js
let edad = 38;
let volumen = "50";
```

> En este caso tenemos dos variables que contienen un número.
> A la variable **edad** le asignamos un tipo de dato **number** y a la variable **volumen** le estamos asignando un tipo de dato **string** por más que el contenido sea un número.
> Es importante entender que son distintos tipos de datos por lo cual vamos a poder utilizarlos de diferente forma, por ejemplo a los **numbers** los vamos a poder utilizar para operaciones matemáticas y a los **string** no.

- Más adelante vamos a utilizar operadores aritméticos para hacer operaciones matemáticas con este tipo de datos (suma, resta, multiplicación)
