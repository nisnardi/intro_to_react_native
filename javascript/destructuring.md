# JavaScript

## Destructuring

- `Destructuring` se conoce como la técnica para obtener valores de un `array` o `propiedades de un objeto` de manera más fácil y asignarlo a variables.

### Array destructuring

- Hasta ahora para asignar un valor de un array a una variable teníamos que hacer lo siguiente:

```javascript
const animales = ["leon", "perro", "gato"];

const primerAnimal = animales[0];
const segundoAnimal = animales[1];

console.log(primerAnimal);
console.log(segundoAnimal);
```

- Por medio de destructuring podemos obtener el mismo resultado de la siguiente manera:

```javascript
const [primerAnimal, segundoAnimal] = animales;

console.log(primerAnimal);
console.log(segundoAnimal);
```

- En este ejemplo vemos como utilizando `[]` al crear las variables y asignar el array podemos obtener los valores y ponerle el nombre que mejor nos quede.
- Utilizando comas podemos salerar items del array y asignar valores de la siguiente manera:

```javascript
const [primerAnimal, , tercerAnimal] = animales;

console.log(primerAnimal);
console.log(tercerAnimal);
```

- Por medio de destructuring tambien se puede asignar valores por defecto en caso de que no existan los items en el array.
- Esto sólo funciona si el valor en el array es `undefined`.

```javascript
const animales = ["leon"];
const [primerAnimal, segundoAnimal = "Loro"] = animales;

console.log(primerAnimal);
console.log(segundoAnimal);
```

- `Destructuring` se combina bien con `rest`.
- Podemos obtener los valores que necesitamos de un array y nombrarlo con variables.
- El resto de los valores los podemos poner en otra colección.

```javascript
const animales = ["leon", "perro", "gato"];
const [primerAnimal, ...otrosAnimales] = animales;

console.log(primerAnimal);
console.log(otrosAnimales);
```

- En este caso obtenemos el primer item y lo asignamos a la variable `primerAnimal`.
- El resto de los animales de la colección son asignados a `otrosAnimales`.

### Destructuring en objetos

- Para asignar el valor de una propiedad de un objeto en una variable:

```javascript
const persona = { nombre: "Marta", edad: 35 };
const nombre = persona.nombre;
const edad = persona.edad;

console.log(nombre); // "Marta"
console.log(edad); // 35
```

- Siguiendo el concepto anterior podemos obtener propiedades de un objeto y asignarlas a una variable.

```javascript
const persona = { nombre: "Marta", edad: 35 };
const { nombre, edad } = persona;

console.log(nombre); // "Marta"
console.log(edad); // 35
```

- Al utilizar destructuring también podemos renombrar las variables con un nombre diferente a las propiedades.
- Para poder renombrar una propiedad podemos hacer `propiedad: nuevoNombre`.

```javascript
const persona = { nombre: "Marta", edad: 35 };
const { nombre: name, edad } = persona;

console.log(name); // "Marta"
console.log(edad); // 35
```

- En este ejemplo le cambiamos el nombre a la propiedad `nombre` por `name`.
- Luego de definir la propiedad `nombre` como `name` podemos utilizar `name` en el resto del código.
- Al igual que con Arrays podemos establecer valores por defecto si la propiedad no existe.
- Para asignar un valor por defecto utilizamos el operador `=` como si asignaramos un valor a una variable.

```javascript
const persona = { nombre: "Marta", edad: 35 };
const { nombre, edad, enPareja = true } = persona;

console.log(nombre); // "Marta"
console.log(edad); // 35
console.log(enPareja);
```

- También podemos utilizar `rest` con `destructuring de objetos`.

```javascript
const persona = { nombre: "Marta", edad: 35, enPareja: true };
const { nombre, ...otrasPropiedades } = persona;

console.log(nombre); // "Marta"
console.log(otrasPropiedades); // { edad: 35, enPareja: true }
```

- `Destructuring` también funciona con objetos enlazados.

```javascript
const persona = {
  nombre: "Marta",
  edad: 35,
  enPareja: true,
  domicilio: { calle: "lala", altura: 1234 },
};
const {
  nombre,
  domicilio: { calle, altura },
} = persona;

console.log(nombre); // "Marta"
console.log(calle); // lala
console.log(altura); // 1234
```

- Puedes aprender más sobre destructuring en la [guía de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment).

#### Practica

- [Ejercicio 193](../ejercicios/consignas/js/ej193.md)
- [Ejercicio 194](../ejercicios/consignas/js/ej194.md)
