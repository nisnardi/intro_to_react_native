# Configuración de Javascript en Mac

Para configurar el entorno de desarrollo de JavaScript con Visual Studio Code en una Mac o Windows, siga los siguientes pasos:

### 1. Instalar Visual Studio Code

Visual Studio Code (VS Code) es un ligero pero potente editor de código fuente que se ejecuta en su escritorio y está disponible para Windows, macOS y Linux.

#### Pasos para la instalación:

- Vaya a la [página de descarga de Visual Studio Code](https://code.visualstudio.com/Download).
- Selecciona la versión para su sistema operativo.
- `Mac`: Una vez finalizada la descarga, abre el archivo `.zip` y arrastra la aplicación Visual Studio Code a la carpeta Aplicaciones. Se instalará en tu Mac.
- `Windows`: Siga todos los pasos del instalarlo.

### 2. Configurar Visual Studio Code para JavaScript

VS Code tiene soporte para JavaScript, pero con algunos ajustes se puede mejorar la configuración y así tu experiencia al programar.

#### Mejorar IntelliSense

IntelliSense proporciona ayuda basada en tipos de variables, definiciones de funciones y módulos importados.

- Abra VS Code.
- Vaya a `Code` > `Settings` > `Settings`.
- Busque "JavaScript" y explore las opciones disponibles para personalizar el comportamiento de JavaScript, como activar la opción "Suggest: Enabled" en “JavaScript”.

#### Instalar Node.js

Node.js es crucial para ejecutar JavaScript para scripts del lado del servidor o desarrollar aplicaciones de servidor.

- Descargue e instale Node.js desde [nodejs.org](https://nodejs.org/).
- Mac: Durante la instalación, permita que el instalador añada Node.js a la ruta de su sistema para que VS Code pueda detectarlo.
- Windows: Durante la instalación, asegúrate de marcar la casilla que dice `Añadir a PATH`.
- Reinicie VS Code tras la instalación para asegurarse de que reconoce Node.js.

### 3. Instale las extensiones necesarias

Mejore su desarrollo con las extensiones de VS Code.

Para instalar extensiones:

- Haga clic en el icono de la vista Extensiones en la barra lateral o pulse `Cmd+Shift+X`.
- Busque e instale las siguientes extensiones útiles:
  - **ESLint**: Para JavaScript linting.
  - **Prettier - Formateador de código**: Para formatear código.
  - **JavaScript (ES6) code snippets**: Para fragmentos de código JavaScript.

### 4. Crear un nuevo proyecto JavaScript

- Abra VS Code.
- Seleccione `File` > `New File`.
- Guarde el archivo con la extensión `.js` para identificarlo como un archivo JavaScript.
- Para crear un proyecto más estructurado, puede seleccionar `Archivo` > `Nueva Carpeta` para crear una nueva carpeta de proyecto y guardar su archivo `.js` dentro de esta carpeta.

### 5. Configure el entorno de su proyec

Si estás trabajando en una aplicación Web o necesitas un servidor:

- Abre la terminal en VS Code seleccionando `Terminal` > `New Terminal`.
- Navega a la carpeta de tu proyecto y configura un servidor Web u otras dependencias ejecutando comandos como `npm init` o `npm install`.

### 6. Escriba y ejecute su primer código JavaScript

- Escriba su código JavaScript en el archivo `.js` que ha creado. Por ejemplo
  ```javascript
  console.log("Hello, JavaScript in VS Code!");
  ```
- Para ejecutar tu código, utiliza el terminal integrado en VS Code. Escriba `node <yourfilename>.js` y pulse Enter.

### 7. Depuración de JavaScript

- Establece puntos de interrupción pulsando a la izquierda del número de línea donde quieres que se detenga el código.
- Abra la barra lateral de depuración haciendo clic en el icono Ejecutar y depurar o pulsando `Cmd+Shift+D`, y luego haga clic en «Ejecutar y depurar» para iniciar la depuración

### 8. Mantener todo actualizado

Mantenga VS Code y extensiones actualizadas para acceder a las últimas características:

- VS Code le avisa cuando hay actualizaciones disponibles. También puede comprobar si hay actualizaciones yendo a `Code` > `Check for Updates`.
- Para las extensiones, vaya a la vista Extensiones y haga clic en `Extensions` > `...` > `Check for Updates`.

Esta guía le ayudará a configurar un completo entorno de desarrollo JavaScript en VSt Code en macOS, adaptado para crear cualquier cosa, desde scripts sencillos hasta aplicaciones complejas
