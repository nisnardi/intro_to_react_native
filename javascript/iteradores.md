# JavaScript

## ForEach

- Podemos iterar o recorrer un array utilizando el método forEach()
- Este método acepta una función como parámetro
- La función que le pasamos a este método recibe como parámetro cada uno de los elementos del array

**Ejemplo:**

```js
const alumnos = ["nico", "pedro", "marta", "belen", "emilia"];

alumnos.forEach(function (alumno) {
  console.log(alumno);
});
```

- En este ejemplo vemos que podemos utilizar el método forEach en el array alumnos
- Le pasamos un function como parámetro como si fuera cualquier otro tipo de parámetro (number, string, etc)
- El parámetro que recibe esta función en este caso le pusimos alumno ya que estamos recorriendo una colección de alumnos
- Le podemos poner el nombre que queremos al parámetro

**Ejemplo:**

```js
const mascotas = ["Amelia", "Ciro", "Ulises", "Carlos"];

mascotas.forEach(function (mascota) {
  console.log(mascota);
});
```

- En este caso la colección es de mascotas por lo cual utilizamos el nombre mascota para que tenga sentido que cada elemento de la colección es una mascota. Podríamos utilizar otros como item, elemento o lo que a nosotros nos guste. Siempre es mejor poner un nombre con contexto que explique de forma fácil de que es la colección que estamos iterando y los elementos que estamos utilizando

- Podemos obtener otro parámetro más en la función que se ejecuta por cada elemento que es el índice del elemento

**Ejemplo:**

```js
const mascotas = ["Amelia", "Ciro", "Ulises", "Carlos"];

mascotas.forEach(function (mascota, indice) {
  console.log("indice", indice);
  console.log(mascota);
});
/*
indice 0
Amelia
indice 1
Ciro
indice 2
Ulises
indice 3
Carlos
*/
```

- Vemos en este ejemplo que agregando un segundo parámetro podemos obtener el índice de los elementos y como primer valor el elemento en sí.

#### Prácticas

- [Ejercicio 135](../ejercicios/consignas/js/ej135.md)
- [Ejercicio 136](../ejercicios/consignas/js/ej136.md)

## Map

- El método **map** crea un nuevo **array** con el resultado de la función que le pasamos como parámetros
- Podemos utilizar este método para cambiar los valores que tenemos en un array
- En la función que pasamos como parámetro tenemos que retornar el elemento que queremos en el nuevo array

**Ejemplo:**

```js
const mascotas = ["Amelia", "Ciro", "Ulises", "Carlos"];
const mascotasMayuscula = mascotas.map(function (mascota) {
  return mascota.toUpperCase();
});

console.log(mascotasMayuscula); // [ 'AMELIA', 'CIRO', 'ULISES', 'CARLOS' ] Todos en mayúscula
console.log(mascotas); // ['Amelia', 'Ciro', 'Ulises', 'Carlos'] Este array quedó igual que antes
```

- En este ejemplo vemos como podemos utilizar **map** para crear un nuevo array modificando los valores de otro array
- El array original queda intacto

#### Prácticas

- [Ejercicio 137](../ejercicios/consignas/js/ej137.md)
- [Ejercicio 138](../ejercicios/consignas/js/ej138.md)

## Filter

- El método **filter** retorna un nuevo **array** utilizando un filtro
- Pasamos una función que retorna verdadero o falso para saber si debemos añadir el nuevo elemento al nuevo array o no

**Ejemplo:**

```js
const notas = [1, 2, 3, 4, 10, 5];
const notasGrosas = notas.filter(function (nota) {
  return nota === 10;
});

console.log(notasGrosas); // [10] array con una sola nota grosa
console.log(notas); // [1, 2, 3, 4, 10, 5] array original
```

#### Prácticas

- [Ejercicio 139](../ejercicios/consignas/js/ej139.md)
- [Ejercicio 140](../ejercicios/consignas/js/ej140.md)

## Reduce

- El método **reduce** nos permite recorrer un array y obtener un sólo dato como resultado final
- Acepta una función con dos parámetro
  - Primer parámetro es el acumulador
  - El segundo valor es cada item en el array
- Podemos utilizar el acumulador para ir sumando valores, por ejemplo:

**Ejemplo:**

```js
const notas = [1, 2, 3, 4, 10, 5];
const sumaDeNotas = notas.reduce(function (total, nota) {
  return total + nota;
});

console.log(sumaDeNotas); // 25 resultado final de sumar todas las notas
```

#### Prácticas

- [Ejercicio 141](../ejercicios/consignas/js/ej141.md)
- [Ejercicio 142](../ejercicios/consignas/js/ej142.md)

Podes ver más métodos de array en el [sitio de MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array)
