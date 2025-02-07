# TypeScript

## Instalar y utilizar TS

- Para poder utilizar TypeScript debemos instalar un módulo que nos permite usar el compilador.
- Node.js junto con `npm` nos permite instalar modulos de manera local o global.
- Dado que vamos a utilizar TypeScript en varios proyectos tiene sentido hacerlo de manera global.
- Para instalar un modulo utilizando `npm` tenemos que escribir en la consola `npm install nombre_del_modulo`.
- Para hacerlo de manera global utilizamos `-g` luego del `install`.
- Para instalar TypeScript tenemos que ejecutar: `npm install -g typescript`.
- TypeScript utiliza archivos con la extensión `.ts` en lugar de `.js`.
- Una vez instalado TypeScript deberíamos poder ejecutar el comando `tsc` desde la consola para compilar un archivo `.ts` a uno de `.js`.

```bash
tsc archivo.ts
```

- Al ejecutar un archivo `.ts` TypeScript va a comprobar los errores y mostrarlos en la consola.
- Si todo sale bien va a generar el nuevo archivo `.js`
- Los motores de JavaScript saben interpretar JavaScript y no TypeScript, es por eso que necesitamos este proceso.

## Ejemplo:

- Crear un archivo `index.ts` con el siguiente código (salvar el código):

```javascript
function sumar(numero1: number, numero2: number) {
  return numero1 + numero2;
}

sumar("uno", "dos");
sumar("1", "2");
```

- Luego ejecutar el comando `tsc` desde la consola utilizando el archivo `index.ts`.

```bash
tsc index.ts
```

- Al ejecutarlo deberíamos obtener el siguiente mensaje de error:

```bash
index.ts:5:7 - error TS2345: Argument of type 'string' is not assignable to parameter of type 'number'.
5 sumar("uno", "dos");
        ~~~~~
index.ts:6:7 - error TS2345: Argument of type 'string' is not assignable to parameter of type 'number'.
6 sumar("1", "2");
        ~~~
Found 2 errors in the same file, starting at: index.ts:5
```

- TypeScript nos está comunicando que nuestro archivo tiene 2 errores de tipos.
- Nos dice que no se puede utilizar un tipo de dato `string` donde se espera un tipo de dato `number`.

- Ahora debemos arreglar este error por medio de llamar a la función con los parámetros correctos (utilizar números).

```typescript
function sumar(numero1: number, numero2: number) {
  return numero1 + numero2;
}

sumar(10, 20);
```

- Ejecutar nuevamente `tsc index.tsc` y ver el resultado.
- Vemos que en consola no sale ningún mensaje porque corrió con éxito.
- Ahora tenemos un nuevo archivo con el nombre `index.js`.
- El código de index.js es:

```javascript
function sumar(numero1, numero2) {
  return numero1 + numero2;
}

sumar(1, 2);
```

- Podemos ver cómo TypeScript removió los tipos numéricos de la definición de parámetros de la función sumar.
- El código final es JavaScript puro y no hay ninguna referencia a TypeScript.
- Si queremos ejecutar `node` tenemos que utilizar el archivo `.js` y no el `.ts`.
- Vamos a utilizar TypeScript para nuestros proyectos y el resultado final va a ser JavaScript.
