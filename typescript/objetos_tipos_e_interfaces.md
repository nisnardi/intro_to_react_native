# TypeScript

## Objetos, Alias e Interfaces

### Object

```typescript
let nombre: string; // solo definimos la variable.
nombre = "Nicolas";

let edad = 45; // No le decimos nada a TS y lo dejamos que infiera el tipo de dato desde el valor asignado.
```

- `object` es otro tipo base de TypeScript que permite definir el tipo de objeto que acepta una variable.
- TypeScript nos puede ayudar a no acceder a una propiedad o método de un objeto que no existe.

```typescript
const persona = {
  nombre: "Nicolas",
  edad: 45,
};

persona.apellido; // Tirra error ya que apellido no existe en el objeto persona
```

- TypeScript al notar que intentamos acceder a una propiedad que no existe nos muestra el siguiente error `Property 'apellido' does not exist on type '{ nombre: string; edad: number; }'`.
- En este caso TS puede inferir que hay un `object` que tiene las propiedades `nombre y edad` y por eso muestra el error.
- Si en VS Code posicionamos el cursor sobre la variable `persona` vemos la siguiente definición:

```typescript
const persona: {
  nombre: string;
  edad: number;
};
```

- En este caso vemos que TS está definiendo las propiedades del `object` persona como también cada tipo de dato para sus propiedades.
- Si queremos definir nosotros el tipo de objeto y sus propiedades podemos utilizar `:{}`.
- Las propiedades y métodos se separan con un `;` al final `propiedad: tipo_de_dato;`

```typescript
const persona: {
  nombre: string;
  edad: number;
} = {
  nombre: "Nicolas",
  edad: 45,
};
```

- Si sacamos una de las propiedades de la definición del objeto, TypeScript nos va a mostrar un error.

```typescript
const persona: {
  nombre: string;
} = {
  nombre: "Nicolas",
  edad: 45, // muestra error ya que no está definido que este objeto tenga una propiedad edad.
};
```

- TS muestra el siguiente error `Object literal may only specify known properties, and 'edad' does not exist in type '{ nombre: string; }'`
- Para objetos literales también podemos dejar que TS infiera las propiedades y métodos.
- En `objects` podemos utilizar el concepto de `propiedades opcionales`, es decir que una propiedad puede o no existir.
- En caso de que la propiedad no exista, JS va establecer el valor en undifined.
- Dado que la propiedad puede tener un valor indefinido es que tenemos que chequear por ese valor al utilizarlo.

```typescript
const persona: {
  nombre: string;
  apellido: string;
} = {
  nombre: "Nicolas",
  apellido: "Isnardi",
};

function saludar(datos: { nombre: string; apellido: string }) {
  console.log(`Hola ${datos.nombre} ${datos.apellido}`);
}

saludar(persona);
```

- En este ejemplo vemos un caso feliz, la persona tiene nombre y apellido y la función espera un objeto que tenga una propiedad con el nombre de `nombre` y otra `apellido`.
- Qué pasa si por ahí no sabemos el apellido de la persona porque nunca lo obtuvimos?
- Podemos hacer que el valor sea opcional agregando `?` al final del nombre de la propiedad `apellido?:tipo_de_dato`.
- Ahora si hacemos ese cambio, también lo tenemos que hacer en la función, no?

```typescript
const persona: {
  nombre: string;
  apellido?: string;
} = {
  nombre: "Nicolas",
};

function saludar(datos: { nombre: string; apellido?: string }) {
  console.log(
    // 'datos.apellido' is possibly 'undefined'.ts(18048)
    `Hola ${datos.nombre.toUpperCase()} ${datos.apellido.toUpperCase()}`
  );
}

saludar(persona);
```

- En este ejemplo llamamos al métod `toUpperCase()` del tipo de dato string.
- Si el valor en apellido es `undefined` estaríamos haciendo `undefined.toUpperCase()` y esto tiraría un error.
- TypeScript acá nos muestra el error que `apellido` puede ser string o undefined.
- En este caso tenemos que validar que apellido no sea undefined.

```typescript
const persona: {
  nombre: string;
  apellido?: string;
} = {
  nombre: "Nicolas",
};

function saludar(datos: { nombre: string; apellido?: string }) {
  if (datos.apellido) {
    console.log(
      `Hola ${datos.nombre.toUpperCase()} ${datos.apellido.toUpperCase()}`
    );
  } else {
    console.log(`Hola ${datos.nombre.toUpperCase()}`);
  }
}

saludar(persona);
```

- Usamos la forma `truthy / falsy` de JavaScript para validar que `datos.apellido` no sea `undefined` y mostramos el mensaje.
- Si apellido es undefined entonces mostramos solo el saludo con el nombre.
- Estamos seguros que el nombre llegó porque TypeScript nos da la tranquilidad que fué chequeado antes de transformar este código a JavaScript.
- De esta forma podemos utilizar propiedades o métodos opcionales en TypeScript.

### Alias

- Hasta ahora aprendimos como utilizar type annotation para definir los tipos de datos.
- Utilizando `type` podemos crear alias de un tipo de dato.
- Por ejemplo, utilizando lo que sabemos podemos crear un tipo desde cualquir tipo de dato que utilizamos, desde `strings` hasta `unions`.
- Es una forma de definir un alias para un tipo de dato que tenga más contexto en lo que estamos haciendo.

```typescript
type ID = number | string;
```

- En este caso estamos definiendo un alias para `number o string` que le da más contexto a lo que es el tipo de dato.
- Si bien sigue siendo una `union` nosotros lo utilizamos como el concepto de `ID`.
- También podemos utilizar esto para objetos.

```typescript
type Persona = {
  nombre: string;
  apellido: string;
};

const persona: Persona = {
  nombre: "Nicolas",
  apellido: "Isnardi",
};

function saludar(datos: Persona): void {
  console.log(`Hola ${datos.nombre} ${datos.apellido}`);
}

saludar(persona);
```

- Definimos un type (Alias) `Persona` que tiene las propiedades nombre y apellido donde ambas son string.
- Después creamos una variable con el nombre de persona y usamos type annotation para decir que es del tipo `Persona`.
- Esto le deja saber a TypeScript que cualquier valor que sea definido como `Persona` tiene propiedades `nombre y apellido del tipo string`.
- Ya que tengo la definición la puedo usar para asignar un objeto a una variable como también para utilizarlo como parámetro de una función.
- En la función me ahorro de tener que utilizar el type annotation para cada uno de los parámetros ya que le paso un objeto con tipo definido como `Persona`.
- El `void` al final de la función es ya que la misma no retorna ningún tipo de dato. Podemos sacarlo y TypeScript lo va a inferir.
- Cabe destacar que `type` es solo un `alias` y no permite ser utilizado para crear otros tipos de datos ya que es un `alias`.

### Interface

- `interface` es otra forma de poder definir tipos.
- Es muy parecido a los `alias` usando `types` pero con la diferencia que `interface` puede utilizado para extender tipos de datos y `alias` no.
- Por otro lado `interface` permite agregar propiedades luego de su definición mientras que `type` no lo permite. ( A mi gusto es difícil saber como es el tipo de dato si se hace esto luego de la definición).
- Para definir una interface utilizamos la palabra reservada `interface`, luego un nombre y por último `{}` con las propiedades.

```typescript
interface Animal {
  nombre: string;
  fechaDeNacimiento: string;
}
```

- En este caso definimos una interface con el nombre `Animal` que tiene como propiedades 2 strings con los nombres `nombre y fechaDeNacimiento`.
- Dado que es una interface podemos agregar propiedades.

```typescript
interface Animal {
  nombre: string;
  fechaDeNacimiento: string;
}

interface Animal {
  nada: boolean;
}

const animal: Animal = {
  nombre: "Amelia",
  fechaDeNacimiento: "01/07/2014",
  nada: true,
};
```

- TS va a mostrar un error si en lugar de utilizar `interface` utilizamos `type` ya que no se puede volver a "abrir" para declarar nuevas propiedades.
- Dado esta definición de `Animal`, también podemos utilizar algo parecido para `Persona`.

```typescript
interface SerVivo {
  nombre: string;
  fechaDeNacimiento: string;
  nada: boolean;
}

interface Animal extends SerVivo {
  cantidadDePatas: number;
}

interface Persona extends SerVivo {
  trabaja: boolean;
}

const animal: Animal = {
  nombre: "Amelia",
  fechaDeNacimiento: "01/07/2014",
  nada: false,
  cantidadDePatas: 4,
};

const persona: Persona = {
  nombre: "Nicolas",
  fechaDeNacimiento: "02/04/1979",
  nada: true,
  trabaja: true,
};
```

- La interface `SerVivo` ahora contiene las propiedades en común entre un `Animal` y una `Persona`.
- Tanto la interfaz `Animal` como `Persona` pueden definir sus propias propiedades extendiendo las que obtiene de `SerVivo`.
- TypeScript va a mostrar un error si al utilizar las interfaces falta alguna propiedad o está mal el nombre.
