# Jest

## Comparadores / Matchers

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
  - `.toBeNull()`: valida si el valor obtenido es `null`.
  - `.toBeUndefined()`: valida si el valor obtenido es `undefined`.
  - `.toBeDefined()`: valida si el valor obtenido no es `undefined`.

```javascript
test("Test null & undefined", () => {
  const valorNulo = null;
  var valorIndefinido;
  const nombre = "Nicolas";

  expect(valorNulo).toBeNull();
  expect(valorIndefinido).toBeUndefined();
  expect(nombre).not.toBeUndefined();
  expect(nombre).toBeDefined();
});
```

- En este ejemplo vemos como podemos testear si un valor es `null` o `undefined`.
- También podemos utilizar `not` para testear que un valor `no sea undefined`.
- `jest` nos da `toBeDefined` para poder testear si un valor no es `undefined`.
- La idea es utilizar estos matchers para no tener que lidiar con valores `undefined`.
- Dado que `jest` es utilizado con JavaScript también podemos utilizar matchers para testear valores `Truthy o Falsy` como hacemos en los `if statements`.
  - `.toBeTruthy()`: valida que el valor sea `truthy`.
  - `.toBeFalsy()`: valida que el valor sea `falsy`.

```javascript
test("Test truty & falsy", () => {
  // Falsy
  const textoVacio = "";
  const cero = 0;
  const nulo = null;
  const indefinido = null;

  // Truthy
  const objeto = {};
  const coleccion = [];
  const nombre = "Nicolas";

  expect(textoVacio).toBeFalsy();
  expect(cero).toBeFalsy();
  expect(nulo).toBeFalsy();
  expect(indefinido).toBeFalsy();

  expect(objeto).toBeTruthy();
  expect(coleccion).toBeTruthy();
  expect(nombre).toBeTruthy();
});
```

- También podemos testear relaciones entre números.
  - `.toBeGreaterThan()`: valida que el número sea más grande que el número esperado.
  - `.toBeGreaterThanOrEqual()`: valida que el número sea más grande o igual que el número esperado.
  - `.toBeLessThan()`: valida que el número sea más chico que el número esperado.
  - `.toBeLessThanOrEqual()`: valida que el número sea más chico o igual que el número esperado.
  - `toBeCloseTo()`: valida que el número (float o decimal) esté cerca al valor esperado. Esta opción es útil para evitar problemas de redondeo.
- Para comparar números también se puede utilizar `.toBe()` y `.toMatch()`.

```javascript
test("Test números", () => {
  expect(2).toBeGreaterThan(1);
  expect(1).toBeGreaterThanOrEqual(1);

  expect(1).toBeLessThan(2);
  expect(1).toBeLessThanOrEqual(1);

  expect(1).toBe(1);
  expect(1).toEqual(1);

  expect(0.3985).toBeCloseTo(0.4);
});
```

- En los arrays podemos tambien utlizar `.toContain()` para validar si un item se encuentra dentro de la colección.
- De esta forma no tenemos que utilizar números u otras técnicas para testear un valor de la colección.

```javascript
test("Test coleccion", () => {
  const animales = ["Perro", "Gato", "Mono"];

  expect(animales).toContain("Mono");
});
```

- En algunos tests también podemos o necesitamos testear si una función o un método tiran un error.
- `jest` nos da `.toThrow()` para detectar si un código tira una exepción.
- También podemos utilizar `.toThrow(error)` para testear un tipo de error especial.
- Un dato importante a la hora de testear `Exeptions` es que el expect tiene que utilizar un `callback` como parámetro y dentro del mismo ejecutamos la función que tira la exepción.

```javascript
function validarUsuario() {
  throw new Error("Testing jest Error");
}

test("Test throw error", () => {
  expect(() => {
    validarUsuario();
  }).toThrow();

  expect(() => {
    validarUsuario();
  }).toThrow("Testing jest Error");

  expect(() => {
    validarUsuario();
  }).toThrow(new Error("Testing jest Error"));
});
```

- `jest` tiene muchos más matchers que puedes aprender leyendo la [Guía oficial de Jest](https://jestjs.io/docs/expect)
