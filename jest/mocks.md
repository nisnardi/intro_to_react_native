# Jest

## Mocks

- `Mocks` es una forma de evitar ejecutar código real y remplazarlo por otra función que definamos.
- Esto permite testear código que depende de otros módulos sin ellos.
- También permite cambiar la implementación de alguna función o asegurarnos que una función fué llamada como parte de la ejecución del código.
- `jest` nos da una función que podemos utilizar como `mock` para testear código.

```javascript
function recorrer(items, callback) {
  let counter = 0;
  for (const item of items) {
    counter += 1;
    callback(`${counter} ${item}`);
  }
}

const mockCallback = jest.fn((x) => x.toUpperCase());

test("forEach mock function", () => {
  const animales = ["Perro", "Gato", "Mono"];

  recorrer(animales, mockCallback);

  expect(mockCallback.mock.calls).toHaveLength(3);

  expect(mockCallback.mock.calls[0][0]).toBe("1 Perro");
  expect(mockCallback.mock.calls[1][0]).toBe("2 Gato");
  expect(mockCallback.mock.calls[2][0]).toBe("3 Mono");

  expect(mockCallback.mock.results[0].value).toBe("1 PERRO");
  expect(mockCallback.mock.results[1].value).toBe("2 GATO");
  expect(mockCallback.mock.results[2].value).toBe("3 MONO");
});
```

- También podemos utilizar `mock` para establecer el valor de retonro de una función.
  - `.mockReturnValueOnce()`: nos permite definir que valor retorna esta función al ser llamada una vez.
  - `.mockReturnValue()`: nos permite definir que valor retorna esta función siempre.
- Estas dos funciones se puden combinar:

```javascript
test("forEach mock function", () => {
  const fetchMock = jest
    .fn()
    .mockReturnValueOnce({ page: 1, data: [{ nombre: "Nicolas" }] })
    .mockReturnValueOnce({ page: 2, data: [{ nombre: "Matias" }] })
    .mockReturnValue({ page: 3, data: [{ nombre: "Willi" }] });

  const data1 = fetchMock();
  const data2 = fetchMock();
  const data3 = fetchMock();
  const data4 = fetchMock();
  const data5 = fetchMock();

  expect(data1.page).toBe(1);
  expect(data1.data[0]).toEqual({ nombre: "Nicolas" });

  expect(data2.page).toBe(2);
  expect(data2.data[0]).toEqual({ nombre: "Matias" });

  expect(data3.page).toBe(3);
  expect(data3.data[0]).toEqual({ nombre: "Willi" });

  expect(data5.page).toBe(3);
  expect(data5.data[0]).toEqual({ nombre: "Willi" });
});
```

- En este caso simulamos tener una función como fetch que puede cambiar el valor de retorno en cada llamado.
- Usando `mockReturnValueOnce` establecemos que la primera vez retorne un objeto con la página en 1.
- Al llamar por segunda vez, utilizamos también `mockReturnValueOnce` establecemos que la primera vez retorne un objeto con la página en 2.
- A partir de ahí, cada vez que llamemos a `fetchMock` va a devolver el mismo valor ya que utilizamod `mockReturnValue`.
- En muchos casos les va a tocar tener que hacer un mock de los valores retornados por alguna función y podemos utilizar `jest.fn` para eso.

### Mockear módulos

- `jest` también nos permite hacer mocks de módulos.
- Axios es un módulo que se utiliza para manejar la comunicación con el servidor y es una buena alternativa a usar `fetch`.
- Supongmos que nuestro código usa `axios` y no queremos que el test haga el llamado real sino que podamos crear un mock y así evitar el llamado real.

```javascript
// modulo.js
import axios from "axios";

class Users {
  static all() {
    console.log(axios);
    return axios.get("/users.json").then((resp) => resp.data);
  }
}

export default Users;

// test

import axios from "axios";
import Users from "./modulo.js";

jest.mock("axios");

test("Axios mock function", () => {
  const users = [{ name: "Bob" }];
  const resp = { data: users };
  axios.get.mockResolvedValue(resp);

  return Users.all().then((data) => {
    expect(data).toEqual(users);
  });
});
```

- El sitio de `jest` nos da este ejemplo que está muy bueno para explicar / simular como funciona un mock de una API.
- En este caso se la clase `Users` usa `axios.get` para llamar a una API y obtener datos.
- Cuando el código se ejecuta en la aplicación, `axios` hace el llamado real y obtiene los datos.
- Como estamos en un test no queremos ejecutar el llamado de la API y entonces tenemos que `simular o mockear` la respuesta.
- `jest.mock` nos permite mockear un módulo pasandole como parámetro el nombre del módulo que queremos mockar.
- Cuando corre el test, en lugar de llamar a `axios.get` llama al mock y podemos configurar cual es el valor de retorno.
- De esta forma podemos ejecutar el test y siempre obtener el mismo resultado sin tener que depender del llamado real.
- La idea no es mockear todas las cosas porque sino el test no es real pero si algunos servicios como puede ser este caso.
- En algúnas oportunidades queremos o necesitamos hacer `mock` de un módulo pero sólo de alguna parte y después utilizar el código real del mismo.
- Para esto podemos hacer un `mock parcial` donde una parte es un mock y el resto usa el código real.

```javascript
// modulo.js
export const nombre = "Nicolas";
export const mostarEdad = () => 45;
export default () => nombre;

// test
import defaultExport, { nombre, mostrarEdad } from "./modulo.js";

jest.mock("./modulo.js", () => {
  const codigoModuloOriginal = jest.requireActual("./modulo.js");

  return {
    __esModule: true,
    ...codigoModuloOriginal,
    default: jest.fn(() => "valor del mock"),
    mostrarEdad: jest.fn(() => "30, soy más joven"),
  };
});

test("should do a partial mock", () => {
  const defaultExportResult = defaultExport();
  expect(defaultExportResult).toBe("valor del mock");
  expect(defaultExport).toHaveBeenCalled();

  expect(nombre).toBe("Nicolas");
  expect(mostrarEdad()).toBe("30, soy más joven");
});
```

- En este ejemplo vemos como podemos importar un modulo y hacer mock de solo una parte.
- Usando `jest.mock()` podemos pasar el path o nombre del módulo que queremos mockear como primer parámetro y luego un callback donde podemos devolver cualquier valor que nosotros necesitamos.
- Usando `jest.requireActual("./modulo.js")` le pedimos a `jest` que traiga el código real del módulo.
- Luego el callback devuelve un objeto como haría el módulo real.
- `__esModule: true` es necesario como parte del valor retornado.
- `...codigoModuloOriginal` usa destructuring para poner en el nuevo objeto (a retornar) con el código real del módulo.
- `default: jest.fn(() => "valor del mock"),` en este caso usando `default` podemos mockear el valor que venía del `export default`. En este caso le asignamos una `jest.fn()` para lugo poder mockear otros valores.
- `mostrarEdad: jest.fn(() => "30, soy más joven")` en esta linea mockeamos la función `mostrarEdad` que está definida en el módulo.
- De esta forma dejamos sólo la variable nombre como parte original del módulo para demostrar que sigue siendo `Nicolas`.

> Lo único que queda ahora es.. testear el código de tus ejercicios!

![proud](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExY241YWh6dWRmbWs0cGRyNHN0YTcwemxhcDdsMjV0eGRwZjduNHhsNiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/fdyZ3qI0GVZC0/giphy.gif)
