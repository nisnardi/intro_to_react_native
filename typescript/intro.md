# TypeScript

## Intro

- TypeScript es un lenguaje de programación fuertemente `tipado` que se `basa en JavaScript`.
- Podemos pensarlo como un JavaScript con esteroides
- JavaScript no es un lenguaje que valide tipos de datos y esto nos permite tener errores inesperados como el siguiente ejemplo:

```javascript
function sumar(numero1, numero2) {
  return numero1 + numero2;
}

sumar("uno", "dos");
sumar("1", "2");
```

- Dada la forma en la que funciona JavaScript, se puede llamar a esta función con parametros del tipo `string` y la función los va a concatenar.
- Si lo que se busca con esta función es sumar los dos valores y retornar un número en este caso podemos caer en un error inesperado.
- Con TypeScript podemos establecer que `tipo de dato` esperamos para cada parámetro y nos muestra un error antes de ejecutar el código en caso de cometer un error.

```typescript
function sumar(numero1: number, numero2: number) {
  return numero1 + numero2;
}

sumar("uno", "dos"); // Argument of type 'string' is not assignable to parameter of type 'number'.
sumar("1", "2"); // Argument of type 'string' is not assignable to parameter of type 'number'.
```

- Al utilizar TypeScript nos va a marcar un error de tipo que nos ayuda a prevenir errores a la hora de ejecutar el código.
- TypeScript convierte código de TypeScript a JavaScript para cualquier plataforma que pueda ejecutar el lenguaje, como el browser, Node u otros.
- TypScript puede interferir los tipos de datos sin código adicional, como que sabe leer e interpretar el código JavaScript y detectar los tipos de datos por su cuenta (y muchas veces lo hace super bien).
- Podemos utilizar el [playground de TS](https://www.typescriptlang.org/play/) para poder ver TypeScript en acción y como transforma a JavaScript.
- TypeScript nos permite utilizar nuevas features de JavaScript, chequear tipos de datos y hasta compilar JavaScript para que funcione en browsers con motores de JS más viejos.
