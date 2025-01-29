# JavaScript

## Scope

> Según Wikipedia: El ámbito (`scope`) es el contexto que pertenece a un nombre dentro de un programa. El ámbito determina en qué partes del programa una entidad puede ser usada.

- [Scope / Ámbito (programación)](<https://es.wikipedia.org/wiki/%C3%81mbito_(programaci%C3%B3n)>)

- En el contexto de JavaScript podemos decir que `scope` va a ser el alcance desde donde podemos acceder a un nombre, ya sea variable o función pero más que nada orientado a variables.

### 1. Global Scope

- Una variable tiene alcance `global` cuando es declarada fuera de cualquier función, bloque o módulo.
- Puede ser accedida o modificada desde cualquier lado.

```javascript
var nombre = "Nicolas";

console.log(nombre); // Tenemos acceso ya que es una variable global

function mostrarDatos() {
  console.log(nombre); // Al ser nombre una variable global la podemos acceder desde una función
}

mostrarDatos();
```

- Esto funciona tanto para `var, let, const`

```javascript
var nombre = "Nicolas";
const apellido = "Isnardi";
let edad = 45;

// Tenemos acceso ya que es una variable global
console.log(nombre);

function mostrarDatos() {
  console.log(nombre); // Al ser nombre una variable global la podemos acceder desde una función

  // let & const también tienen alcance global si son defnidas como tal
  console.log(apellido);
  console.log(edad);
}

mostrarDatos();
```

### 2. Function Scope

- En JavaScript al declarar una variable dentro de una función, sólo podemos accederla desde esa función.
- La variable no puede ser accedida desde afuera de la función y tira un error.

```javascript
function funcionConVariable() {
  var nombre = "Nicolas";

  // Podemos acceder a la variable nombre ya que la estamos usando dentro de la función
  console.log(`Nombre: ${nombre} desde dentro de la función`);
}

funcionConVariable();

console.log(`Nombre: ${nombre} desde afuera de la función`); // No podemos acceder desde afuera de la función donde fue declarada la variable
```

- Esto funciona igual para `var, let & const`

```javascript
function funcionConVariable() {
  var nombre = "Nicolas";
  const apellido = "Isnardi";
  let edad = 45;

  // Podemos acceder a la variable nombre ya que la estamos usando dentro de la función
  console.log(`Nombre: ${nombre} desde dentro de la función`);
  console.log(`Apellido: ${apellido} desde dentro de la función`);
  console.log(`Edad: ${edad} desde dentro de la función`);
}

funcionConVariable();

console.log(`Nombre: ${nombre} desde afuera de la función`); // No podemos acceder desde afuera de la función
console.log(`Apellido: ${apellido} desde afuera de la función`); // No podemos acceder desde afuera de la función
console.log(`Edad: ${edad} desde afuera de la función`); // No podemos acceder desde afuera de la función
```

### 3. Block Scope

- Antes de ES6 no existía el alcance a nivel bloque como puede ser un if statement, iterador o simplemente entre { }.
- `let & const` tienen alcance de bloque.

```javascript
{
  var nombre = "Nicolas";
  const apellido = "Isnardi";
  let edad = 45;
}

console.log(nombre); // Se puede acceder
console.log(apellido); // No se puede acceder
console.log(edad); // No se puede acceder
```

- Lo mismo pasa si utilizamos un if statement.

```javascript
if (true) {
  var nombre = "Nicolas";
  const apellido = "Isnardi";
  let edad = 45;
}

console.log(nombre); // Se puede acceder
console.log(apellido); // No se puede acceder
console.log(edad); // No se puede acceder
```

- En iteradores como el for podemos tener un problema ya que la variable termina siendo global si utilizamos var y no let.
- const no la podemos utilizar ya que no se puede cambiar el valor una vez asignado.

```javascript
for (var index = 0; index < 10; index++) {
  console.log(`index dentro del for: ${index}`);
}

console.log(`index fuera del for: ${index}`);

for (let i = 0; i < 10; i++) {
  console.log(`i dentro del for: ${i}`);
}

console.log(`i fuera del for: ${i}`);
```

### 4. Module

- JavaScript tiene modulos que nos permiten escribir código y re usarlo en diferentes lugares.
- Con Node podemos usar nmp para instalar modulos externos y en web podemos usar scrpt como modulo.
- Los modulos tienen su propio scope donde las variables definidas en un modulo pueden ser usadas dentro del mismo siguiendo los principios de scope de JavaScript pero no pueden ser accedidos por fuera del modulo a no ser que sean exportadas.
- Como programadores podemos definir que es privado para el modulo y que es accesible desde afuera.
- Para poder usar un modulo necesitamos crear al menos 2 archivos, uno para el modulo y el otro para utilizarlo.

```javascript
// Archivo: modulo.js
export const nombre = "Nicolas";
const apellido = "Isnardi";

// Archivo: index.js
import { nombre } from "./module.js";

console.log(nombre);
console.log(apellido);
```

- En este ejemplo vemos como nombre es una variable definida en el modulo pero que exportamos usando la palabra `export`
- El modulo no exporta la variable `apellido` por lo cual es privada y se puede utilizar sólo dentro del modulo.
- `{ nombre }` en el archivo que utiliza el modulo establece que queremos importar la variable `nombre` del archivo `modulo`
- Los modulos pueden exportar variables con un nombre especifico como es este caso o usar la palabra reservada `default` y le asignamos el nombre que queremos al importarla. Solo se puede usar un `default` export por archivo.

### Lexical Scope

- JavaScript utiliza lo que se llama `lexical scope` que quiere decir que el alcance de las variables está determiando por su posición en el código.
- Las funciones pueden acceder a su propio alcance como también al contexto de las funciones en las que están dentro.

```javascript
function funcionPadre(valor1) {
  function funcionHijo(valor2) {
    console.log(`Valor 1 ${valor1} desde dentro de la función hijo`);
    console.log(`Valor 2 ${valor2} desde dentro de la función hijo`);
  }

  funcionHijo(2); // Puedo llamar la función hijo desde dentro de la función padre

  console.log(`Valor 1 ${valor1} desde dentro de la función padre`);
  console.log(`Valor 2 ${valor2} desde dentro de la función padre`); // Tira error
}

// console.log(`Valor 1 ${valor1} desde fuera de la función padre`); // Tira error
// console.log(`Valor 2 ${valor2} desde fuera de la función padre`); // Tira error

funcionPadre(1);
// funcionHijo(3); // Tira error
```

- En este ejemplo podemos ver que dentro de la función hijo podemos acceder a las variables que fueron definidas o pasadas como parámetro en la función padre.
- La función padre sólo tiene acceso a las variables que fueron definidas ahí dentro como son `valor1` o llamar a la `funcionHijo` pero no puede acceder a `valor2` ya que está encerrada `(Clousure)` dentro de otra función.
- Desde fuera de la `funcionPadre` no podemos acceder ni a los valores `valor1` como `valor2` ni tampoco llamar al a `funcionHijo`.

### Scope Chain

- JavaScript busca las variables dentro del alcance local y de no encontrarlo busca en un ambito superior.
- En el siguiente ejemplo primero se busca en la función interior, luego en la superior y finalmente en el ambito global.

```javascript
const variableGlobal = "Soy una variable global!";

function funcionExterior() {
  const variableEnFuncionExterior = "Estoy en la función exterior!";

  function funcionInterior() {
    const variableEnFuncionInterior = "Estoy en la función interior!";

    console.log(variableEnFuncionInterior); // Se puede encontrar en la función Interior
    console.log(variableEnFuncionExterior); // Se puede encontrar en la función Exterior
    console.log(variableGlobal); // Se puede encontrar en el scope global
  }

  funcionInterior();
}

funcionExterior();
```

- Algo que ayuda con `scope` es entender que la visibilidad de las variables es desde adentro para afuera y no de afuera hacia adentro.

#### Practica

- [Ejercicio 166](../ejercicios/consignas/js/ej166.md)
- [Ejercicio 167](../ejercicios/consignas/js/ej167.md)
- [Ejercicio 168](../ejercicios/consignas/js/ej168.md)
- [Ejercicio 169](../ejercicios/consignas/js/ej169.md)
- [Ejercicio 170](../ejercicios/consignas/js/ej170.md)
- [Ejercicio 171](../ejercicios/consignas/js/ej171.md)
- [Ejercicio 172](../ejercicios/consignas/js/ej172.md)
