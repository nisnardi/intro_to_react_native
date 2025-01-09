# JavaScript

## Objetos

- Otro de los tipos base que tenemos en ECMAScript son los **object**, es decir que tenemos objetos
- Los objetos nos ayudan a representar valores de una manera más fácil y agrupada
- Los objetos literales se escriben entre {}

**Ejemplo:**

```js
{
} // objeto literal
const miObjeto = {}; // objeto asignado a una variable
```

#### Prácticas

- [Ejercicio 143](../ejercicios/consignas/js/ej143.md)

### Propiedades

- Un objeto puede tener propiedades
- Las propiedades se definen con un nombre como si fueran variables
- A las propiedades se les puede asignar un valor utilizando dos puntos
- Las propiedades se separan con comas

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

console.log(persona);
```

- Podemos acceder a la propiedad de un objeto utilizando el nombre del objeto, punto y el nombre de la propiedad

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

console.log(persona.nombre);
console.log(persona.edad);
```

#### Prácticas

- [Ejercicio 144](../ejercicios/consignas/js/ej144.md)
- [Ejercicio 145](../ejercicios/consignas/js/ej145.md)
- [Ejercicio 146](../ejercicios/consignas/js/ej146.md)
- [Ejercicio 147](../ejercicios/consignas/js/ej147.md)

- Si accedemos a una propiedad que no existe vamos a obtener undefined

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

console.log(persona.dni); // undefined
```

- Para asignar un valor a una propiedad lo hacemos de la misma forma que lo hacemos con una variable

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

persona.nombre = "Martín";
persona.edad = 20;

console.log(persona);
// { nombre: 'Martín', edad: 20 }
```

- Las propiedades de un objeto terminan siendo variables de las cuales podemos obtener o asignar valores
- Un tema importante con los objetos de ECMAScript es que son dinámicos
- Podemos crear propiedades que no fueron definidas en el objeto
- Si bien es un gran beneficio tener esta flexibilidad nos puede dar un dolor de cabeza si no tenemos cuidado

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

console.log(persona.dni); // undefined

persona.nombre = "Martín";
persona.edad = 20;
persona.dni = 20202123;

console.log(persona);
// { nombre: 'Martín', edad: 20, dni: 20202123 }

console.log(persona.dni); // 20202123
```

- Podemos caer en el error de escribir mal una propiedad o por ahí utilizar mayúscula y no encontrar la propiedad buscada o eventualmente terminar creando nuevas propiedades
- De nuevo, por las dudas... tener cuidado con las propiedades de los objetos de ECMAScript

#### Prácticas

- [Ejercicio 148](../ejercicios/consignas/js/ej148.md)
- [Ejercicio 149](../ejercicios/consignas/js/ej149.md)

### Métodos

- Los objetos pueden tener métodos
- Un método es una propiedad que tiene una función

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  saludar: function () {
    console.log("Hola, cómo estan?");
  },
};
```

- Como podemos ver nombre y saludar son dos propiedades iguales
- Nombre tiene asinado un string
- Saludar tiene asignado una función como vimos antes

**Ejemplo:**

```js
const saludar = function () {
  console.log("Hola, cómo estan?");
};

saludar();
```

- Para ejecutar un método de un objeto lo hacemos de la misma forma casi:

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  saludar: function () {
    console.log("Hola, cómo estan?");
  },
};

persona.saludar(); // Hola, cómo estan?
```

#### Prácticas

- [Ejercicio 150](../ejercicios/consignas/js/ej150.md)
- [Ejercicio 151](../ejercicios/consignas/js/ej151.md)

- Cuando utilizamos métodos de string, number o arrays estabamos utilizando funciones propias de cada uno de estos tipos.
- **ECMAScript transforma los strings, numbers y arrays a objetos para poder utilizar métodos sobre estos tipos de datos**

- Un método también puede aceptar parámetros:

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  saludar: function (nombre) {
    console.log("Hola, " + nombre + " cómo estas?");
  },
};

persona.saludar("Marta"); // Hola, Marta cómo estas?
```

- Vemos que utilizar un método es muy similar a simplemente utilizar una función
- Esto se da porque un método es una función dentro de un objeto
- Dentro de los métodos también podemos acceder a las propiedades del objeto por medio de la palabra reservada **this**
- Por ahora podemos decir que **this** es una referencia al objeto que creamos

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  saludar: function () {
    console.log("Hola, mi nombre es " + this.nombre);
  },
};

persona.saludar(); // Hola, mi nombre es Nico
```

#### Prácticas

- [Ejercicio 152](../ejercicios/consignas/js/ej152.md)
- [Ejercicio 153](../ejercicios/consignas/js/ej153.md)
- [Ejercicio 154](../ejercicios/consignas/js/ej154.md)
- [Ejercicio 155](../ejercicios/consignas/js/ej155.md)
- [Ejercicio 156](../ejercicios/consignas/js/ej156.md)
- [Ejercicio 157](../ejercicios/consignas/js/ej157.md)
- [Ejercicio 158](../ejercicios/consignas/js/ej158.md)

- También dentro de un método podemos modificar una propiedad de un objeto

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
  saludar: function () {
    console.log("Hola, mi nombre es " + this.nombre);
  },
  cumpleanios: function () {
    this.edad++;
  },
};

console.log(persona.edad); // 38
persona.cumpleanios();
console.log(persona.edad); // 39
```

### Propiedades dinámicas de un objeto

- Puede pasar que no sabemos el nombre de una propiedad y necesitemos acceder de forma dinámica
- Podemos acceder a las propiedades utilizando los corchetes como si fueran array pero en lugar de pasarle un ídince numérico le pasamos el nombre de la propiedad

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
  saludar: function () {
    console.log("Hola, mi nombre es " + this.nombre);
  },
  cumpleanios: function () {
    this.edad++;
  },
};

console.log(persona["nombre"]); // nico
console.log(persona["edad"]); // 38
```

- Podemos hacer esto utilizando variables

**Ejemplo:**

```js
const nombre = "nombre";
const edad = "edad";

const persona = {
  nombre: "Nico",
  edad: 38,
  saludar: function () {
    console.log("Hola, mi nombre es " + this.nombre);
  },
  cumpleanios: function () {
    this.edad++;
  },
};

console.log(persona[nombre]); // nico
console.log(persona[edad]); // 38
```

#### Prácticas

- [Ejercicio 159](../ejercicios/consignas/js/ej159.md)
- [Ejercicio 160](../ejercicios/consignas/js/ej160.md)

- De esta forma podemos acceder a propiedades de un objeto de forma dinámica
- Esto es útil si lo usamos con `Object.keys`
- `Object.keys` retorna todas las propiedades de un objeto
- El método keys acepta un objeto como parámetro

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

const propiedades = Object.keys(persona);

propiedades.forEach(function (propiedad) {
  console.log(persona[propiedad]);
});
```

- Si agregamos más propiedades el código sigue pudiendo acceder a las propiedades de forma dinámica

**Ejemplo:**

```js
const persona = {
  nombre: "Nico",
  edad: 38,
};

persona.dni = 20202138;
persona.calle = "arcos 220";

const propiedades = Object.keys(persona);

propiedades.forEach(function (propiedad) {
  console.log(persona[propiedad]);
});
/*
  Nico
  38
  20202138
  arcos 220
*/
```

- Podes leer más sobre `Object.keys` en el [sitio del MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Object/keys)

#### Prácticas

- [Ejercicio 161](../ejercicios/consignas/js/ej161.md)
- [Ejercicio 162](../ejercicios/consignas/js/ej162.md)
