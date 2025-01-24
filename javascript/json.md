# JavaScript

## JSON

- `JSON` es por `JavaScript Object notation`.
- `JSON` es un formato que nos permite intercambiar datos de una manera simple y liviano.
- `JSON` se parece mucho a un objeto en JavaScript pero con algunas diferencias.
- Es fácil de leer, entender la estructura y jerarquía entre los datos.
- Se utiliza mucho a la hora de transferir datos entre un cliente y un servidor.
- Podemos mandar datos en formato `JSON` que luegos serán convertidos del lado del servidor.
- Hacemos lo mismo cuando el servidor envía de vuelta una respuesta donde los datos están en formato `JSON`.
- `JSON` se representa como un objeto utilizando `{}` utilizando pares de clave y valor.
- Las claves tienen que estar en formato string por lo cual van entre `""` y se utiliza siempre comilla doble.
- Los valores pueden ser `strings, otros objetos, arrays, boolean o null`.

```json
{
  "nombre": "Nicolas",
  "apellido": "Isnardi",
  "edad": 45,
  "amigos": ["Cristian", "Char", "Mauri"],
  "hinchaDe": {
    "nombre": "Club Atlético Boca Juniors"
  }
}
```

- JavaScript nos da dos funciones que nos permiten interactuar con `JSON`.
- `JSON.parse` transforma un objeto JSON en objeto de JavaScript.
- `JSON.stringify` transforma un objeto JavaScript en objeto de JSON.

```javascript
const objetoJavaScript = {
  nombre: "Nicolas",
  apellido: "Isnardi",
  edad: 45,
  amigos: ["Cristian", "Char", "Mauri"],
  hinchaDe: {
    nombre: "Club Atlético Boca Juniors",
  },
};

// Pasamos el objeto de JS a JSON
const objetoPasadoAJson = JSON.stringify(objetoJavaScript);
console.log(objetoPasadoAJson);

// Pasamos el objeto de JSON a JavaScript
const objetoJs = JSON.parse(objetoPasadoAJson);
console.log(objetoJs);
```

- [JSON MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON)
