# JavaScript

## Módulos

- Es común que una aplicación pueda crecer rápido al crear nuevas features o tener mucha gente trabajando en un proyecto.
- Es un buena practica mantener nuestro código corto para que sea más fácil de leer, entender y seguir el contexto.
- Si abrimos un archivo y tiene 2000 lineas de código es difícil de seguir y entender de maneara aislada.
- Dado el tamaño del código y la complejidad del código es que se recomienda utilizar el concepto de `módulos`.
- Un `módulo` no es más ni menos que un archivo donde ponemos parte del código que luego podemos utilizar desde otros módulos o archivos.
- El `módulo` debe `exportar` el codigo que va a ser utilizado en otros lados.
- Los otros archivos o módulos deben `importar` el codigo del módulo que necesitan utilizar.
- Por ejemplo podemos tener un módulo de funciones tipo utilitarios y poner en ese archivo todo el codigo relacionado.
- Para exportar algo de un módulo en JavaScript se utiliza la palabra reservada `export`.
- Para importar algo de otro módulo se utiliza la palabra reservada `import`.
- Vamos a crear un ejemplo simple para poner en práctica este nuevo concepto.
- Necesitamos 2 archivos, uno para el módulo (utils.js) y otro para llamar o utilizar el módulo(usandoutils.js)

```javascript
// En el archivo utils.js declaramos y exportamos la siguiente función:
export function acortarPalabra(palabra, cantidadDeCaracteres, simbolo = ".") {
  if (palabra.length > cantidadDeCaracteres) {
    const palabraAcortada = palabra
      .slice(0, cantidadDeCaracteres)
      .concat(simbolo.repeat(3));
    return palabraAcortada;
  }

  return palabra;
}

// En usandoutils.js importamos la función del módulo utils de la siguiente manera:
import { acortarPalabra } from "./utils.js";

const nombre = "Nicolas";
const palabraAcortada = acortarPalabra(nombre, 4);
const palabraAcortada2 = acortarPalabra("AGUANTE JAVASCRIPT!!!!", 18);

console.log(palabraAcortada);
console.log(palabraAcortada2);
```

- En este ejemplo vemos como `utils.js` utiliza la palabra `export` para exportar una función con el nombre de `acortarPalabra`.
- El archivo `usandoutils.js` importa la función utilizando la palabra `import` y luego `{ nombreDeLoQueQuieroImportar }` y también establecemos de donde queremos importar utilizando `from 'path a nuestro archivo`.
- El import nos queda como: `import { acortarPalabra } from "./utils.js";`.
- Este tipo de import se llama Named import ya que utilizamos el mismo nombre que tiene la función en el lugar donde fue declarado.
- También podemos importar variables siguiendo la misma estructura tanto en el módulo como en el archivo que utiliza al mismo.

```javascript
// utils.js
export const SIMBOLO = ".";

export function acortarPalabra(
  palabra,
  cantidadDeCaracteres,
  simbolo = SIMBOLO
) {
  if (palabra.length > cantidadDeCaracteres) {
    const palabraAcortada = palabra
      .slice(0, cantidadDeCaracteres)
      .concat(simbolo.repeat(3));
    return palabraAcortada;
  }

  return palabra;
}

// usandoutils.js
import { acortarPalabra, SIMBOLO } from "./utils.js";

const nombre = "Nicolas";
const palabraAcortada = acortarPalabra(nombre, 4);
const palabraAcortada2 = acortarPalabra("AGUANTE JAVASCRIPT!!!!", 18, "<3");

console.log(palabraAcortada);
console.log(palabraAcortada2);

console.log(`El símbolo utilizado por default es: ${SIMBOLO}`);
```

- Con `export const SIMBOLO = ".";` declaramos la variable, le asignamos un valor y con `export` lo exportamos del módulo.
- Luego `import { acortarPalabra, SIMBOLO } from "./utils.js";` establece que queremos importar la función y la variable `SIMBOLO`.
- Vemos que siempre utilizamos el mísmo nombre con el que fueron declarados los exports.
- En caso de necesitarlo o querer también podemos renombrar los valores donde los utilizamos.

```javascript
// utils.js
export const SIMBOLO = ".";

export function acortarPalabra(
  palabra,
  cantidadDeCaracteres,
  simbolo = SIMBOLO
) {
  if (palabra.length > cantidadDeCaracteres) {
    const palabraAcortada = palabra
      .slice(0, cantidadDeCaracteres)
      .concat(simbolo.repeat(3));
    return palabraAcortada;
  }

  return palabra;
}

// usandoutils.js
import { acortarPalabra, SIMBOLO as elSimbolo } from "./utils.js";

const nombre = "Nicolas";
const palabraAcortada = acortarPalabra(nombre, 4);
const palabraAcortada2 = acortarPalabra("AGUANTE JAVASCRIPT!!!!", 18, "<3");

console.log(palabraAcortada);
console.log(palabraAcortada2);

console.log(`El símbolo utilizado por default es: ${elSimbolo}`);
```

- Utilizamos la palabra reservada `as` para establecer que `SIMBOLO` ahora es `elSimbolo`.
- Esto nos ayuda por ejemplo a no tener problemas con los nombres de las variables donde utilizamos un módulo pero conservamos el nombre original del import.
- Otra opción es importar todo junto utilizando `*` y un nombre para el import de la siguiente manera:

```javascript
import * as Utils from "./utils.js";

const { acortarPalabra, SIMBOLO } = Utils;
const nombre = "Nicolas";
const palabraAcortada = acortarPalabra(nombre, 4);
const palabraAcortada2 = acortarPalabra("AGUANTE JAVASCRIPT!!!!", 18, "<3");

console.log(palabraAcortada);
console.log(palabraAcortada2);

console.log(`El símbolo utilizado por default es: ${SIMBOLO}`);
```

- Por medio de `*` establecemos que queremos importar todo lo que exporta el módulo y con `as Utils` le definimos un nombre para utilizarlo.
- En este ejemplo usamos destructuring para obtener la función y variable que queremos utilizar pero también podríamos usar `Utils.acortarPalabra y Utils.SIMBOLO` ya que lo importado es un `objeto`.
- Los módulos también pueden exportar valores por default.
- Esto significa que establecemos sólo un valor por archivo donde establecemos todo lo que queremos exportar:

```javascript
const SIMBOLO = ".";

function acortarPalabra(palabra, cantidadDeCaracteres, simbolo = SIMBOLO) {
  if (palabra.length > cantidadDeCaracteres) {
    const palabraAcortada = palabra
      .slice(0, cantidadDeCaracteres)
      .concat(simbolo.repeat(3));
    return palabraAcortada;
  }

  return palabra;
}

export default {
  acortarPalabra,
  simbolo: SIMBOLO,
};
```

- En este caso exportamos la función `acortarPalabra` y definimos un nombre en minúscula para `SIMBOLO`.
- Dado que utilizamos default export sólo podemos utilizar un export default por módulos.
- Al utilizar default export no podemos utilizar named imports ya que sólo exporta un objeto y esta en nosotros definir el nuevo nombre de import.

```javascript
import Utils from "./utils.js";

const { acortarPalabra, simbolo } = Utils;
const nombre = "Nicolas";
const palabraAcortada = acortarPalabra(nombre, 4);
const palabraAcortada2 = acortarPalabra("AGUANTE JAVASCRIPT!!!!", 18, "<3");

console.log(palabraAcortada);
console.log(palabraAcortada2);

console.log(`El símbolo utilizado por default es: ${simbolo}`);
```

- En este caso `import Utils from "./utils.js";` importa lo exportado por default en el módulo que es un objeto que tiene 2 propiedades, `acortarPalabra y simbolo`.
- Puedes aprender más sobre módulos en la [guía de módulos de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Modules)

#### Practica

- [Ejercicio 205](../ejercicios/consignas/js/ej205.md)
