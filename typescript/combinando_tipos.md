# TypeScript

## Combinando tipos

### Union

- TypeScript permite crear tipos combinando los existentes como `string, number, boolean, etc`.
- La forma más fácil de combinar tipos es lo que se conoce como una `union o union`.
- Podemos establecer que un valor puede ser de un tipo u otro tipo, por ejemplo, un valor puede ser `string` o `number` y TS valida que sólo esos dos tipos de datos sean válidos.
- Para establecer una union utilizamos el símbolo `|` para establecer el tipo de valor.
- Podemos utilizar 2 o más tipos de datos separados por `|`.

```typescript
// Válido ya que es un número.
let numero: string | number = 5;

// Válido ya que es un string.
numero = "5";

// Tira un error porque undefined no es ni string ni número.
numero = undefined;
```

- En este ejemplo vemos como `string` o `number` son `union members` o miembros de la union y son los tipos de datos permitidos.
- Cualquier otro tipo de dato tira error.

```typescript
// Válido ya que es un número.
let numero: string | number | undefined = 5;

// Válido ya que es un string.
numero = "5";

// Válido
numero = undefined;
```

- Trabajar con `union` es útil pero al igual que los parámetros opcionales nos hace tener que validar el tipo de dato para poder utilizar un método o hacer una operación según el tipo de valor.

```typescript
function sumar(number1: string | number, number2: string | number) {
  // Podemos validar el tipo de dato y permitir que venga un string o un número
  const valor1 = typeof number1 === "string" ? parseInt(number1) : number1;
  const valor2 = typeof number2 === "string" ? parseInt(number2) : number2;

  console.log(
    `El resultado de sumar ${number1} y ${number2} es ${valor1 + valor2}`
  );
}

sumar(4, 10);
sumar("4", "10");
```

- Todavía queda un caso más por validar y es que le pasemos a la función un valor que no puede convertir a número.
- En algunas operaciones JavaScript puede utilizar un valor llamado `NaN` que significa `Not a Number` o no es un número.
- Podemos validar los parámetros de entrada, hacer la operación y si el resultado da `NaN` entonces tiramos un error.

```typescript
function sumar(number1: string | number, number2: string | number) {
  try {
    const valor1 = typeof number1 === "string" ? parseInt(number1) : number1;
    const valor2 = typeof number2 === "string" ? parseInt(number2) : number2;
    const resultado = valor1 + valor2;

    if (isNaN(resultado)) {
      throw new Error("No se pueden sumar los valores pasados por parámetro");
    }

    console.log(
      `El resultado de sumar ${number1} y ${number2} es ${resultado}`
    );
  } catch (error) {
    console.log("error");
  }
}

sumar(4, 10);
sumar("4", "10");
sumar("Nico", "10");
```

- Ahora si nuestra función acepta `string | number` como tipo de datos de los parámetros y la función siempre imprime el resultado validando tipo de datos y si hay algún error.
- En algún caso se puede dar que los tipo de datos tengan métodos o propiedades con el mismo nombre y en esos casos es seguro utilizarlos sin comprobar.

```typescript
const animales = ["Perro", "Gato", "Mono"];
const numero = 42;

function mostrarDatos(valor: string[] | number) {
  return valor.toString();
}

const valor1 = mostrarDatos(animales);
const valor2 = mostrarDatos(numero);

console.log(valor1);
console.log(valor2);
```

- TypeScript no muestra ni tira ningún error en este caso ya que tanto la colección animales o un número tienen el método `toString`.
- En este caso no hay validación ya que la función no va a tirar error.

### Tuple

- JavaScript no tiene el tipo de dato `Tuple` que es un array con una cantidad de elementos determinados y con un tipo de dato definido para cada item.
- En JavaScript va a ser un array normal pero en TS podemos definir la cantidad y tipos de items que tiene un `tuple`.
- Al definir un tuple especificamos `[]` para decir que es una colección pero además ponemos tipo de dato para cada posicion.
- Por ejemplo si queremos definir un array con sólo 2 items donde el primero es número y el segundo es un estring: `[number, string];`.

```typescript
const fila: [number, string] = [1, "Nicolas"];

fila[0] = "Juan"; // Esto  muestra un error.
```

- TS nos muestra el siguiente error `Type 'string' is not assignable to type 'number'` ya que definimos que el primer item de la colección es un `number` y no un `string`.
- Si queremos definir más items lo podemos hacer agregando más definiciones: `[number, string, string, number]`;

```typescript
const fila: [number, string, string, number] = [1, "Nicolas", "Juan", 42];

fila[2] = 10; // vemos un error ya que espera un string en esa posición.
```

- Un downside de `tuple` es que no valida al utilizar `push` los valores que tiene la colección.

```typescript
const fila: [number, string] = [1, "Nicolas"];

fila.push("juan");
```

- La longitud del `tuple` se valida sólo si lo hacemos manualmente:

```typescript
const fila: [number, string] = [1, "Nicolas", "Juan"]; // Error
```

- TS muestra el error `Source has 3 element(s) but target allows only 2.` para mostrarnos que tenemos un item de más.

### Valores literales

- TypeScript permite utilizar valores literales como tipo de datos.

```typescript
const animal = "Perro";
```

- TypeScript toma la definición de este tipo de dato como `const animal: "Perro"` ya que en una constante no se puede cambiar el valor y sería siempre del tipo `perro` en formato string.
- Utilizando union podemos definir que una variable puede aceptar valores literales diferentes.

```typescript
type Animales = "Perro" | "Gato" | "Mono";

// Definición válida
const animal: Animales = "Gato";

// Type '"Elefante"' is not assignable to type 'Animales'
const animal2: Animales = "Elefante";
```

- En este ejemplo creamos un alias con los valores literales de `Perro, Gato y Mono`.
- Esto significa que cualquier valor utilizando el tipo de dato Animal puede sólo tener el valor de Perro o Gato o Mono.
- Este concepto es útil también a la hora de definir parámetos en propiedades.

```typescript
function getBorder(size: "small" | "medium" | "large" = "small") {
  if (size === "small") {
    return 4;
  } else if (size === "medium") {
    return 8;
  } else {
    return 12;
  }
}

const borderSize = getBorder("medium");
console.log(borderSize);
```

- Definimos que el parámetro size puede ser sólo la palabra `small, medium o large`.
- Establecemos el valor por defecto en `small`, es decir que si no se pasa ningún parámetro esta función retorna 4.
- A la hora de ejecutar la función `getBorder` sólo se puede pasar como parámetro el string literal de `small, medium o large`.
- Otra forma de hacer esto sería definir un alias con los valores que necesitamos y utilizarlo como tipo de dato.

```typescript
type BorderSize = "small" | "medium" | "large";

function getBorder(size: BorderSize = "small") {
  if (size === "small") {
    return 4;
  } else if (size === "medium") {
    return 8;
  } else {
    return 12;
  }
}

const borderSize = getBorder("medium");
console.log(borderSize);
```

- En este ejemplo se ve como podemos utilizar `union` y un `alias o type` para poder crear un nuevo tipo de dato que con un nombre le damos contexto para lo que puede ser utilizado o lo que significa.
- El siguiente ejemplo sale de la Guía de TypeScript y muestra un buen ejemplo de como se pueden usar numeros literales como retorno de una función para sort u ordenamiento.

```typescript
function compare(a: string, b: string): -1 | 0 | 1 {
  return a === b ? 0 : a > b ? 1 : -1;
}
```

- La función `compare` devuelve los valores `-1, 0 o 1` a la hora de comparar valores mientra que los parámetros de entrada son un `string`.

### Type Assertions

- `Type Assertions` es como decirle al compilador de TypeScript `Si no sabes que tipo de dato es.. confía en mi`.
- Esto no previene errores de ejecución pero si ayuda en tiempo de compilación.
- Es una forma de decirle a TypeScript, ejecutá este código que va andar bien.
- Para utilizar `type assertion` utilizamos la palabra `as`.

```typescript
function mostrarLongitud(data: unknown) {
  const longitud = (data as string).length;
  console.log("Longitud:", longitud);
}

mostrarLongitud("Vamos TypeScript!!");
```

- En este ejemplo simulamos una función donde no sabemos el tipo de dato que entra como parámetro.
- Si estamos seguros que va a ser un string podríamos declararlo como tal pero en algunas oportunidades no podemos.
- Es ahí donde entra la opción de decirle a TypeScript usa este dato como si fuera de tal tipo.
- Acá usamos `data as string` para establecer que TS tiene que confiar que este dato es un `string` y que va a tener la propiedad `length`.
