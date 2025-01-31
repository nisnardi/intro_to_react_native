# JavaScript

## Nuevos Iteradores

- JavaScript incorporó 2 iteradores llamados `for of` y `for in`.
- Se utilizan de manera diferentes.

### For of

- Se usa para iterar `iterables` como pueden ser los `arrays, strings, maps, sets`.
- En cada iteración se obtiene un item del iterable.

```javascript
for (const item of iterable) {
  // Código a ejecutar por cada item
}
```

- Ejemplo con una colección:

```javascript
const animales = ["perro", "gato", "elefante"];

for (const animal of animales) {
  console.log(animal);
}
```

- Ejemplo con un string:

```javascript
const texto = "Nicolas";

for (const letra of texto) {
  console.log(letra);
}
```

### For in

- Se utiliza para iterar por las propiedades de un `objeto`.
- Podemos decir que es algo parecido a usar `Object.keys()` y después iterarlo.
- A diferencia de `for of`, este iterador devuelve la `key` o `propiedad` del objeto iterado.

```javascript
for (const key in object) {
  // Código a ejecutar
}
```

- Ejemplo:

```javascript
const usuario = {
  name: "Nicolas",
  age: 45,
  city: "Toronto",
};

for (const key in usuario) {
  console.log(`${key}: ${usuario[key]}`);
}
```

#### Practica

- [Ejercicio 203](../ejercicios/consignas/js/ej203.md)
- [Ejercicio 204](../ejercicios/consignas/js/ej204.md)
