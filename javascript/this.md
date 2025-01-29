# JavaScript

## This

- `this` en JavaScript es una palabra reservada que guarda una referencia dinámica a quién llamó una función.
- Esto significa que cambia según como se lo utiliza / llama.
- Provee acceso al contexto donde se está ejecutando el código.

### Contexto global

- `this` utilizado en el scope global hace referencia al objeto `global` en Node.js y al objeto `Window` en el browser.

```javascript
console.log(this);
```

### Dentro de un metodo de un Objeto literal

- `this` dentro de un objeto literal utilizando una función hace referencia al objeto

```javascript
const persona = {
  nombre: "Nicolas",
  saludar: function () {
    console.log(this);
    console.log(this.nombre);
  },
};

persona.saludar();
```

### Dentro de una función

- `this` en una función cambia según como fué ejecutada la funciión.
- Al llamar una función el scope global, `this` hace referencia a `global` en Node.js o `Window` en browsers.

```javascript
function saludar() {
  console.log(this); // global
}

saludar();
```

- JavaScript tiene un modo estricto que permite ejecutar JS de una manera menos confusa.
- Para usar el modo estricto se debe agregar `"use strict"` al principio del archivo.
- Este modo elimina algunos de los problemas silenciosos que puede tener JavaScript.
- Al utilizar `"use strict"` `this` en funciones cambia a ser `undefined`.

```javascript
"use strict";

function saludar() {
  console.log(this); // undefined
}

saludar();
```

- Existen 3 funciones (`call, apply & bind`) que permiten manejar `this` en una función.

#### Call

- `call` acepta como primer parámetro cual es el contexto de `this` dentro de la función.
- El resto de los parámetros son pasados como parámetros individuales a la función.

```javascript
function calcularPromedio(nota1, nota2) {
  const promedio = (nota1 + nota2) / 2;

  console.log(`El promedio de ${this.nombre} es ${promedio}`);
}

const alumno = {
  nombre: "Martín",
};

calcularPromedio.call(alumno, 10, 6);
```

- En este ejemplo vemos como `this` pasa a hacer referencia al objeto `alumno`.
- Los otros dos parámetros de `call` pasan a ser `nota1` y `nota2`.

#### Apply

- `bind` funciona de una manera similar a `call` pero cambia la forma de pasar parámetros.
- El primer parámetro sigue siendo el contexto que toma `this`.
- el segundo parámetro es una colección que pasan como parametros.

```javascript
function calcularPromedio(nota1, nota2) {
  const promedio = (nota1 + nota2) / 2;

  console.log(`El promedio de ${this.nombre} es ${promedio}`);
}

const alumno = {
  nombre: "Martín",
};

const notas = [10, 6];

calcularPromedio.apply(alumno, notas);
```

- En este ejemplo creamos una colección (Array) de notas.
- Pasamos como primer parámetro de `bind` el objeto alumno para que `this` haga referencia a ese objeto.
- Como segundo parámetro pasamos la colección `notas` y cada valor de la colección se transforma en un parámetro de la función.
- El primer item de la colección notas pasa a ser nota1 y el segundo pasa a ser nota2.
- Podemos hacer una versión más dinámica.

```javascript
function calcularPromedio(nota1, ...notas) {
  const sumaDeNotas = (acumulador, nota) => {
    return acumulador + nota;
  };

  const promedio = (nota1 + notas.reduce(sumaDeNotas, 0)) / arguments.length;

  console.log(`El promedio de ${this.nombre} es ${promedio}`);
}

const alumno = {
  nombre: "Martín",
};

const notas = [10, 6, 8, 7, 9];

calcularPromedio.apply(alumno, notas);
```

- En este ejemplo agregamos más notas del alumno.
- La función `calcularPromedio` recibe una nota como primer parámetro y luego utilizamos `rest` para obtener una colección con el resto de las notas.
- Para calcular el promedio sumamos todas las notas de la colección notas usando reduce y luego le sumamos la primer nota que vino como primer parámetro.
- Utilizando `arguments.length` para saber la cantidad de notas pasadas como parámetro.
- `this` sigue siendo una referencia al objeto alumno.

#### Bind

- `bind` funciona de una manera un poco diferente.
- Esta función devuelve una función donde `this` está bindeado o relacionado con el contexto pasado como parámetro.
- Dado que retorna una función nueva, tenemos que ejecutarla para que funcione.

```javascript
function saludar() {
  console.log(this);
}

const alumno = {
  nombre: "Martín",
};

// bind retorna una nueva función donde alumno es el contexto de this
const nuevaFuncion = saludar.bind(alumno);

// ejecutamos la función para ver quién es this
nuevaFuncion(); // { nombre: 'Martín' }
```

### Arrow Functions

- Arrow functions no son un remplazo de las `functions` de JavaScript sino que son útiles en algunos casos.
- Las arrow functions no tienen su propio `this` como las `functions`.
- Toman el contexto de `this` heredandolo de su contexto.

```javascript
const alumno = {
  nombre: "Martín",
  saludar: () => {
    console.log(this); // undefined
  },
};

alumno.saludar();
```

- Al ejecutar este código vemos que `this` se transformó en el objeto global o windwow.
- Esto cambia si una arrow function es utilizada dentro de otra función.

```javascript
const alumno = {
  nombre: "Martín",
  saludar: function () {
    const otraFuncion = () => {
      console.log(this);
    };

    otraFuncion(); // { nombre: 'Martín', saludar: [Function: saludar] }
  },
};

alumno.saludar();
```

- Dado que la arrow function está dentro de otra `function` toma el contexto de `this` de la función.
- La `function` tiene el `this` como la instancia del objeto alumno por lo cual es lo que toma la arrow function como tal.
- Las arrow functions no funcionan con `call, apply o bind`.

### Iteradores

- Utilizar arrow functions para funciones de iteradores como `map, reduce, filter, forEach` es una buena idea ya que no cambia el contexto de this.
- Vale recordad que las `functions` tienen un `this` dinámico.

```javascript
const animales = ["leon", "delfin", "mono"];

const global = this;

animales.forEach((animal) => {
  console.log(this, this === global); // {}, true
});
```

- El `this` dentro del `forEach` es el mismo objeto que el del espacio global ya que está siendo ejecutado en un ambiente global.

```javascript
const animales = ["leon", "delfin", "mono"];

const global = this;

animales.forEach((animal) => {
  console.log(this === global); // false
});
```

- En este caso la comparación es falsa ya que la función tiene su propio `this`.

### Consejo

- A mi me resulta últil muchas veces pensar que `this` en funciones se refiere a quién está delante de la función al ser llamado.

```javascript
const persona = {
  nombre: "Nicolas",
  saludar: function () {
    console.log(this.nombre);
  },
};

persona.saludar();
```

- En este ejemplo `persona.` está a la izquierda de la ejecución de la función.
- El objeto persona pasa a ser el contexto de `this`.

```javascript
function saludar() {
  console.log(this);
}

saludar();
```

- En este caso a la izquierda de la función no hay ninguna referencia.
- En este caso elijo pensar como si fuera global o window ya que no hay otro contexto.

```javascript
function saludar() {
  console.log(this);
}

window.saludar();
global.saludar();
```
