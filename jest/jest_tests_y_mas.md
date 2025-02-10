# Jest

## Jest Tests y Más!

- Escribir código es una de las tareas que más hacemos como programadores pero también necesita demostrar que nuestro código funciona como se espera.
- Podemos escribir tests que nos ayuden a demostrar que nuestro código hace lo que tiene que hacer.
- Por ejemplo, podemos programar una función que acepta unos parámetros y luego tiene que hacer algo.
- Utilizando tests unitarios podemos testear que la función hace lo que se espera.
- En el ecosistema de JavaScript existe una herramienta llamada `Jest` que nos permite crear y ejecutar tests.
- Puedes aprender más sobre `jest` en el [Sitio Oficial](https://jestjs.io)
- Para poder utilizar `Jest` debemos instalar algunos módulos y configurar como lo vamos a utilizar.
- En nuestro caso como ya tenemos bastante código escrito, podemos utilizar Jest para testear nuestro código y de paso aprender a usarlo.

## Instalar y usar Jest

- En el repo donde tengas los ejercicios de JavaScript vamos a installar y configurar `Jest` para poder crear tests para algunos de nuestros ejercicios.
- Lo primero que tenemos que hacer es instalar el módulo `jest` utilizando `npm`

```bash
$ npm install --save-dev jest
```

- En este momento deberías tener una carpeta llamada `node_modules`, un archivo `package.json` y otro `package-lock.json`.
- `node_modules` es una carpeta donde `node` instala todas las dependencias de nuestro proyecto.
- Dado que las dependencias pueden pesar mucho es mejor agregar un `.gitignore` con el el contenido `node_modules` para evitar commitear esta carpeta.
- Si en algún momento necesitas instalar los módulos lo podes hacer usando `npm install`.
- Una vez instalado `jest` debemos agregar la siguiente configuración al archivo `package.json`.

```json
{
  "scripts": {
    "test": "jest"
  },
  "devDependencies": {
    "@babel/core": "^7.26.8",
    "@babel/preset-env": "^7.26.8",
    "babel-jest": "^29.7.0",
    "jest": "^29.7.0"
  }
}
```

- En este caso estamos agregando un script a nuestro package.json que luego podemos llamar desde la consola para correr `jest` en los tests
- El próximo paso es crear un proyecto / configuración para `jest` y lo podemos hacer ejecutando el siguiente comando:

```bash
$ npm init jest@latest
```

- Este comando va a preguntar algunas cosas para poder configurar el proyecto
- Por ahora podemos seleccionar las siguientes respuestas:

```bash
1) Would you like to use Typescript for the configuration file? › (y/N)
n

2) Choose the test environment that will be used for testing?
node

3) Do you want Jest to add coverage reports?
n

4) Which provider should be used to instrument code for coverage?
babel

5) Automatically clear mock calls, instances, contexts and results before every test?
n
```

- Si todo el proceso se ejecutó correctamente deberías tener un archivo con el nombre de `jest.config.js`.
- Este archivo permite configurar como funciona `jest` en nuestro proyecto
- Puedes encontrar todas las opciones de configuración en la [documentación de configuración de Jest](https://jestjs.io/docs/configuration)
- Dado que vamos a utilizar imports y `jest` no sabe como manejarlos debemos instalar otra herramienta llamada `Babel`.
- Babel es un transpilador de JavaScript que permite agregar algunas funcionalidades a nuestro proyecto como utilizar `next-gen` JavaScript en el proyecto y mucho más.
- Podes aprender más sobre Babel en el [Sitio Oficial](https://babeljs.io)
- Para instalar `Babel` y configurar `jest` para utilizarlo instalamos los siguientes módulos:

```bash
$ npm install --save-dev babel-jest @babel/core @babel/preset-env
```

- Luego de instalar `Babel` debemos configurarlo creando el archivo de configuración llamado `babel.config.js`
- También tenemos que agregar la configuración inicial:

```javascript
module.exports = {
  presets: [["@babel/preset-env", { targets: { node: "current" } }]],
};
```

- En esta configuración vemos que es un archivo JavaScritp que exporta un objeto con presets y otros valores que necesita Babel y jest para trabajar juntos.
- Ahora solo nos queda crear nuestro primer test y correrlo.
- Crea un archivo con el nombre `ejemplo.spec.js` con el siguiente código:

```javascript
describe("Nuestro primer test", () => {
  it("Comprobamos que nos gusta JavaScript y escribir tests", () => {
    const meGustaJavaScript = true;
    expect(meGustaJavaScript).toBe(true);
  });
});
```

- Una vez creado el primer test podemos correrlo de la siguiente manera:

```bash
$ npm test ejemplo.spec.js
```

- Si todo va bien deverías ver los siguientes mensajes de salida:

```bash
> test
> jest ejemplo.spec.js

 PASS  ./ejemplo.spec.js
  Nuestro primer test
    ✓ Comprobamos que nos gusta JavaScript y escribir tests (2 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.286 s
Ran all test suites matching /ejemplo.spec.js/i.
```

- Felicitaciones!! escribiste tu primer TEST!!!!

![Festejo](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExZHl1Mzhia25udDE3M3I5MmRzZGZ0cjA3ZDhjeHYwbnU2djNlNDJsMCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/humidv0MqqdO5ZoYhn/giphy.gif)
