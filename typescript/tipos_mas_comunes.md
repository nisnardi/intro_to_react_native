# TypeScript

## Tipos Más Comunes

### string, number & boolean

- TypeScript tiene tipos base similares a JavaScript pero con mínimas diferencias.
- `number` acepta cualquier tipo de number, no hay diferencia entre `integer or float`.
- `string` acepta cualquier tipo de `string` de JavaScript "", '', ``.
- `boolean` acepta `true o false` pero no truthy o falsy values.
- Para declarar una variable lo seguimos haciendo de la misma forma que en JavaScript `var, let, const` y el nombre de la variable.
- Con TypeScript podemos agregar el tipo de dato que esperamos tenga esa variable agregando `:tipo_de_dato` luego de la declaración.

```typescript
let nombre: string = "Nicolas";
let edad: number = 45;
let leGustaElFutbol: boolean = true;
let promedio: numer = 9.5;
```

- Utilizando `:tipo_de_dato` podemos establecer que tipo de dato puede ser asignado a cada una de las variables.
- Esto se llama `type annotation`.
- TypeScript es capaz de inferir los tipos de datos asignados a una variable sin tener que especificarlos.

```typescript
let nombre = "Nicolas"; // TypeScript define en este momento que nombre:string sin que nosotros lo tengamos que especificar.
nombre = 32; // TypeScript va a tirar un error.
```

- En este caso obtenemos un error de TS `Type 'number' is not assignable to type 'string'` ya que puede identificar que la variable `nombre` fue inicializada con un valor de `string` entonces no permite que asignemos otro tipo de dato como `number`.
- La regla que podemos utilizar es no especificar el tipo de dato si al declarar una variable también le asignamos el valor pero si especificar el tipo si sólo declaramos la variable para luego utilizarla.

### Arrays

- Para los `arrays` TypeScript permite que la definición sea estricta o no según nuestra definición.
- Como sabemos JS permite tener en un array valores diferentes o todos del mismo tipo, depende de como lo queremos utilizar.
- Si la colección que vamos a utilizar tiene todos items del mismo tipo de dato podemos definirlo como `tipo_de_dato[]`.
- Por ejemplo si tenemos una colección de solo `strings` podemos definirlo como `string[]`.

```typescript
let animales: string[]; // Podría asignar la colección si quiero, esto es solo para ejemplo
animales = ["Perro", "Gato", "Mono"];
animales.push(42); // tira un error ya que se espera sólo tener strings
```

- Tratar de asignar un número a una colección que solo acepta strings hace que TS nos muestre el siguiente error `Argument of type 'number' is not assignable to parameter of type 'string'`.
- Dado que definimos los tipos de datos de la colección `animales`, TS puede ayudarnos mostrando las propiedades de `string` a utilizar un item.

```typescript
for (animal of animales) {
  console.log(animal.toUpperCase()); // Al poner . después de animal, VS code debería mostrar los métodos y propiedades de los string.
}
```

### Any

- Hay un tipo de dato que nos permite asignar cualquier tipo de valor llamado `any`.
- Si bien puede ser útil en algún momento podemos decir que `any` va en contra de la razón por la que utilizamos TypeScript.
- TypeScript hasta tiene una opción en el compilador que no permite el uso de `any` para que sea más estricto.
- Muchas veces se da que todavía no sabemos como va a ser el tipo de dato, no queremos ver u obtener el error de TS y podemos utilizar `any`.
- También se puede dar el caso donde realmente aceptemos que sea cualquier valor.
- También se puede configurar `noImplicitAny` para que TypeScript no use `any` cuando no puede inferir el tipo de dato.

```typescript
let numero: any = 10;
numero = "10";
```

- Este código es válido en TS y no tira ningún error.
- Me gusta ver `any` como que rompimos TypeScript.
- Esto también funciona para un `array` definiendo el tipo como sería el de JavaScript.

```typescript
const coleccion: any = [10, "Nico", () => {}, true];
```

### Functions

- TypeScript permite establecer los tipos de datos de los parámetros de una función como el valor que retorna.
- Podemos utilizar type anonotations después de cada parámetro para establecer el tipo de dato luego del nombre del parámetro.

```typescript
function sumar(number1: number, number2: number) {
  return number1 + number2;
}

sumar(2, 4);
```

- TypeScript valida siempre la cantidad de parámetros pasado a una función.
- También podemos establecer que tipo de valor retorna una función especificandolo con una type annotation.
- Luego de los paréntesis agregamos `():tipo_retornado`.
- TypeScript hace un buen trabajo al inferir que tipo retorna una función aún si no lo especificamos.

```typescript
function sumar(number1: number, number2: number): number {
  return number1 + number2;
}

sumar(2, 4);
```

- Si una función retorna una promesa podemos utilizar el tipo `Promise` y establecer que tipo de valor se resuelve de misma utilizando `<tipo_de_valor>`.

```typescript
// Recordemos que async siempre retorna una promesa pero con el valor retornado por la función.
async function fetch(path: string): Promise<string> {
  return JSON.stringify("{}");
}
```

- TypeScript es muy bueno en inferir los tipos de datos de parámetros y retornados en una función anónima.

```typescript
// (parameter) animal: string
const animales = ["Perro", "Gato", "Mono", "Delfin"];

animales.forEach(function (animal) {
  return console.log(animal.length);
});
```

- Dado que TypeScript puede inferir que animales es una colección `string[]`, donde todos los valores son `string`, puede inferir que la función anónima recibe un valor `string` al iterarlo.
- Esto también funciona con las arrow functions.

```typescript
// (parameter) animal: string
const animales = ["Perro", "Gato", "Mono", "Delfin"];

animales.forEach((animal) => {
  return console.log(animal.length);
});
```

- Esta forma de detectar el tipo de dato entre la colección, la función y donde está siendo ejecutada se llama `tipado por contexto o contextual typing`.

### Enums

- `enum` es un tipo de dato que solo funciona en TypeScript que nos permiten tener la sensación de utilizar constantes.
- TypeScript nos permite asignar una palabra como valor e internamente utiliza un número empezando por 0.

```typescript
enum TipoDeJugador {
  ARQUERO,
  DEFENSOR,
  MEDIOCAMPISTA,
  ENGANCHE,
  DELANTERO,
}

const jugador: {
  nombre: string;
  apellido: string;
  tipoDeJugador: TipoDeJugador;
} = {
  nombre: "Juan Roman",
  apellido: "Riquelme",
  tipoDeJugador: "ENGANCHE", // Tira error
};
```

- En este ejemplo definimos un `enum` o constante que tiene las posiciones en las que puede jugar un jugador de fútbol.
- Al definir el objeto jugador establecemos que la propiedad `tipoDeJugador` es del tipo `TipoDeJugador`.
- TS muestra un error al intentar asignar un `string` cuando espera un tipo de dato `TipoDeJugador`.
- Es confuso porque el valor parece ser el mismo pero para TS no lo es.

```typescript
enum TipoDeJugador {
  ARQUERO,
  DEFENSOR,
  MEDIOCAMPISTA,
  ENGANCHE,
  DELANTERO,
}

const jugador: {
  nombre: string;
  apellido: string;
  tipoDeJugador: TipoDeJugador;
} = {
  nombre: "Juan Roman",
  apellido: "Riquelme",
  tipoDeJugador: TipoDeJugador.ENGANCHE, // Problema solucionado ya que la asignación es igual a lo definido.
};
```

- El error de TS se va cuando utilizamos el tipo de dato esperado.
- `enum` puede ser útil a la hora de validar algun valor.

```typescript
enum TipoDeJugador {
  ARQUERO,
  DEFENSOR,
  MEDIOCAMPISTA,
  ENGANCHE,
  DELANTERO,
}

const jugador: {
  nombre: string;
  apellido: string;
  tipoDeJugador: TipoDeJugador;
} = {
  nombre: "Juan Roman",
  apellido: "Riquelme",
  tipoDeJugador: TipoDeJugador.ENGANCHE,
};

if (jugador.tipoDeJugador === TipoDeJugador.ENGANCHE) {
  console.log("Que lindo ver jugar un equipo con Enganche!");
}
```

- Si utilizaramos `strings` para la posición entonces tenemos que tener mucho cuidado de acordarnos como se llama cada opción para que esto funcione.
- Enums es un tipo de dato medio discutido dentro de la comunidad de JS pero igual lo podemos utilizar si lo necesitamos.
- TS genera todo este código (IIFE) para crear un enum:

```javascript
var TipoDeJugador;
(function (TipoDeJugador) {
  TipoDeJugador[(TipoDeJugador["ARQUERO"] = 0)] = "ARQUERO";
  TipoDeJugador[(TipoDeJugador["DEFENSOR"] = 1)] = "DEFENSOR";
  TipoDeJugador[(TipoDeJugador["MEDIOCAMPISTA"] = 2)] = "MEDIOCAMPISTA";
  TipoDeJugador[(TipoDeJugador["ENGANCHE"] = 3)] = "ENGANCHE";
  TipoDeJugador[(TipoDeJugador["DELANTERO"] = 4)] = "DELANTERO";
})(TipoDeJugador || (TipoDeJugador = {}));
```

- En la definición de `enum` dijimos que internamente utiliza 0 para el primer valor pero se puede cambir de ser necesario.

```typescript
enum TipoDeJugador {
  ARQUERO = 5,
  DEFENSOR,
  MEDIOCAMPISTA,
  ENGANCHE,
  DELANTERO,
}
```

- Al asignar 5 establecemos que el número inicial tiene que ser 5.
- En JavaScript lo utiliza de esta forma:

```javascript
var TipoDeJugador;
(function (TipoDeJugador) {
  TipoDeJugador[(TipoDeJugador["ARQUERO"] = 5)] = "ARQUERO";
  TipoDeJugador[(TipoDeJugador["DEFENSOR"] = 6)] = "DEFENSOR";
  TipoDeJugador[(TipoDeJugador["MEDIOCAMPISTA"] = 7)] = "MEDIOCAMPISTA";
  TipoDeJugador[(TipoDeJugador["ENGANCHE"] = 8)] = "ENGANCHE";
  TipoDeJugador[(TipoDeJugador["DELANTERO"] = 9)] = "DELANTERO";
})(TipoDeJugador || (TipoDeJugador = {}));
```

- También se puede dar que necesitamos establecer el valor del `enum` con un string.
- Por ejemplo si traemos datos de la Base de datos o del servidor y el `tipoDeJugador` se utiliza en minúscula.

```typescript
enum TipoDeJugador {
  ARQUERO = "arquero",
  DEFENSOR = "defensor",
  MEDIOCAMPISTA = "mediocampista",
  ENGANCHE = "enganche",
  DELANTERO = "delantero",
}
```

### null & undefined

- Al igual que en JavaScript se puede utilizar `null o undefined`.
- Se puede asignar un valor null o undefined a cualquier otro tipo.
- Hay una forma de configurar el compilador para que sea más estricto al chequear valores `null`.
- TS tiene una forma estricta para compilar que no permite el uso de null o undefined en otros tipos de datos.
- Por una cuestión de flexibilidad en algunos casos no se configura el modo estricto pero si queremos realmente tener el beneficio de TypeScript es mejor hacerlo o al menos configurar las propiedades que más nos ayude.
- También se puede ir adoptando de a poco.

```typescript
let numero: number = null; // Modo estricto: error TS2322: Type 'null' is not assignable to type 'number'.
let saludo: string = undefined; // Modo estricto: error TS2322: Type 'undefined' is not assignable to type 'string'.
```
