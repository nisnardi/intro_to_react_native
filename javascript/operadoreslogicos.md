# JavaScript

## Operadores lógicos

- Existen operadores lógicos que nos permiten anidar condicionales
- Puedo saber si dos conciones son **true** utilizando el operador `&&` conocido como **and** o en español como **Y**
- Por ejemplo si queremos saber si el la edad del usuario es mayor de 18 años y si el password es el esperado lo podemos hacer de la siguiente manera
- Para que este operador retorne **true** ambas condiciones deben ser verdaderas

**Ejemplo**

```js
let edad = 20;
let password = "js1234";
let resultado = edad >= 18 && password === "js1234";
console.log("resultado: ", resultado); // true
```

- En este ejemplo obtenemos un valor de true ya que ambas condiciones (edad >= 18 y password === 'js1234') son verdaderas
- Existe el operador `||` conocido como **or** u **O** en español que nos permite preguntar si al menos una de 2 condiciones es verdadera.
- Si la primer condición es verdadera ya no evalúa la segunda ya que al menos una de las dos condiciones es verdadera
- Caso de que la primer condición no sea verdadera va a comprobar si la segunda lo es
- Si ninguna de las dos condiciones es verdadera retorna falso
- Este operador retorna **true** si al menos una de las condiciones es verdadera

**Ejemplo**

```js
let edad = 20;
let password = "js12345";
let resultado = edad >= 18 || password === "js1234";
console.log("resultado: ", resultado); // true
```

- En este caso la condición es verdadera ya que la edad del usuario es mayor a 18 y no importa si el password es igual o no

**Ejemplo**

```js
let edad = 10;
let password = "js1234";
let resultado = edad >= 18 || password === "js1234";
console.log("resultado: ", resultado); // true
```

- En este caso el resultado es **true** ya que el usuario no es mayor de 18 pero el password es correcto

**Ejemplo**

```js
let edad = 10;
let password = "js12345";
let resultado = edad >= 18 || password === "js1234";
console.log("resultado: ", resultado); // false
```

- En este caso la condición es **false** ya que ambas condiciones son falsas

## Negación

- Por medio del operador `!` podemos negar una condición
- Si tenemos un valor **true** negado obtenemos un valor **false**
- Si tenemos un valor **false** negado obtenemos un valor **true**

**Ejemplo**

```js
console.log(!true); // false
console.log(!false); // true
```

- Por ejemplo podemos utilizar la negación en el siguiente caso:

**Ejemplo**

```js
let edad = 21;
let resultado = edad < 18;
console.log("El usuario es mayor de edad?: ", !resultado); // la condición es false pero al negarla pasa a ser verdadera
```

#### Práctica

- [Ejercicio 36](../ejercicios/consignas/js/ej36.md)
- [Ejercicio 37](../ejercicios/consignas/js/ej37.md)
