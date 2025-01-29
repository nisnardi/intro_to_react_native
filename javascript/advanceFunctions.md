# JavaScript

## Más conceptos sobre funciones

### Arguments

- Las funciones tienen un parámetro especial llamado `arguments` que es un objeto que funciona como tu array.
- Tiene una propiedad `length` que retorna la cantidad de items que fueron pasados por parámetro cuando se ejecutó la función.
- Podemos acceder a cada item utilizando `arguments[indice]` donde índice es un número entre 0 (primer item) y la longitud - 1.
- Este valor es medio raro ya que se llama `argument` y no vemos que esté definido en ningún lado.
- El ínidice va en orden como fueron pasados los parámetros.

```javascript
function sumar() {
  console.log(arguments); // Arguments] { '0': 10, '1': 20, '2': 30, '3': 40 }
  console.log(typeof arguments); // object
  console.log(arguments.length); // 4
  console.log(arguments[0]); // 10
  console.log(arguments[1]); // 20
  console.log(arguments[2]); // 30
  console.log(arguments[3]); // 40
}

sumar(10, 20, 30, 40);
```

- Podemos utizar este valor para consultar parámetros de manera dinámica.

```javascript
function sumar() {
  let resultado = 0;
  for (let index = 0; index < arguments.length; index++) {
    resultado += arguments[index];
  }
  return resultado;
}

const resultado = sumar(10, 20, 30, 40);
console.log(resultado);
```

### Parametros por default

- Los parametros por default se inicializan en `undefined`.
- Algunas veces necesitamos establecer un parametro con valor por defecto.
- Para establecer un valor por default utilizamos la sintaxis `nombreParametro = valorPorDefault`

```javascript
function sumar(numero1 = 0, numero2 = 0) {
  return numero1 + numero2;
}
```

- Usar parametros por defecto nos pueden ayudar a evitar errores o validaciones de más.

```javascript
function mostrarItemsDeColeccion(coleccion) {
  for (let index = 0; index < coleccion.length; index++) {
    console.log(coleccion[index]);
  }
}
// Esto tira un error de type error porque colección es undefined y no tiene la propiedad length
mostrarItemsDeColeccion();
```

- Solucionamos el problema utilizando valores por defecto asignando un array vacio.

```javascript
function mostrarItemsDeColeccion(coleccion = []) {
  for (let index = 0; index < coleccion.length; index++) {
    console.log(coleccion[index]);
  }
}

// No importa si la función es llamada sin parametros ya que tiene como valor por defecto un array vacio con la propiedad length
mostrarItemsDeColeccion();
```

### Parametros rest

- Por medio de los parámetros rest podemos representar un número indefinido de parámetros como un array.
- Las funciones sólo pueden tener un parametro rest y tiene que ser el último en la definición.
- El parametro rest no puede tener valor por defecto como el resto de los parametros.

```javascript
function mostrarIntegrantesDeClase(
  profesor,
  alumnos,
  ...restoDeLosIntegrantes
) {
  console.log("Profesor: ", profesor); // Nicolas
  console.log("Alumnos", alumnos); // [ 'Juan', 'María' ]
  console.log(
    "Resto de los que hacen posible un curso:",
    restoDeLosIntegrantes
  ); // [ 'Soledad', 'Pablo' ]
}

mostrarIntegrantesDeClase("Nicolas", ["Juan", "María"], "Soledad", "Pablo");
```

```
Profesor:  Nicolas
Alumnos [ 'Juan', 'María' ]
Resto de los que hacen posible un curso: [ 'Soledad', 'Pablo' ]
```

- La principal diferencia con `arguments` es que el parametro rest es un `array` por lo cual lo podemos utilizar como tal.

### Recursividad

- Una función puede llamarse a si mismo y esto se conoce como función recursiva.

```javascript
function mostrarNumeros(numero = 0) {
  console.log(numero);
  mostrarNumeros(numero + 1);
}

mostrarNumeros();
```

- Al igual que los iteradores necesitamos alguna condición para deje de llamarse a si misma para cortar la ejecución.

```javascript
function mostrarNumeros(numero = 0) {
  console.log(numero);
  if (numero < 10) {
    mostrarNumeros(numero + 1);
  }
}

mostrarNumeros();
```

### Funciones anidadas

- Como sabemos una función puede tener otra función definida como parte de su cuerpo.
- La función dentro de la otra es privada, significa que solo puede ser accedida desde adentro de la función padre y no desde afuera.
- La función interna tiene acceso a los parámetros del padre y recurda el valor durante la ejecución de la función.

```javascript
function mostrarMensajeSecreto(mensaje) {
  function mensajeSecreto(secreto) {
    return `${mensaje} secreto: ${secreto}`;
  }

  const nuevoMensaje = mensajeSecreto("Que bueno es JavaScript!");

  console.log(nuevoMensaje);
}

mostrarMensajeSecreto("Mostar este mensaje");
```

### Funciones que retornan funciones y closure

- Sabemos que una función puede retornar o devolver un valor de cualquier tipo.
- Dado que las funciones son un tipo de dato podemos devolver una función desde otra función.

```javascript
function obtenerFuncionSumar() {
  const suma = function (numero1, numero2) {
    console.log(
      `Resultado de sumar ${numero1} + ${numero2} es ${numero1 + numero2}`
    );
  };

  return suma;
}

const mostrarSuma = obtenerFuncionSumar();

mostrarSuma(10, 20);
```

- En este ejemplo vemos como la función `obtenerFuncionSumar` retoran una función que acepta 2 parámetros.
- La función retornada suma los dos números y muestra el resultado en pantalla.
- Cuando ejecutamos la función `obtenerFuncionSumar` asignamos el valor retornado dentro de la variable `mostrarSuma`.
- Es ahí cuando `mostrarSuma` se le asigna una función (la que definimos como suma) que suma los valores y los muestra en pantalla.
- Otra forma de ejecutar esta función es simplemente ejecutando la función retornada sin asignar a una variable auxiliar.

```javascript
function obtenerFuncionSumar() {
  const suma = function (numero1, numero2) {
    console.log(
      `Resultado de sumar ${numero1} + ${numero2} es ${numero1 + numero2}`
    );
  };

  return suma;
}

obtenerFuncionSumar()(10, 20);
```

- El primer paréntesis es para ejecutar la función `obtenerFuncionSumar` y el segundo es para ejecutar la función retornada (suma) pasando los parámetros necesarios.
- Ahora que aprendimos todos estos conceptos podemos aprender que las funciones internas mantienen los valores pasados por parametros de las funciones padres.

```javascript
function obtenerFuncionSumar(numero3) {
  const suma = function (numero1, numero2) {
    console.log(
      `Resultado de sumar ${numero1} + ${numero2} + ${numero3} es ${
        numero1 + numero2 + numero3
      }`
    );
  };

  return suma;
}

const mostrarSuma = obtenerFuncionSumar(5);

mostrarSuma(10, 20);
```

- En este ejemplo vemos como la función interna puede acceder a `numero3` que es el valor pasado por parámetro a la función padre.
- La función interna mantiene el contexto al ser ejecutada "recordando" que el parámetro `numero3` tiene un valor de 5.
- De esta manera podemos utilizar ese parámetro aún si no lo pasamos a la función interna al momento de ejecutarla.
- Estos conceptos de funciones privadas + manejo de contexto se llama closure.

- Para aprender más sobre funciones podes seguir la guía de [funciones en MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Functions)

### Arrow Functions

- ES6 agregó un tipo de función que se llama Arrow functions.
- En principio podemos decir que es una forma más simple de escribir funciones.

```javascript
// función anónima

function(num1, num2) {
  return num1 + num2
}

// Arrow functions
(num1, num2) => {
  return num1 + num2;
}
```

- La primer diferencia que vamos a notar entre una función anónima y un Arrow function es que no utiliza la palbra function para definirla.
- `() => {}` esta es la forma más fácil de definir / declarar una función.
- Entre los paréntesis van los parámetros al igual que en las funciones normales.
- `=>` define que esto es una función Arror function dado la forma de flecha que tienen los símbolos igual y mayor.
- `{}` entre llaves podemos definir el cuerpo de una Arrow function

```javascript
// Arrow functions
(num1, num2) => num1 + num2;
```

- CUando la Arrow function tiene sólo una linea podemos hasta no utilizar cuerpo de función como también la palabra `return`.

```javascript
// Arrow functions
(nombre) => console.log(nombre);
```

- Si la función tiene tan solo un parámetro podemos no poner los paréntesis, por cuestiones de formato en este ejemplo se agregan solos.

```javascript
(valor) => ({ nombre: valor });
```

- Si la Arrow function retorna un objeto tenemos que poner paréntesis para evitar errores.
- Esto es lo mismo que hacer:

```javascript
(valor) => {
  return { nombre: valor };
};
```

- Las Arrow functions son muy buenas para poder utilizar dentro de iteradores como `map, forEach, filter, reduce`.

```javascript
const numeros = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

numeros.forEach((numero) => console.log(numero + 1));
```

- Esto es lo mismo que hacer:

```javascript
const numeros = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const mostrarNumeroIncrementado = (numero) => console.log(numero + 1);

numeros.forEach(mostrarNumeroIncrementado);
```

- Este tipo de funciones pueden utilizar los parámetros Rest y parámetros por default pero no soporta arguments.

```javascript
const mostrarIntegrantesDeClase = (
  profesor,
  alumnos,
  ...restoDeLosIntegrantes
) => {
  console.log("Profesor: ", profesor); // Nicolas
  console.log("Alumnos", alumnos); // [ 'Juan', 'María' ]
  console.log(
    "Resto de los que hacen posible un curso:",
    restoDeLosIntegrantes
  ); // [ 'Soledad', 'Pablo' ]
};

mostrarIntegrantesDeClase("Nicolas", ["Juan", "María"], "Soledad", "Pablo");

// Parametros por defecto
const mostrarNumeros = (numeros = []) => {
  for (let index = 0; index < numeros.length; index++) {
    console.log(numeros[index]);
  }
};

mostrarNumeros();
```

- Hay otras diferencias entre funciones originales y las arrow functions pero necesitamos entender como funciona `this` en JavaScript primero.
- Para aprender más sobre Arrow functions podes seguir la guía de [Arrow functions en MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

### Higher Order Functions

- Se llama `Higher order function` a una función que al menos cumple con alguna de estas dos condiciones;
  - Recibe una función como parámetro (callback).
  - Retorna una función.
- Este es un concepto de programación funcional y que en JavaScript lo podemos utilizar de las formas aprendidas.
- Ejemplo función que recibe una función como parámetro:

```javascript
function map(coleccion = [], callback = () => {}) {
  for (let index = 0; index < coleccion.length; index++) {
    callback(coleccion[index]);
  }
}

const alumnos = ["Juan", "Marta", "Pepe", "Agustina", "Soledad"];
const mostrarNombreDeAlumno = (alumno) => console.log(alumno);

map(alumnos, mostrarNombreDeAlumno);
```

- Ejemplo función que retorna una función:

```javascript
function mostrarLinea(caracter, cantidad) {
  const texto = caracter.repeat(cantidad);
  console.log(texto);
}

function obtenerFuncionTemplate(caracter = "*") {
  return (texto) => {
    const cantidadMaximaCaracteres = texto.length + 4;

    mostrarLinea(caracter, cantidadMaximaCaracteres);
    console.log(`${caracter} ${texto} ${caracter}`);
    mostrarLinea(caracter, cantidadMaximaCaracteres);
  };
}

obtenerFuncionTemplate("=")("Nicolas");
```

- Las funciones `map, filter, reduce, forEach` son consideradas Higher-Order Functions.

### IIFE

- IIFE se le llama al autoejecutar una función ni bien fué definida.
- El concepto es simple, declarar una función entre paréntesis y luego ejecutarla.

```javascript
//
funcion();
```

- En este ejemplo se ve bien simple pero no es real.
- Veamos un ejemplo más real:

```javascript
(function () {
  console.log("Esta funcion se ejectuto");
})();
```

- También le podemos pasar parámetros como a cualquier función normal.

```javascript
(function (mensaje) {
  console.log(mensaje);
})("Esta funcion se ejectuto");
```

- Al igual que cuando ejecutamos una función normal podemos pasar los parámetros entre los paréntesis.

#### Practica

- [Ejercicio 177](../ejercicios/consignas/js/ej177.md)
- [Ejercicio 178](../ejercicios/consignas/js/ej178.md)
- [Ejercicio 179](../ejercicios/consignas/js/ej179.md)
