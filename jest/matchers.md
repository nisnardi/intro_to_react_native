# Jest

## Matchers

- Como sabemos `jest` utiliza `matchers` para testear valores esperados.
- `jest` provee varios `matchers` y también se pueden agregar / configurar otros.
- Al crear tests vamos a utilizar diferentes `matchers` que mejor se adapten al valor que queremos testear.
- Uno muy común es `toBe`.

### ToBe

- `toBe` utiliza JavaScript `Object.is()`.
- Este matcher compara valores por igualdad de `valor`.
- Podemos utilizar este matcher para valores como `numeros, strings, booleans` pero no para `objetos u arrays`.
- Si queres aprender más de `Object.is` podes leer la [guía del MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is)

```javascript
test("Testeando toBe", () => {
  expect(false).toBe(false);
  expect(3).toBe(3);
  expect("Nicolas").toBe("Nicolas");
});
```

### toEqua

- Para testear objetos o arrays podemos utilizar `toEqual`.
- `.toEqual` recorre cada propiedad de un objeto o items de una colección para así compararlos.

```javascript
test("Testeando toEqual en objetos", () => {
  const objeto1 = {
    nombre: "Nicolas",
  };

  const objeto2 = {
    nombre: "Nicolas",
  };

  // expect(objeto1).toBe(objeto2); // Esto tiraría un error por comparar por valor
  expect(objeto1).toEqual(objeto2);
});

test("Testeando toEqual en arrays", () => {
  const animales1 = ["Perro", "Gato"];
  const animales2 = ["Perro", "Gato"];

  // expect(animales1).toBe(animales2); // esto tira error por no ser el mismo valor
  expect(animales1).toEqual(animales2);
});
```

- En algun caso necesitamos chequear que dos objetos sean la misma instancia y en ese caso podemos utilizar `toStrictEqual`

```javascript
test("Testeando igualdad por referencia", () => {
  function Animal(nombre) {
    this.nombre = nombre;
  }

  // Este expect pasa sin problemas
  expect(new Animal("Amelia")).toEqual({ nombre: "Amelia" });

  // Este expect tira error ya que no son el mismo objeto
  expect(new Animal("Amelia")).toStrictEqual({ nombre: "Amelia" });
});
```

### not

- En algunos tests por ahí necesitamos negar la comparación y decir que no queremos que un valor sea otro valor.
- En este caso podemos utilizar `.not` antes del `matcher`.

```javascript
test("Test", () => {
  const animales = ["Perro"];

  expect(animales.leangth).not.toBe(0);
});
```

- En este caso comprobamos que la longitud de la colección no sea 0 para saber que no está vacio.
- No nos importa cuántos items tiene la colección, sólo que no esté vacia.

### Testeando undefined, null y false

- `jest` provee algunos `matchers` que nos permiten testear si un valor es `undefined, null o false`.

```jest

```
