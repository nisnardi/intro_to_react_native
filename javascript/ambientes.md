# JavaScript - Ambientes

Como sabemos lo más común es correr este lenguaje en el browser, hacer páginas web o una app mobile. Esto cambió cuando salió Node.js

## Node.js

[Node.js](https://nodejs.org/es/) Es una aplicación que permite ejecutar ECMAScript fuera del browser. Esto quiere decir que nos da la posibilidad de crear más tipo de aplicaciones y fué creado por [Ryan Dahl](https://es.wikipedia.org/wiki/Node.js) en el año 2009.

Durante esta etapa del curso vamos a utilizar esta herramienta para aprender los fundamentos del lenguaje y ver una introducción a la programación sin tener que utilizar el browser por el momento.

Para utilizar Node.js debemos tenerlo instalado, abrir una consola y correr el comando node.

```bash
node
```

Vemos que al ejecutar este comando parece que no pasa nada pero en realidad si miramos bien en la consola vamos a ver algo similar a:

```bash
node
>
```

Cuando vemos el símbolo **>** significa que abrimos la consola de Node.js llamada REPL que nos permite escribir código en ECMAScript y ver el resultado.

### Usando la consola de Node.js

Vamos a ejecutar una operación sumando dos valores:

- Abrir la consola
- Ejecutar el comando node
- Cuando veas el símbolo **>** escribir la siguiente sentencia

```javascript
2 + 2;
```

- Presiona la tecla enter y deberías ver el siguiente resultado:

```javascript
> 2+2
4
>
```

- Presiona una vez las teclas CTRL + C y deberías ver el siguiente mensaje:

```bash
(To exit, press ^C again or type .exit)
```

- Presiona de nuevo las teclas CTRL + C para finalmente salir y ver la consola de tu sistema operativo en lugar de la de Node.js (no deberías ver más el símbolo >)

En este ejercicio lo que hicimos fue ejecutar una sentencia de ECMAScript en la consola de Node.js y como sabe interpretar este código nos pudo mostrar el resultado (4).

Si bien está muy bueno poder programar en la consola de Node.js podemos decir que no es muy práctico.

Existe otra forma de ejecutar nuestro código de ECMAScript en Node.js y es por medio del uso de un archivo externo de la siguiente manera:

```bash
node progama.js
```

Al ejecutar este comando Node.js lee e interpreta el código ECMAScript que esta en el archivo llamado programa.js. Utilizamos la extensión `.js` para los archivos que estén programados en JavaScript / ECMAScript (ejemplo: ejercicio1.js, alumnos.js, etc).

### Usando Node.js con un archivo

- Crear una carpeta llamada js
- Crear un archivo de texto llamado `programa.js` dentro de la carpeta `js`
- Escribir el siguiente código dentro del archivo `programa.js` y salvarlo

```javascript
2 + 2;
```

- Abrir la consola y posicionarse dentro de la carpeta `js`
- Ejecutar el siguiente comando

```bash
node progama.js
```

- Ver el resultado

Al ejecutar este programa no vemos ningún resultado y eso se debe a que Node.js está ejecutando la suma y no estamos mostrando el resultado en ningún lado. Podemos utilizar `console.log(valor a mostrar en consola)` para mostrar un valor en la consola. Modifiquemos el código del archivo `programa.js` para que se vea de la siguiente manera:

```js
console.log(2 + 2);
```

- Volvemos a ejecutar el siguiente comando:

```bash
node progama.js
```

- Si todo sale bien podemos ver el resultado esperado

### Usando la consola del Browser

- Abrir Chrome
- Abrir devtools
- Seleccionar el tab console dentro del devtools (es como la consola de Node.js pero dentro del browser)

![Devtools](../assets/js/mostrar_devtools.png)

- Escribir el siguiente código en la consola del devtools:

```javascript
2 + 2;
```

```js
console.log(2 + 2);
```

![Devtools](../assets/js/devtools.png)

- Utilizando la consola del browser obtenemos el mismo resultado que en Node.js.
- Tanto Chrome como Node.js utilizan el mismo motor de JavaScript que se llama V8 y es mantenido por un equipo de Google.
- Podemos utilizar JavaScript tanto en el browser como con Node.js
