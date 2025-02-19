# React Native

## Intro

- [React Native](https://reactnative.dev/): Aprende una vez, escribe en cualquier lugar (Learn once, write anywhere).
- React Native recomienda utilizar Expo para crear aplicaciones de manera más fácil.
- [Expo es un Framework](https://expo.dev/) que nos da muchas herramientas como:
  - Expo-router: Navegador basado en archivos.
  - Crear aplicaciones universales que corran en iOS, Android y Web al mismo tiempo.
  - Crear módulos nativos para comunicar el mundo de JS y Nativo.
  - Módulos que podemos utilizar para simplificar nuestra experiencia al crear aplicaciones.
- Durante este curso vamos a aprender sobre Expo y todos sus beneficios.

## Crear un proyecto usando Expo

- Para crear un proyecto nuevo con Expo corremos el siguiente comando:

```bash
$ npx create-expo-app@latest nombre_de_la_nueva_app
```

- Después de unos minutos Expo instaló todo lo necesario para tener un nuevo proyecto.
- Vemos en pantalla un mensaje como este:

```bash
✅ Your project is ready!

To run your project, navigate to the directory and run one of the following npm commands.

- cd nombre_de_la_nueva_app
- npm run android
- npm run ios
- npm run web
```

- Luego de crear el proyecto necesitamos ingresar a la carpeta donde el proyecto fué creado `cd nombre_de_la_nueva_app`.
- `npm run` permite utilizar android, ios, web para correr el proyecto en uno de esos dispositivos o browser.
- Con Expo podemos utilizar otro comando para correr nuestro proyecto `npx expo`.

```bash
 Metro waiting on exp://10.0.0.107:8081
› Scan the QR code above with Expo Go (Android) or the Camera app (iOS)

› Web is waiting on http://localhost:8081

› Using Expo Go
› Press s │ switch to development build

› Press a │ open Android
› Press i │ open iOS simulator
› Press w │ open web

› Press j │ open debugger
› Press r │ reload app
› Press m │ toggle menu
› shift+m │ more tools
› Press o │ open project code in your editor

› Press ? │ show all commands
```

- Expo nos da dos opciones a la hora de correr nuestro proyecto, `Development build` y `Expo Go`.
- Development build crea las carpetas del proyecto nativo para Android y iOS que luego podemos abrir y correr en Android Studio o Xcode.
- Expo Go es una aplicación creada por Expo parar ejecutar aplicaciones que fueron cradas con Expo de manera fácil.
- Expo Go se instala en el simulador / emulador para correr las apps localmente en nuestra computadora.
- También podemos instalar Expo Go en un dispositivo móbil utilizando la cámara y el código QR.
- Expo Go es una buena herramienta pero no nos permite hacer todo lo que por ahí necesitamos.
- Correr la aplicación en un dispositivo móvil siempre es lo mejor y más cercano a la experiencia real.
- Por ejemplo si queremos utilizar la cámara de un dispositivo, es mejor utilizar el dispositivo y no un simulador / emulador.
- El proyecto en `development build` nos da acceso a todo porque son las aplicaciones nativas pero también tenemos que instalar más cosas para compilar el proyecto, correrlo y abrirlo.
- Podemos decir que Expo nos da maneras más flexibles de crear / ejecutar aplicaciones y también obtener la versión nativa de ser necesario.
- Para facilitar el curso vamos a utilizar Expo Go para la mayoría de los ejercicios.
- También podemos utilizar los dispositivos para otro tipo de experiencia.
- Para correr la app en Expo Go podemos utilizar alguna de las siguientes opciones:
  - Apretar `a` para abrir el emulador de Android con Expo Go y nuestra app.
  - Apretar `i` para abrir el simulador de iOS con Expo Go y nuestra app.
  - Apretar `w` para abrir un browser nuestra app. (No todo lo de React Native va a funcionar en web sin configuración previa)
- También podemos apretar `r` para recargar la app.
- Apretando `m` abrimos la consola de Expo en el dispositivo.
- Otra opción es apretar `SHIFT + m` para más herramientas.
- Con `j` podemos abrir las herramientas de debug.

### Obtener un proyecto limpio

- Expo inicialmente nos da un proyecto con algunos ejemplos y documentación.
- A la hora de trabajar necesitamos resetear el proyecto para tener una versión más limpia inicialmente.
- Para resetear el proyecto podemos correr el comando `npm run reset-project`.
- Nos va a preguntar si queremos mover los archivos a una nueva carpeta como backup o si queremos borrarlos.
- Por ahora podemos borrarlos ya que no los necesitamos.

```bash
npm run reset-project

> react_native_basics@1.0.0 reset-project
> node ./scripts/reset-project.js

Do you want to move existing files to /app-example instead of deleting them? (Y/n):
n
```

- Presionando `n` borra los archivos y nos deja el proyecto con configuración inicial pero el resto limpio para nuestra app.
- Si todo va bien deberíamos ver el siguiente mensaje:

```bash
❌ /app deleted.
❌ /components deleted.
❌ /hooks deleted.
❌ /constants deleted.
❌ /scripts deleted.

📁 New /app directory created.
📄 app/index.tsx created.
📄 app/_layout.tsx created.

✅ Project reset complete. Next steps:
1. Run `npx expo start` to start a development server.
2. Edit app/index.tsx to edit the main screen.
```

- En este mensaje vemos que Expo creo una carpeta `app/` con los archivos `index.tsx` y `_layout.tsx`.
- La carpeta `app` es donde van a estar nuestras pantallas.
- `index.tsx` es el archivo inicial que Expo abre al ejecutar una aplicación, podemos pensarlo como la pantalla `Home`.
- `_layout.tsx` es un archivo que `expo-router` utiliza para configurar las rutas.
- Vamos a ver que tiene el archivo `index.tsx` abriendolo en VS Code.

```javascript
import { Text, View } from "react-native";

export default function Index() {
  return (
    <View
      style={{
        flex: 1,
        justifyContent: "center",
        alignItems: "center",
      }}
    >
      <Text>Edit app/index.tsx to edit this screen.</Text>
    </View>
  );
}
```

- Con lo que aprendimos hasta ahora podemos identificar las siguientes cosas:
  - Hay un `import` que importa 2 valores: `Text y View` del módulo `react-native`.
  - Utiliza `export default` para exportar una función con el nombre `Index`.
  - Nos llama la atención el nombre de la función porque está en mayúscula como si fuera una clase.
  - La función retorna o devuelve algo raro.
  - <View> es lo que se conoce como un componente de React Native.
  - <Text> es otro componente básico de React Native que permite mostrar texto en pantalla.
  - El `<View>` usa un objeto de JavaScript con propiedades `flex: 1, justifyContent: "center", alignItems: "center",`.
- Bien, sabemos muchas cosas sobre este archivo!
- Podemos modificar el texto dentro de `<Text></Text>` parar ver que pasa al salvar.
- Modificar el texto `Edit app/index.tsx to edit this screen.` por `Bienvenidos a React Native`.
- Si todo salió bien deverías ver un mensaje `Bienvenidos a React Native` en el simulador / emulador.
- No te olvides de presionar `a` o `i` para correr el proyecto en el emulador de Android o simulador de iOS.

### Alternativa para crear un proyecto con Expo

- Expo nos permite utilizar diferentes templates a la hora de crear un nuevo proyecto.

```bash
$ npx create-expo-app --example
```

- Cada template define una configuración inicial diferente.
- Cuando llamamos sólo a `npx create-expo-app@latest` utiliza el template por defecto.
- El template `blank` por ejemplo nos da un proyecto sin mucha configuración para que nosotros podamos elegir que queremos utilizar.
- Hay otras opciones como `navigation` para cambiar el navegador utilizado (Expo usa expo-router por defecto), with-apollo para usar GraphQL, with-auth0 para autenticación y mucho más.
- En general podemos configuar todo esto nosotros mismos en nuestros proyectos pero los templates nos ayudan a empezar un proyecto.

```bash
➜  intro_to_react_native git:(main) npx create-expo-app@latest --example
? Choose an example: › - Use arrow-keys. Return to submit.
❯   blank
  navigation
  stickersmash
  with-apollo
  with-auth0
  with-aws-storage-upload
  with-camera
  with-canary-new-arch-tv
  with-canary-new-arch
↓ with-canary-react-19
```

- Para crear un proyecto nuevo utilizando templates corremos el siguiente comando.

```bash
$ npx create-expo-app --template blank
```

- Ahora a crear y aprender!

![Mobile](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExOHVzeXVremVqcHNpdTkzaGQ0cWJnd2x0M2lyOWo2MnYyZjlwbXVyNiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/8kdQGAkiCBQXd1cZ2W/giphy.gif)
