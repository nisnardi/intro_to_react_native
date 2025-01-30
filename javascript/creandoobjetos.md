# JavaScript

## Creando Objetos

- JavaScript tiene muchas formas de crear un objeto.

### Objetos literales

- Hasta ahora vimos que podemos crear `objetos` utilizando `objetos literales`.
- Los objetos literales son útiles y una manera fácil de agrupar datos y funcionalidad.

```javascript
const persona = {
  nombre: "Nicolas",
  apellido: "Isnardi",
  mostrarNombreCompleto: function () {
    console.log(`${this.nombre} ${this.apellido}`);
  },
};

persona.mostrarNombreCompleto();
```

- Otra forma de escribir métodos es por medio del `nombre(parametros) {}`.

```javascript
const persona = {
  nombre: "Nicolas",
  apellido: "Isnardi",

  mostrarNombreCompleto() {
    console.log(`${this.nombre} ${this.apellido}`);
  },
};

persona.mostrarNombreCompleto();
```

### Funciones constructoras

- Para poder crear más de un objeto con la misma estructura y funcionalidad podemos utilizar el concepto de `funciones constructoras`.
- Las funciones constructoras son `funciones` que retoran una nueva instancia de un objeto.
- Para crear una nueva instancia la función tiene que ser llamada con la palabra reservada `new`.
- La función acepta parámetros como cualquier otra función.
- Dentro de la función se utiliza la palabra reservada `this` para establecer valores a la nueva instancia.
- Cuando llamamos una función con `new` un nuevo objeto se crea y eso se llama instancia.
- La función constructora retoran la nueva instancia de manera implícita por lo cual no necesitamos hacer un return.
- Podemos establecer el nombre con la primer letra en mayúscula para distinguir que es una función constructora y no una función normal.
- La función constructora podemos pensarla como un template para crear objetos que tengan la misma estructura y funcionalidad para que sea más fácil crear y mantener objetos.

```javascript
function Persona(nombre, apellido) {
  this.nombre = nombre;
  this.apellido = apellido;
  this.mostrarNombreCompleto = function () {
    console.log(`${this.nombre} ${this.apellido}`);
  };
}

const persona = new Persona("Nicolas", "Isnardi");
const persona1 = new Persona("Ximena", "Cruz");

persona.mostrarNombreCompleto();
persona1.mostrarNombreCompleto();
```

- En este ejemplo vemos como utilizar una función para construir dos nuevas instancia de Persona.
- La función constructora es una `función` como las que vimos hasta ahora con la diferencia que utiliza la palabra reservada `this` para asignar un valor a una nueva instancia.
- La función acepta 2 parámetros `nombre y apellido` que luego son asignados a `this.nombre y this.apellido`.
- La nueva instancia tiene un método que se llama `mostrarNombreCompleto` que permite mostrar en pantalla el nombre y apellido de la persona.
- Para definir un método utilizamos una función y podemos utilizar `this` para hacer referencia a los datos y metodos de esa instancia.

```javascript
function Persona(nombre, apellido) {
  this.nombre = nombre;
  this.apellido = apellido;
  this.mostrarNombreCompleto = function () {
    console.log(`${this.nombre} ${this.apellido}`);
  };
}

const persona = new Persona("Nicolas", "Isnardi");
const persona1 = new Persona("Ximena", "Cruz");

persona.mostrarNombreCompleto();
persona1.mostrarNombreCompleto();

console.log(persona.nombre);
console.log(persona1.nombre);
```

- Podemos seguir utilizando las instancias de los objetos como lo hacíamos con objetos literales.
- Podemos asignar o borrar propiedades de manera dinámica de la misma forma que lo venimos haciendo.

### Metodo Create de Object

- Otra forma de crear objetos es por medio de `Object.create()`.
- Este metodo acepta un objeto como parámetro para ser utilizado como prototipo.

```javascript
const Persona = {
  nombre: "",
  apellido: "",
  mostrarNombreCompleto: function () {
    console.log(`${this.nombre} ${this.apellido}`);
  },
};

const persona = Object.create(Persona);
persona.nombre = "Nicolas";
persona.apellido = "Isnardi";

persona.mostrarNombreCompleto();
```

### Classes

- JavaScript agregó `Class` para poder crear objetos utilizando una clase como template.
- Esto es lo que se conoce como `syntaxis sugar` ya que se utiliza los mismos conceptos que utiliza JavaScript pero le da una forma más de `class` como en otros lenguages.
- Para crear una clase utilizamos la palabra reservada `class`, un `Nombre con la primer letra en mayúscula y `{}`.

```javascript
class Persona {}
```

- Las clases tienen una función especial llamada `constructor` que nos permite inicializar las propiedades de las instancias.
- La función `constructor` acepta parámetros necesarios para construir la nueva instancia.
- Para crear una instancia desde una clase también utilizamos la palabra reservada `new`.

```javascript
class Persona {
  constructor(nombre, apellido) {
    this.nombre = nombre;
    this.apellido = apellido;
  }
}

const persona = new Persona("Nicolas", "Isnardi");
console.log(persona.nombre);
```

- También podemos agregarle métodos a las clases.

```javascript
class Persona {
  constructor(nombre, apellido) {
    this.nombre = nombre;
    this.apellido = apellido;
  }

  mostrarNombreCompleto() {
    console.log(`${this.nombre} ${this.apellido}`);
  }
}

const persona = new Persona("Nicolas", "Isnardi");

persona.mostrarNombreCompleto();
```

- `Class` se utilizó durante un tiempo en React y React Native pero lentamente se fueron moviendo de este concepto.

### Comparar objetos

- JavaScript compara objetos por `referencia` lo cual significa que se fija si 2 objetos tienen la misma posición de memoria.
- Aún si dos objetos tienen las mismas propiedades y datos, la comparación es negativa.

```javascript
const persona1 = { nombre: "Nicolas" };
const persona2 = { nombre: "Nicolas" };

console.log(persona1 == persona2); // false
console.log(persona1 === persona2); // false
```

- Sólo asignando la misma referencia a otra variable hace que dos objetos sean iguales.

```javascript
const persona1 = { nombre: "Nicolas" };
const persona2 = persona1;

console.log(persona1 == persona2);
console.log(persona1 === persona2);
```

#### Practica

- [Ejercicio 196](../ejercicios/consignas/js/ej196.md)
- [Ejercicio 197](../ejercicios/consignas/js/ej197.md)
- [Ejercicio 198](../ejercicios/consignas/js/ej198.md)
