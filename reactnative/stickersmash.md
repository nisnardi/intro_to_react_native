# React Native

- Esta sección del curso está basada en el [tutorial StickerSmash de la documentación de Expo](https://docs.expo.dev/tutorial/introduction/).
- Al completarlo nos va a dar una mejor idea de como utilizar algunas funcionalidades de `Expo` y `React Native`.
- Todas las imágenes y videos que vas a ver son propiedad de Expo (por las dudas).

## StickerSmash - Tutorial: Using React Native and Expo

- Estamos a punto de embarcarnos en un viaje donde construiremos una aplicacion universales.
- En este tutorial, vamos a crear una aplicación Expo que se ejecuta en `Android, iOS y web`; todo con el mismo código.

### Sobre el tutorial de React Native y Expo

- El objetivo de este tutorial es tener un conocimiento básico de Expo y familiarizarse con el SDK.
- Cubre los siguientes temas:
  - Crear una aplicación utilizando el template por defecto con TypeScript habilitado.
  - Implementar un diseño de tabs en dos pantallas utilizando [Expo Router](https://docs.expo.dev/router/introduction).
  - Descomponer el diseño de la aplicación e implementarlo con flexbox.
  - Utilizar la IU del sistema de cada plataforma para seleccionar una imagen de la biblioteca multimedia.
  - Crear un modal de stickers utilizando los componentes <Modal> y <FlatList> de React Native.
  - Añadir gesture táctiles para interactuar con un sticker.
  - Utilizar módulos de terceros para capturar una pantalla y guardarla en el disco.
  - Manejar las diferencias entre Android, iOS y Web.
  - Por último, pasar por el proceso de configuración de una barra de estado, una pantalla de bienvenida, y un icono para completar la aplicación.
- Estos temas proporcionan una base para aprender los fundamentos creando una aplicación Expo.
- Este tutorial está dividido en nueve capítulos.
- Cada capítulo contiene el código necesarios para completar los pasos, así que puedes seguirlo creando una aplicación desde cero.
- Antes de empezar, echa un vistazo a lo que vamos a construir. Es una aplicación llamada [StickerSmash que funciona en Android, iOS y la web](https://docs.expo.dev/static/videos/tutorial/final.mp4)

### Crear la app

- Usamos `create-expo-app` para crear una nueva Expo app con el nombre `StickerSmash`

```bash
npx create-expo-app@latest StickerSmash && cd StickerSmash
```

- Este template tiene el código esencial y las librerías necesarias para construir nuestra aplicación, incluyendo Expo Router.
- Ventajas de utilizar el template por defecto:
  - Crea un nuevo proyecto React Native con el paquete expo instalado.
  - Incluye herramientas recomendadas como Expo CLI.
  - Incluye un navegador de Tabs de Expo Router.
  - Configurado automáticamente para ejecutar un proyecto en múltiples plataformas: `Android, iOS y web`.
  - TypeScript viene configurado por defecto.
- También necesitamos resetear el proyecto para sacar todo el código inicial que agrega Expo como demo.

```bash
npm run reset-project
```

- [Descarga los assets](../assets/react-native/sticker-smash-assets.zip) iniciales que vamos a utilizar a lo largo del tutorial.
- Una vez descargado el archivo tenes que descomprimirlo y reemplazar los archivos en el directorio que utiliza Expo por defecto `/assets/images`.

#### Correr el proyecto en dispositibos móbiles y web

- En el directorio del proyecto, ejecuta el siguiente comando para iniciar el servidor de desarrollo desde el terminal

```bash
npx expo start
```

- Después de ejecutar el comando se iniciará el servidor de desarrollo y verás un código QR dentro de la terminal.
- Escaneá ese código QR para abrir la aplicación en el dispositivo.
  - En Android, utiliza la opción `Expo Go > Escanear código QR`.
  - En iOS, utiliza la aplicación de cámara predeterminada.
  - Para ejecutar la aplicación Web, pulsa `w` en el terminal. Se abrirá la aplicación web en el navegador web predeterminado.
- Una vez ejecutada en todas las plataformas, la aplicación se debería ver así:

![Todas las plataformas](../assets/react-native/01-app-running-on-all-platforms.png)

#### Editar la pantalla de index

- El archivo `app/index.tsx` define el texto que se muestra en la pantalla de la app.
- Es el `punto de entrada de nuestra app` y se ejecuta cuando se inicia el servidor de desarrollo.
- Utiliza componentes de React Native como <View> y <Text> para mostrar el fondo y el texto.
- Los estilos aplicados a estos componentes utilizan objetos JavaScript en lugar de CSS, que se utiliza en la web. Sin embargo, muchas de las propiedades te resultarán familiares si ya has usado CSS en web.
- La mayoría de los componentes de React Native aceptan una propiedad de estilo que acepta un objeto JavaScript como valor.
- Vamos a modificar la pantalla `app/index.tsx`:

  - Importar `StyleSheet` de react-native y crear un objeto styles para definir nuestros estilos personalizados.
  - Durante este tutorial si decimos que agregamos un estilo tipo `styles.container.backgroundColor` significa que vamos a crear una variable con el nombre `styles` y le vamos a crear una propiedad con el nombre `container` y le asignamos la propiedad `backgroundColor` con el valor que describa. Esto luego se utiliza en el componente como `<Componente style={styles.container}>`.
  - Agregamos una propiedad `styles.container.backgroundColor` a <View> con el valor `#25292e`. Esto cambia el color de fondo.
  - Cambiá el valor por defecto de <Text> por `Home screen`.
  - Agregamos una propiedad `styles.text.color` a <Text> con el valor `#fff` (blanco) para cambiar el color del texto.

```javascript
import { Text, View, StyleSheet } from "react-native";

export default function Index() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Home screen</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e",
    alignItems: "center",
    justifyContent: "center",
  },
  text: {
    color: "#fff",
  },
});
```

- React Native utiliza el mismo formato de color que la web.
- Admite colores hexadecimales, rgba, hsl y colores con nombre, como red, green, blue, peru y papayawhip.Para más información, consulta [Colores en React Native](https://reactnative.dev/docs/colors).
- Estos cambios se reflejan automáticamente en todas las plataformas.

![cambios](../assets/react-native/02-index-screen-changes.png)

### Agregar navegación

- En este sección vamos a aprender los fundamentos de Expo Router para crear una navegación `Stack` y una barra inferior con dos Tabs.
