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

#### Conceptos básicos de Expo Router

- Expo Router es un framework de navegación basado en archivos para construir aplicaciones Universales (iOS, Android, Web).
- Gestiona la navegación entre pantallas y utiliza los mismos componentes en múltiples plataformas.
- Para empezar, necesitamos conocer las siguientes convenciones:
  - `Directorio app`: Es un directorio especial que contiene sólo rutas (Pantallas) y sus diseños. Cualquier archivo añadido a este directorio se convierte en una pantalla dentro de nuestra app nativa y en una página en la web.
  - `Layout raíz`: El archivo `app/_layout.tsx`. define los elementos compartidos de la UI, como los headers y los Tabs, para que sean coherentes entre las distintas rutas.
  - `Convención de nombres de archivo`: Los nombres de archivos de `index`, como `index.tsx`, coinciden con su directorio principal y no añaden un segmento de ruta.
    - Por ejemplo, si tenemos `app/index.tsx` expo router toma indes como raiz de la ruta como en web sería `/`.
    - Si tenemos una carpeta `app/usuario/index.ts` esta ruta se transforma en `usuario/` ya que index es la raíz de esta carpeta y es la pantalla principal.
  - `Rutas`: Un archivo de ruta exporta un componente React como valor predeterminado. Puede utilizar la extensión .js, .jsx, .ts o .tsx.
  - Android, iOS y la web comparten una estructura de navegación unificada.

#### Agregar una nueva pantalla Stack

- Vamos a crear un nuevo archivo nuevo llamado `about.tsx` dentro de la carpeta `app`. Muestra el nombre de la pantalla cuando el usuario navega a la ruta `/about`.

```javascript
// app/about.tsx
import { Text, View, StyleSheet } from "react-native";

export default function AboutScreen() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>About screen</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e",
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    color: "#fff",
  },
});
```

- Expo router puede detectar que hay un archivo nuevo dentro de `app` y con eso sabe que hay una ruta nueva.
- Igual vamos a modificar el archivo `app/_layout.tsx` para establecer con un componente que hay una nueva ruta.
- Cuando apenas creamos la aplicación expo en su template tiene que `_layout.tsx` sólo tiene un componente `<Stack/>`.
- Ahora tenemos que agregar la definición para `index` y para `about`.
- Hacer los siguientes cambios en el archivo `_layout.tsx`:
  - Vamos a agregar dentro de `<Stack> </Stack>` dos nuevos componentes que son del tipo `<Stack.Screen />`.
  - Este componente tiene una propiedad `name` que acepta un string con el nombre de la ruta. En este caso es el mismo que los archivos `index y about`.
  - Agregamos a cada componente una propiedad `options` que acepta como valor un objeto de configuración.
  - El objeto de configuración tiene una propiedad `title` que acepta un string para definit el título de cada pantalla en lugar de mostrar el nombre del archivo.
  - Establecemos a cada componente su título utilizando `options={{title: ''}}` y asignando el valor `Home` para la ruta index y `About` para `about`.

```javascript
import { Stack } from "expo-router";

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="index" options={{ title: "Home" }} />
      <Stack.Screen name="about" options={{ title: "About" }} />
    </Stack>
  );
}
```

- `¿Qué es Stack?` Es un tipo de navegación para navegar entre las diferentes pantallas de una app.
- En Android, una ruta Stack tiene una animación en la parte superior de la pantalla actual.
- En iOS, una ruta Stack tiene una animación de derecha hacia izquierda.
- Expo Router proporciona un componente Stack para crear una pila de navegación para añadir nuevas rutas.

#### Navegar entre pantallas

- Para navegar de una pantalla a otra podemos utilizar el componente `Link` de Expo router.
- De esta manera podemos navegar desde `index` a `about`.
- `Link` es un componente React que renderiza un <Text> con un propiedad `href` con el valor de la pantalla o ruta a la que queremos navegar.
- Importamos el componente `Link` de `expo-router` dentro de archivo `index.tsx`.
- Agrega un componente `Link` después del componente `<Text>` y le pasamos como propiedad href el valor `/about`.
- Agregamos el siguiente estilo al componente `Link`.

```javascript
 button: {
  fontSize: 20,
  textDecorationLine: 'underline',
  color: '#fff',
},
```

- El componente debe quedar de la siguiente manera:

```javascript
import { Text, View, StyleSheet } from "react-native";
import { Link } from "expo-router";

export default function Index() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Home screen</Text>
      <Link href="/about" style={styles.button}>
        Go to About screen
      </Link>
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
  button: {
    fontSize: 20,
    textDecorationLine: "underline",
    color: "#fff",
  },
});
```

- Para que la navegación funcione por ahí tenes que recargar el servidor Metro que es lo que está corriendo cuando ejecutamos `npx expo`. Puede presionar `r`.
- Presiona en el componente Link para navegar a la pantalla `/about`.

#### Agregar Ruta no encontrada

- En una app mobile es poco común que un usuario trate de navegar a una pantalla que no existe en la aplicación.
- Dado que Expo y Expo router soportan aplicaciones universales que incluyen a Web podemos crear un documento en caso de que el usuario quiera navegar a una ruta que no existe.
- Expo router utiliza el conecpto de `+not-found.tsx` que es un documento que se va a mostrar cuando la pantalla / ruta no exista.
  Expo Router utiliza un archivo especial +not-found.tsx para gestionar este caso.
- Crear un nuevo archivo `+not-found.tsx` dentro del directorio `app` y creamos un componente `NotFoundScreen`.
- Agregamos como parte del contenid un componente `Stack.Screen` con la propiedad options con el valor `{ title: 'OOpss} Not FOund`.
- Podemos agregar un componente `Link` para que el usuario pueda navegar a la pantalla `Home`.

```javascript
// app/+not-found.tsx
import { View, StyleSheet } from "react-native";
import { Link, Stack } from "expo-router";

export default function NotFoundScreen() {
  return (
    <>
      <Stack.Screen options={{ title: "Oops! Not Found" }} />
      <View style={styles.container}>
        <Link href="/" style={styles.button}>
          Go back to Home screen!
        </Link>
      </View>
    </>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e",
    justifyContent: "center",
    alignItems: "center",
  },

  button: {
    fontSize: 20,
    textDecorationLine: "underline",
    color: "#fff",
  },
});
```

- En este componente vemos como podemos utilizar `Stack.Screen` aún dentro de un componente para configurar o sobrescribir las propiedades de la pantalla. Acá estamos sobrescribiendo la propiedad `title` para mostrar otro título.
- Para probar esto lo más fácil es abrir la app en el navegador (browser) y traar de ir a una URL que no existe como: `http:localhost:8081/123`.
- La aplicación debería mostrar el componente `NotFoundScreen`.

### Agregar tabs

- En este estado, la estructura de archivos de nuestra aplicación tiene el siguiente aspecto:

```bash
/app
  |_ _layout.tsx # Root layout
  |_ index.tsx # Coincide con la ruta '/'
  |_ about.tsx # Coincide con la ruta '/about'
  |_ +not-found.tsx # Coincide con cualquier ruta que de 404
```

- Ahora vamos a agregar un sistema de navegación utilizando `Tabs` que es una barra inferior de nuestra app que permite a los usuarios presionar un botón con un icon y navegar a otra pantalla.
- Este es un patrón de navegación bastante utilizado en aplicaciones mobile.
- También vamos a seguir utilizando el sistema de navegación `Stack` para la ruta no encontrada (404).
- Dentro del directorio `app`, agregamos un subdirectorio con el nombre `(tabs)`.
- Este directorio es especial y utiliza para agrupar/mostrar rutas en un formato de barra de navegación `Tabs`.
- Creamos un archivo dentro del directorio `(tabs)` con el nombre de `_layout.tsx`.
- Este archivo se utiliza para definir el diseño de los Tabs, que es independiente del diseño de la raíz principal (`Stack`).
- Mové los archivos `index.tsx` y `about.tsx` existentes dentro del directorio `(tabs)`.
- La estructura del directorio de la aplicación será la siguiente:

```bash
/app
  |_ _layout.tsx # Root layout
  |_ +not-found.tsx # Coincide con cualquier ruta que de 404
  (tabs)
    |_ _layout.tsx # Tab layout
    |_ index.tsx # Coincide con la ruta '/'
    |_ about.tsx # Coincide con la ruta '/about'
```

- Actualizamos el archivo `_layout.tsx` principal para añadir una ruta utilizando Tabs.

```javascript
// app/_layout.tsx
import { Stack } from "expo-router";

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
      <Stack.Screen name="+not-found" />
    </Stack>
  );
}
```

- En este layout estamos especificando que hay unas rutas que utilizan `Tabs` y luego el archivo `+not-found` para las rutas que no existen en la app.
- Ahora vamos a crear el contenido del documento `app/(tabs)/_layout.tsx` para establecer cuales son las rutas que se van a mostrar en los Tabs.

```javascript
// app/(tabs)/_layout.tsx
import { Tabs } from "expo-router";

export default function TabLayout() {
  return (
    <Tabs>
      <Tabs.Screen name="index" options={{ title: "Home" }} />
      <Tabs.Screen name="about" options={{ title: "About" }} />
    </Tabs>
  );
}
```

- Reiniciamos el servidor Metro para ver el cambio realizado.
- Ahora la app debería mostrar el contenido de la pantalla `index o Home` y en la parte inferior de la pantalla 2 Tabs con el texto `Index` y `About`.
- Al presionar los `Tabs` deberían navegar a la pantalla seleccionada.
- Y así como si nada.. tenemos un sistema de navegación con Tabs.
- Expo router nos permite establecer como queremos que se vean los Tabs y sus iconos.

#### Actualizar como se ven los Tabs

- En este momento los Tabs tienen un diseño que se ve igual para todas las plataformas pero no tiene nada que ver con el diseño de nuestra app.
- Por ejemplo, la barra de Tabs o la cabecera no muestran un icono personalizado, y el color de fondo de la pestaña inferior no coincide con el color de fondo de la aplicación. Vamos a cambiarlo!
- Vamos a modificar el archivo `(tabs)/_layout.tsx` para agregar iconos a la barra de Tabs.

```javascript
import { Tabs } from "expo-router";

import Ionicons from "@expo/vector-icons/Ionicons";

export default function TabLayout() {
  return (
    <Tabs
      screenOptions={{
        tabBarActiveTintColor: "#ffd33d",
      }}
    >
      <Tabs.Screen
        name="index"
        options={{
          title: "Home",
          tabBarIcon: ({ color, focused }) => (
            <Ionicons
              name={focused ? "home-sharp" : "home-outline"}
              color={color}
              size={24}
            />
          ),
        }}
      />
      <Tabs.Screen
        name="about"
        options={{
          title: "About",
          tabBarIcon: ({ color, focused }) => (
            <Ionicons
              name={
                focused ? "information-circle" : "information-circle-outline"
              }
              color={color}
              size={24}
            />
          ),
        }}
      />
    </Tabs>
  );
}
```

- Primero tenemos que importar los iconos que queremos utilizar, en este caso vamos a usar `Ionicons` de `'@expo/vector-icons/Ionicons`.
- Luego podemos agregar la propiedad `screenOptions` del componente `Tabs` y pasarle el valor `{ tabBarActiveTintColor: '#ffd33d' }` para establecer el color del Tab que está activo.
- Para mostrar el icono debemos utilizar la propiedad `tabBarIcon` de los componentes `Tabs.Screen`. Esta propiedad acepta una función como valor que debe retornar el icono que queremos utilizar.
- La función que pasamos como valor recibe 2 parámetros `color y focused` para saber si el tab tiene que tener un color y también si es el Tab que está activo.

```javascript
tabBarIcon: ({ color, focused }) => (
  <Ionicons name={focused ? 'home-sharp' : 'home-outline'} color={color} size={24} />
),
```

- En este ejemplo vemos como podemos utilizar `focused` para saber si el Tab está activo o no para mostrar un icono con color de fondo lleno o sólo lineas.
- Le pasamos el color obtenido al icono para que se muestre de ese color y también podemos establecer el tamaño por medio la propiedad size.
- Agregamos los iconos `'home-sharp' y 'home-outline'` al componente `Tab.Screen` de la pantalla `index`.
- Agregamos los iconos `'information-circle' : 'information-circle-outline'` al componente `Tab.Screen` de la pantalla `about`.

```javascript
import { Tabs } from "expo-router";

import Ionicons from "@expo/vector-icons/Ionicons";

export default function TabLayout() {
  return (
    <Tabs
      screenOptions={{
        tabBarActiveTintColor: "#ffd33d",
      }}
    >
      <Tabs.Screen
        name="index"
        options={{
          title: "Home",
          tabBarIcon: ({ color, focused }) => (
            <Ionicons
              name={focused ? "home-sharp" : "home-outline"}
              color={color}
              size={24}
            />
          ),
        }}
      />
      <Tabs.Screen
        name="about"
        options={{
          title: "About",
          tabBarIcon: ({ color, focused }) => (
            <Ionicons
              name={
                focused ? "information-circle" : "information-circle-outline"
              }
              color={color}
              size={24}
            />
          ),
        }}
      />
    </Tabs>
  );
}
```

- Al hacer este cambio vemos iconos en nuestros Tabs y también utilizan un color más acorde al diseño de la app.
- También podemos customizar más opciones de la Barra de Tabs de la siguiente manera.

```javascript
<Tabs
  screenOptions={{
    tabBarActiveTintColor: '#ffd33d',
    headerStyle: {
      backgroundColor: '#25292e',
    },
    headerShadowVisible: false,
    headerTintColor: '#fff',
    tabBarStyle: {
    backgroundColor: '#25292e',
    },
  }}
>
```

- `tabBarActiveTintColor: "#ffd33d"`: establece el color activo de los tabs.
- `headerShadowVisible: false`: saca la sombra que utiliza el `header` para diferenciarse del contenido.
- `headerTintColor: "#fff"`: nos permite establecer el color de texto del header. En este caso usa el color blanco.
- `tabBarStyle`: acepta un objeto para configurar los estilos de los Tabs. En este caso estamos utilizando `{ backgroundColor: "#25292e" }` para cambiar el color de fondo.
- `headerStyle`: acepta un objeto para configurar el `header`. ` { backgroundColor: "#25292e" }` En este caso también le asigna un color para establecer el color de fondo.
- Con todos estos cambios nuestra aplicación empieza a tener un diseño propio y toda la pantalla quedó unificada aún si sigue manteniendo el header y la barra de navegación inferior con los Tabs.
- Hasta acá le agregamos un sistema de navegación `Stack` y otro `Tabs` a nuestra aplicación.

### Creando la primer pantalla

- En esta sección vamos a crear la primer pantalla de la aplicación.

![Sticker App](../assets//react-native/initial-layout.png)

- Esta pantalla muestra una imagen y dos botones.
- El usuario puede seleccionar una imagen utilizando uno de los dos botones.
- El primer botón permite al usuario seleccionar una imagen de su dispositivo.
- El segundo botón permite al usuario continuar con una imagen predeterminada proporcionada por la aplicación.

#### Analizando la pantalla

- Antes de escribir código, vamos a desglosarl algunos elementos esenciales.
- Hay dos elementos esenciales:
  - Una gran imagen en el centro de la pantalla.
  - Dos botones en la mitad inferior de la pantalla.
- El primer botón contiene varios componentes. Tiene un borde amarillo, con un icono y un componente de texto dentro de una fila.
- Ahora que dividimos la UI en partes más pequeñas, estamos listos para empezar a programar.

#### Mostrar la imagen

- En este tutorial vamos a usar el módulo `expo-image` para mostrar imagenes.
- Este módulo proporciona un componente `<Image>` multiplataforma para cargar y renderizar una imagen.
- Para poder utilizarlo debemos instalar el módulo `expo-image`.
- Si está corriendo `Metro` debemos primero frenar el server con `Ctrl + c` y luego ejecutar:

```bash
$ npx expo install expo-image
```

- Este comando instala la librería y la añadirá a las dependencias del proyecto en package.json.
- Al utilizar `expo` para instalar el módulo nos ayuda detectando la versión de Expo que utilizamos y se encarga de instalar la versión del módulo correspondiente.
- El componente `Imagen` acepta como propiedad `source` la ruta a la imagen que queremos mostrar.
- La fuente puede ser un asset o una URL.
- Por ejemplo, los assets dentro del directorio assets/images son estáticos.
- También podemos obtener una imágen de la red utilizando el valor uri.
- Utilizamos el componente `Image` en el archivo `app/(tabs)/index.tsx` de la siguiente manera:
  - Importamos `Image` del módulo `expo-image`.
  - Creamos una variable `PlaceholderImage` para utilizar el archivo `assets/images/background-image.png` como propiedad de origen en el componente Image.

```javascript
// app/(tabs)/index.tsx
import { View, StyleSheet } from "react-native";
import { Image } from "expo-image";

const PlaceholderImage = require("@/assets/images/background-image.png");

export default function Index() {
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <Image source={PlaceholderImage} style={styles.image} />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e",
    alignItems: "center",
  },
  imageContainer: {
    flex: 1,
  },
  image: {
    width: 320,
    height: 440,
    borderRadius: 18,
  },
});
```

- Si agregamos los assets iniciales a la carpeta `/assets/images/` podemos ver la ímagen que agregamos en el centro de la pantalla.
- Al agregar la imágen también agregamos nuevos estilos.
- Utilizamos `width y height` para establecer el ancho y alto de la imagen y un `borderRadius` para redondear los bordes.
- La imágen tiene un `View` con la propiedad `flex:1` para tomar todo el espacio disponible.
- El contenedor principal `container` centra el contenido con `alignItems: 'center'`.
- La variable `PlaceholderImage` está importando una imágen de la carpeta assets/images para mostrar por defecto cuando el usuario todavía no seleccionó ninguna imágen.

#### Dividiendo la aplicación en componentes

- Vamos a dividir el código en varios archivos a medida que añadimos más componentes a esta pantalla.
- A lo largo de este tutorial, utilizaremos el directorio `components` para crear componentes personalizados.
- Crea una carpeta con el nombre `componentes` al nivel de `app` y un archivo con el nombre `ImageViewer.tsx`.
- Mové el código para mostrar la imagen en este archivo junto con los estilos de la imagen.

```javascript
// components/ImageViewer.tsx
import { StyleSheet } from "react-native";
import { Image, type ImageSource } from "expo-image";

type Props = {
  imgSource: ImageSource,
};

export default function ImageViewer({ imgSource }: Props) {
  return <Image source={imgSource} style={styles.image} />;
}

const styles = StyleSheet.create({
  image: {
    width: 320,
    height: 440,
    borderRadius: 18,
  },
});
```

- Dado que `ImageViewer` es un componente personalizado, lo colocamos en un directorio separado en lugar del directorio `app`.
- Cada archivo dentro del directorio `app` es un archivo de layout o un archivo de ruta.
- En este componente estamos utilizando TypeScript para definir que este compomente acepta una propiedad que se llama `imgSource` y que es del tipo `ImageSource` que podemos importar de `expo-image`.
- También estamos creando un tipo de dato `Props` utilizando `type`.
- Ahora tenemos que importar `ImageViewer` y úsalo en `app/(tabs)/index.tsx`.

```javascript
// app/(tabs)/index.tsx
import { StyleSheet, View } from "react-native";

import ImageViewer from "@/components/ImageViewer";

const PlaceholderImage = require("@/assets/images/background-image.png");

export default function Index() {
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e",
    alignItems: "center",
  },
  imageContainer: {
    flex: 1,
  },
});
```

- `¿Qué significa @ en la sentencia import?`: El símbolo `@` es un `alias` de ruta personalizado para importar componentes personalizados y otros módulos en lugar de rutas relativas. Expo CLI lo configura automáticamente en `tsconfig.json`. (Es un alias de TS)

#### Crear botones usando Pressable

- React Native tiene diferentes maneras de manejar los eventos táctiles pero se recomienda utilizar `Pressable` por su flexibilidad.
- Puede detectar toques simples, pulsaciones largas, desencadenar eventos separados cuando el botón se presiona y se suelta, y más.
- En el diseño, hay dos botones que tenemos que crear.
- Cada uno tiene un estilo y una etiqueta diferentes.
- Vamos a empezar por crear un componente reutilizable para estos botones.
- Cree un archivo `Button.tsx` dentro del directorio `components` con el siguiente código:

```javascript
// components/Button.tsx
import { StyleSheet, View, Pressable, Text } from "react-native";

type Props = {
  label: string,
};

export default function Button({ label }: Props) {
  return (
    <View style={styles.buttonContainer}>
      <Pressable
        style={styles.button}
        onPress={() => alert("You pressed a button.")}
      >
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: {
    width: 320,
    height: 68,
    marginHorizontal: 20,
    alignItems: "center",
    justifyContent: "center",
    padding: 3,
  },
  button: {
    borderRadius: 10,
    width: "100%",
    height: "100%",
    alignItems: "center",
    justifyContent: "center",
    flexDirection: "row",
  },
  buttonLabel: {
    color: "#fff",
    fontSize: 16,
  },
});
```

- Este componente utiliza una función para manejar el evento `onPress` y mostrar un mensaje en pantalla.
- Luego aplicamos algunos estilos al botón que ya conocemos.
- La aplicación muestra una alerta cuando el usuario pulsa cualquiera de los botones de la pantalla.
- Esto sucede porque `Pressable` llama a `alert()` en su propiedad `onPress`.
- Vamos a importar este componente en el archivo `app/(tabs)/index.tsx` y añadir estilos para la `View` que encapsula estos botones.

```javascript
import { View, StyleSheet } from "react-native";

import Button from "@/components/Button";
import ImageViewer from "@/components/ImageViewer";

const PlaceholderImage = require("@/assets/images/background-image.png");

export default function Index() {
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} />
      </View>
      <View style={styles.footerContainer}>
        <Button label="Choose a photo" />
        <Button label="Use this photo" />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e",
    alignItems: "center",
  },
  imageContainer: {
    flex: 1,
    paddingTop: 28,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: "center",
  },
});
```

- Agregamos dos botones con el texto `Choose a photo` para que el usuario elija una foto y `Use this photo` para utilizar la imagen seleccionada.
- El contenedor de los botones tiene el estilo `footerContainer: { flex: 1 / 3, alignItems: "center" }` que establece que el alto del componente es 1/3 de la pantalla y que los botones tienen que estar centrados.
- Recordá que podes utilizar un color de fondo de este componente para ver el tamaño real que ocupa.
- Es un buen momento para revisar como se ve nuestra app en iOS, Android y también Web.
- Vemos que el segundo botón con la etiqueta `Use this photo` se parece al botón del diseño. Sin embargo, el primer botón necesita más estilo para ajustarse al diseño.

#### Mejorar el botón reutilizable

- El botón `Choose a photo` requiere un estilo diferente al del botón `Use this photo`, por lo que vamos a agregar una nueva propiedad al componente `Button` que nos permitirá aplicar un theme principal.
- Este botón también tiene un icono antes de la etiqueta.
- Vamos a agregar un icono `FontAwesome` del módulo `@expo/vector-icons`.
- Modificamos el componente `Button.tsx`:

```javascript
// components/Button.tsx
import { StyleSheet, View, Pressable, Text } from "react-native";
import FontAwesome from "@expo/vector-icons/FontAwesome";

type Props = {
  label: string,
  theme?: "primary",
};

export default function Button({ label, theme }: Props) {
  if (theme === "primary") {
    return (
      <View
        style={[
          styles.buttonContainer,
          { borderWidth: 4, borderColor: "#ffd33d", borderRadius: 18 },
        ]}
      >
        <Pressable
          style={[styles.button, { backgroundColor: "#fff" }]}
          onPress={() => alert("You pressed a button.")}
        >
          <FontAwesome
            name="picture-o"
            size={18}
            color="#25292e"
            style={styles.buttonIcon}
          />
          <Text style={[styles.buttonLabel, { color: "#25292e" }]}>
            {label}
          </Text>
        </Pressable>
      </View>
    );
  }

  return (
    <View style={styles.buttonContainer}>
      <Pressable
        style={styles.button}
        onPress={() => alert("You pressed a button.")}
      >
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: {
    width: 320,
    height: 68,
    marginHorizontal: 20,
    alignItems: "center",
    justifyContent: "center",
    padding: 3,
  },
  button: {
    borderRadius: 10,
    width: "100%",
    height: "100%",
    alignItems: "center",
    justifyContent: "center",
    flexDirection: "row",
  },
  buttonIcon: {
    paddingRight: 8,
  },
  buttonLabel: {
    color: "#fff",
    fontSize: 16,
  },
});
```

- Agregamos el icono `FontAwesome` que vamos a utilizar.
- Agregamos una propiedad con el nombre `theme` para establecer que tipo de botón queremos utilizar.
- En la definición de tipo de TypeScript establecemos que el theme puede utilizar un valor literal con el valor `primary`.
- Dentro del componente utilizamos el theme para renderizar un botón diferente según si `theme` es `primary` o no.
- Si el theme no es primary entonces el componente sigue retornando el diseño de botón que retornaba anteriormente.
- En cambio si el theme es primary retorna algo diferente:

```javascript
if (theme === "primary") {
  return (
    <View
      style={[
        styles.buttonContainer,
        { borderWidth: 4, borderColor: "#ffd33d", borderRadius: 18 },
      ]}
    >
      <Pressable
        style={[styles.button, { backgroundColor: "#fff" }]}
        onPress={() => alert("You pressed a button.")}
      >
        <FontAwesome
          name="picture-o"
          size={18}
          color="#25292e"
          style={styles.buttonIcon}
        />
        <Text style={[styles.buttonLabel, { color: "#25292e" }]}>{label}</Text>
      </Pressable>
    </View>
  );
}
```

- Ambos botones utilizan el estilo en común definido en `styles.buttonContainer` pero si el theme es primary entonces agrega o sobrescribe algunas propiedades de estilo `{ borderWidth: 4, borderColor: "#ffd33d", borderRadius: 18 }`.
- Este botón utiliza un icono como hijo y también un texto.
- Al tener que utilizar otros estilos en este tutorial vemos como utilizando `style={[]}` podemos pasar un array de estilos.
- El primer estilo que pasamos es el `'base'` que luego podemos modificar en el segundo estilo. Ejemplo `style={[ {color: 'white'}, {color: 'blue'} ]}`.
- React Native crea un estilo con toda esta definición y se aplicará el resultado de hacer un merge entre todos los objetos. En caso de existir propiedades en común entre los objetos, RN va a utilizar las últimas propiedades.
- Usar estilo en la propiedad `style` se conoce como `inline style`.
- Ahora, modificamos el archivo `app/(tabs)/index.tsx` para utilizar la propiedad `theme="primary"` en el primer botón.

```javascript
<View style={styles.footerContainer}>
  <Button label="Choose a photo" theme="primary" />
  <Button label="Use this photo" />
</View>
```

- Excelente, la pantalla nos va quedando como estaba definido en el diseño inicial.
- Al presionar cualquiera de los botones se muestra una alerta con un mensaje.
- Esta pantalla se puede ver bien en iOS, Android y Web.

### Usar un selector de imágenes

- React Native proporciona componentes como `<View>, <Text> y <Pressable>`.
- Estamos construyendo una feature para seleccionar una imagen de la galería multimedia del dispositivo.
- Esto no es posible con los componentes básicos de React Native y necesitaremos un módulo para añadir esta funcinalidad en nuestra aplicación.
- Vamos a utiliza `expo-image-picker`, un módulo de Expo SDK.
- `expo-image-picker` proporciona acceso a la UI del sistema operativo para seleccionar imágenes y vídeos de la biblioteca del dispositivo.

#### Instalar expo-image-picker

- Para instalar este módulo ejecutamos el siguiente comando:

```bash
$ npx expo install expo-image-picker
```

- `Consejo`: Cada vez que instalemos una nueva librería en nuestro proyecto, es conveniente detener el servidor de desarrollo pulsando `Ctrl + c` en la terminal y a continuación ejecutemos el comando de instalación.
- Una vez finalizada la instalación, podemos volver a iniciar el servidor de desarrollo ejecutando `npx expo` desde la misma ventana de terminal.

#### Elige una imagen de la biblioteca multimedia del dispositivo

- `expo-image-picker` proporciona el método `launchImageLibraryAsync()` para mostrar la interfaz de usuario del sistema seleccionando una imagen o un vídeo de la biblioteca multimedia del dispositivo.
- Utilizaremos el botón principal para seleccionar una imagen de la biblioteca multimedia del dispositivo. Para ello vamos a crear una función para abrir la biblioteca de imágenes del dispositivo.
- En `app/(tabs)/index.tsx`, importamos la biblioteca `expo-image-picker` y creamos una función con el nombre `pickImageAsync` dentro del componente Index.

```javascript
// ...Los imports anteriores siguen igual.
import * as ImagePicker from "expo-image-picker";

export default function Index() {
  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ["images"],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      console.log(result);
    } else {
      alert("You did not select any image.");
    }
  };

  // ...El resto del código sige igual.
}
```

- En `import * as ImagePicker from "expo-image-picker"` importamos todo el código que exporta el módulo para poder utilizar el ImagePicker. `*` es la forma de especificar que queremos todo del módulo y luego con `as ImagePicker` lo renombramos.
- Definimos la función `const pickImageAsync = async ()` utilizando async ya que vamos a utilizar la función `.launchImageLibraryAsync` que retorna una promise.

```javascript
let result = await ImagePicker.launchImageLibraryAsync({
  mediaTypes: ["images"],
  allowsEditing: true,
  quality: 1,
});
```

- Usamos `await` para esperar que ImagePicker abra el selector de imágenes.
- Le pasamos un objeto como parámetro con opcones para que muestre imágenes, que se pueda editar.
- Cuando `allowsEditing` es `true` le permite al usuario cropear la imagen durante la selección ya sea en Android o iOS.

```javascript
if (!result.canceled) {
  console.log(result);
} else {
  alert("You did not select any image.");
}
```

- Luego validamos si el resultado no es `cancelado` mostramos un mensaje en consola con el resultado.
- Si el resultado fue cancelado mostramos un mensaje de que ningúna imagen fue seleccionada.

#### Actualizar el compponente Button

- Al presionar el botón primario, llamamos a la función `pickImageAsync()` del componente Button.
- Actualizamos la propiedad `onPress` del componente Button en `components/Button.tsx`.

```javascript
import { StyleSheet, View, Pressable, Text } from "react-native";
import FontAwesome from "@expo/vector-icons/FontAwesome";

type Props = {
  label: string,
  theme?: "primary",
  onPress?: () => void,
};

export default function Button({ label, theme, onPress }: Props) {
  if (theme === "primary") {
    return (
      <View
        style={[
          styles.buttonContainer,
          { borderWidth: 4, borderColor: "#ffd33d", borderRadius: 18 },
        ]}
      >
        <Pressable
          style={[styles.button, { backgroundColor: "#fff" }]}
          onPress={onPress}
        >
          <FontAwesome
            name="picture-o"
            size={18}
            color="#25292e"
            style={styles.buttonIcon}
          />
          <Text style={[styles.buttonLabel, { color: "#25292e" }]}>
            {label}
          </Text>
        </Pressable>
      </View>
    );
  }

  return (
    <View style={styles.buttonContainer}>
      <Pressable
        style={styles.button}
        onPress={() => alert("You pressed a button.")}
      >
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: {
    width: 320,
    height: 68,
    marginHorizontal: 20,
    alignItems: "center",
    justifyContent: "center",
    padding: 3,
  },
  button: {
    borderRadius: 10,
    width: "100%",
    height: "100%",
    alignItems: "center",
    justifyContent: "center",
    flexDirection: "row",
  },
  buttonIcon: {
    paddingRight: 8,
  },
  buttonLabel: {
    color: "#fff",
    fontSize: 16,
  },
});
```

- En `app/(tabs)/index.tsx`, utilizamos la función `pickImageAsync` como valor de la propiedad `onPress` del primer `Button`.

```javascript
<Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
```

- La función `pickImageAsync` invoca a `ImagePicker.launchImageLibraryAsync()` y luego maneja el resultado.
- El método `launchImageLibraryAsync()` retorna un objeto que contiene información sobre la imagen seleccionada.
- Los propiedades del objeto cambian según el dispositivo o si es web.

#### Utilizar la imágen seleccionada

- El objeto `result` nos da un array de `assets`, que contiene la `uri` de la imagen seleccionada.
- Tomemos este valor del selector de imágenes y lo utilizamos para mostrar la imagen seleccionada en la app.
- Modificamos el componente `app/(tabs)/index.tsx` de la siguiente manera.
- Agregamos `import { useState } from 'react';` para utilizar `useState`.
- Creamos una nueva variable de estado con el nombre `selectedImage` de la siguiente manera: `  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);`.
- Si el usuario no cancela la selección entonces podemos establecer la imágen seleccionada en el estado del componente: ` setSelectedImage(result.assets[0].uri);`.
- Finalmente podemos utilizar la `uri` de la image seleccionada para mostrar localmente la imágen: `<ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />`.
- Con todos estos cambios el componente nos queda de la siguiente forma:

```javascript
// app/(tabs)/index.tsx
import { View, StyleSheet } from "react-native";
import * as ImagePicker from "expo-image-picker";

// Importamos `useState`
import { useState } from "react";

import Button from "@/components/Button";
import ImageViewer from "@/components/ImageViewer";

const PlaceholderImage = require("@/assets/images/background-image.png");

export default function Index() {
  // Creamos la variable de estado
  const [selectedImage, setSelectedImage] =
    (useState < string) | (undefined > undefined);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ["images"],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      // Seleccionamos y guardamos en estado la imagen seleccionada.
      setSelectedImage(result.assets[0].uri);
    } else {
      alert("You did not select any image.");
    }
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        {
          // Utilizamos la imágen seleccionada.
        }
        <ImageViewer
          imgSource={PlaceholderImage}
          selectedImage={selectedImage}
        />
      </View>
      <View style={styles.footerContainer}>
        <Button
          theme="primary"
          label="Choose a photo"
          onPress={pickImageAsync}
        />
        <Button label="Use this photo" />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e",
    alignItems: "center",
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: "center",
  },
});
```

- Para poder mostrar la imágen todavía tenemos que pasar la propiedad `selectedImage` al componente `ImageViewer`.
- Modificamos el archivo `components/ImageViewer.tsx` para que acepte la propiedad `selectedImage`.
- El código de la imágen se está haciendo largo por lo cual podemos moverlo también a una variable separada llamada `imageSource`.
- Pasamos `imageSource` como el valor de la propiedad `source` en el componente Image.

```javascript
import { StyleSheet } from "react-native";
import { Image, type ImageSource } from "expo-image";

type Props = {
  imgSource: ImageSource,
  // Agregamos la propiedad selectedImage al componente ImageViewer
  selectedImage?: string,
};

// Agregamos selectedImage como propiedad del componente.
export default function ImageViewer({ imgSource, selectedImage }: Props) {
  // Si el componente recibe una imágen seleccionada entonces utiliza un objeto con la propiedad uri. Sino usa la propiedad imgSource.
  const imageSource = selectedImage ? { uri: selectedImage } : imgSource;

  // Ahora que tenemos el valor en una variable lo podemos utilizar como imageSource.
  return <Image source={imageSource} style={styles.image} />;
}

const styles = StyleSheet.create({
  image: {
    width: 320,
    height: 440,
    borderRadius: 18,
  },
});
```

- En el componente utiliza un operador condicional para cargar la fuente de la imagen.
- La imagen seleccionada es una `cadena uri`, no un archivo local como la imagen inicial que está en la carpeta assets.
- Podes descargar y utilizar imágenes de [Unsplash](https://unsplash.com/) como utiliza el ejemplo de la documentación de Expo.
- Genial, agregamos con éxito la funcionalidad para elegir una imagen de la biblioteca multimedia del dispositivo.

### Crear un Modal

- Como sabemos React Native nos da un componente `<Modal>` que presenta contenido por encima del resto de la aplicación.
- En general, los modals se utilizan para llamar la atención del usuario hacia información crítica o para que realice una acción.
- Vamos a crear un Modal que muestre una lista de emojis que el usuario pueda seleccionar.

#### Agregar un nuevo estado para mostrar / ocultar los botones

- Antes de implementar el modal, vamos a agregar tres nuevos botones.
- Estos botones son visibles después de que el usuario elige una imagen.
- Uno de estos botones activará el modal para seleccionar un emoji.
- En `app/(tabs)/index.tsx` deeclaramos una variable de estado del tipo boolean con el nombre `showAppOptions` para mostrar u ocultar los botones que abren el modal, junto con algunas otras opciones.
- Incialmente vamos a establecer esta nueva variable con el valor `false`.
- Cuando el usuario selecciona una imagen la establemos en `true`.

```javascript
// Vamos a agregar la nueva variable con el valor false por defecto.
const [showAppOptions, setShowAppOptions] = useState < boolean > false;

// Luego al seleccionar la imágen vamos a cambiar el estado de la variable showAppOptions a true.
setShowAppOptions(true);

// Finalmente necesitamos manejar el render del componente para mostrar los botones de selección de imágen o una nueva sección luego de elegir la imágen.
{
  showAppOptions ? (
    <View />
  ) : (
    <View style={styles.footerContainer}>
      <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
      <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
    </View>
  );
}
```

- Utilizamos `showAppOptions` como condicional para elegir si mostramos los nuevos botones que vamos a crear o los de selección de imágen.
- La idea es que cuando el usuario selecciona la imágen cambiamos el valor de la variable `showAppOptions` y de esta forma podemos ocultar los botones de selección en el próximo render y mostramos los nuevos que vamos a crear.
- Así te debería quedar el componente:

```javascript
// app/(tabs)/index.tsx
import { View, StyleSheet } from "react-native";
import * as ImagePicker from "expo-image-picker";
import { useState } from "react";

import Button from "@/components/Button";
import ImageViewer from "@/components/ImageViewer";

const PlaceholderImage = require("@/assets/images/background-image.png");

export default function Index() {
  const [selectedImage, setSelectedImage] =
    (useState < string) | (undefined > undefined);
  const [showAppOptions, setShowAppOptions] = useState < boolean > false;

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ["images"],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert("You did not select any image.");
    }
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer
          imgSource={PlaceholderImage}
          selectedImage={selectedImage}
        />
      </View>
      {showAppOptions ? (
        <View />
      ) : (
        <View style={styles.footerContainer}>
          <Button
            theme="primary"
            label="Choose a photo"
            onPress={pickImageAsync}
          />
          <Button
            label="Use this photo"
            onPress={() => setShowAppOptions(true)}
          />
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e",
    alignItems: "center",
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: "center",
  },
});
```

- Ahora, podemos eliminar el alerta que llamamos en el componente Button y actualizar el event handler `onPress` al renderizar el segundo botón en `components/Button.tsx`.

```javascript
// components/Button.tsx

<Pressable style={styles.button} onPress={onPress} >
```

#### Agregar botones

- Vamos a mirar el diseño de los botones de opciónes que vamos a implementar.
- Podemos ver el diseño en la siguiente imágen:

![Botones](../assets/react-native/buttons-layout.jpg)

- Por lo que podemos ver podemos tener compnente padre `<View>` con tres botones alineados en fila.
- El botón del medio con el icono de más (+) va a abrir el modal y tiene un estilo diferente al de los otros dos botones.
- Dentro de la carpeta `components` vamos a crear un nuevo archivo con el nombre `CircleButton.tsx` con el siguiente código:

```javascript
import { View, Pressable, StyleSheet } from "react-native";
import MaterialIcons from "@expo/vector-icons/MaterialIcons";

type Props = {
  onPress: () => void,
};

export default function CircleButton({ onPress }: Props) {
  return (
    <View style={styles.circleButtonContainer}>
      <Pressable style={styles.circleButton} onPress={onPress}>
        <MaterialIcons name="add" size={38} color="#25292e" />
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  circleButtonContainer: {
    width: 84,
    height: 84,
    marginHorizontal: 60,
    borderWidth: 4,
    borderColor: "#ffd33d",
    borderRadius: 42,
    padding: 3,
  },
  circleButton: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    borderRadius: 42,
    backgroundColor: "#fff",
  },
});
```

- Este componnte usa `MaterialIcons` para mostrar el icono de más.
- Los otros dos botones también van a usar `MaterialIcons` para mostrar un componente de texto y un iconos alineados verticalmente.
- Cree un archivo con el nombre de `IconButton.tsx` dentro del directorio components.
- Este componente acepta tres propiedades:
  - `icon`: el nombre del icono de MaterialIcons.
  - `label`: el texto que se muestra en el botón.
  - `onPress`: un callback para que se llame cuando se presiona el botón.

```javascript
import { Pressable, StyleSheet, Text } from 'react-native';
import MaterialIcons from '@expo/vector-icons/MaterialIcons';

type Props = {
  // Esta forma define que tome uno de los keys o llaves que están definidos dentro de MaterialIcons.glyphMap para limitar que sólo se pueda elegir un nombre de ese tipo.
  icon: keyof typeof MaterialIcons.glyphMap;
  label: string;
  onPress: () => void;
};

export default function IconButton({ icon, label, onPress }: Props) {
  return (
    <Pressable style={styles.iconButton} onPress={onPress}>
      <MaterialIcons name={icon} size={24} color="#fff" />
      <Text style={styles.iconButtonLabel}>{label}</Text>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  iconButton: {
    justifyContent: 'center',
    alignItems: 'center',
  },
  iconButtonLabel: {
    color: '#fff',
    marginTop: 12,
  },
});

```

- Ahora tenemos que actualizar `app/(tabs)/index.tsx` para utilizar los botones.
- Para hacer esto tenemos que importar los componentes `CircleButton` e `IconButton`.
- Agregamos tres funciones `placeholder` para estos botones.
- Vamos a llamar a una función con el nombre `onReset` cuando el usuario presiona el botón de reinicio, haciendo que el botón de selección de imagen aparezca de nuevo.
- La otra funcionalidad la agregamos más adelante.

```javascript
// Importamos los componentes
import IconButton from "@/components/IconButton";
import CircleButton from "@/components/CircleButton";

// Agregamos 3 funciones que van a manejar el evento onPress de los botones.
const onReset = () => {
  setShowAppOptions(false);
};

const onAddSticker = () => {
  // TODO: Agregar esto luego
};

const onSaveImageAsync = async () => {
  // TODO: Agregar esto luego
};

// Agregamos los botones
{
  showAppOptions ? (
    <View style={styles.optionsContainer}>
      <View style={styles.optionsRow}>
        <IconButton icon="refresh" label="Reset" onPress={onReset} />
        <CircleButton onPress={onAddSticker} />
        <IconButton icon="save-alt" label="Save" onPress={onSaveImageAsync} />
      </View>
    </View>
  ) : (
    <View style={styles.footerContainer}>
      <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
      <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
    </View>
  );
}
```

#### Creamos el modal para seleccionar Emojis

- El modal le va a permitir al usuario elegir un emoji de una lista de emoji disponibles.
- Creamos un archivo `EmojiPicker.tsx` dentro de la carpeta `components`.
- Este componente acepta tres propiedades:
  - `isVisible`: es un valor boolean para determinar el estado de visibilidad del modal.
  - `onClose`: una función para cerrar el modal.
  - `children`: se utiliza más adelante para mostrar una lista de emoji.

```javascript
import { Modal, View, Text, Pressable, StyleSheet } from "react-native";
import { PropsWithChildren } from "react";
import MaterialIcons from "@expo/vector-icons/MaterialIcons";

type Props = PropsWithChildren<{
  isVisible: boolean,
  onClose: () => void,
}>;

export default function EmojiPicker({ isVisible, children, onClose }: Props) {
  return (
    <View>
      <Modal animationType="slide" transparent={true} visible={isVisible}>
        <View style={styles.modalContent}>
          <View style={styles.titleContainer}>
            <Text style={styles.title}>Choose a sticker</Text>
            <Pressable onPress={onClose}>
              <MaterialIcons name="close" color="#fff" size={22} />
            </Pressable>
          </View>
          {children}
        </View>
      </Modal>
    </View>
  );
}

const styles = StyleSheet.create({
  modalContent: {
    height: "25%",
    width: "100%",
    backgroundColor: "#25292e",
    borderTopRightRadius: 18,
    borderTopLeftRadius: 18,
    position: "absolute",
    bottom: 0,
  },
  titleContainer: {
    height: "16%",
    backgroundColor: "#464C55",
    borderTopRightRadius: 10,
    borderTopLeftRadius: 10,
    paddingHorizontal: 20,
    flexDirection: "row",
    alignItems: "center",
    justifyContent: "space-between",
  },
  title: {
    color: "#fff",
    fontSize: 16,
  },
});
```

- El componente `Modal` muestra un título y un botón de cierre.
- Su propiedad `visible` toma el valor de `isVisible` y controla si el modal está abierto o cerrado.
- La propiedad `transparent` es un valor booleano, que determina si el modal llena toda la vista.
- `animationType` determina cómo entra y sale de la pantalla. En este caso, se desliza desde la parte inferior de la pantalla.
- Por último, el `EmojiPicker` invoca la proposición `onClose` cuando el usuario pulsa el componente `Pressable`.
- Ahora, tenemos que modificar el componente `app/(tabs)/index.tsx`.
- Vamos a importar el componente `EmojiPicker`.
- Creamoms una variable de estado `isModalVisible` con el hook `useState`. Su valor por defecto es `false`, que oculta el modal hasta que el usuario pulsa el botón para abrirlo.
- Cambiamos el comentario en la función `onAddSticker` para actualizar la variable `isModalVisible` a `true` cuando el usuario pulse el botón. Esto abrirá el selector de emoji.
- Crea una nueva función `onModalClose` para actualizar la variable de estado `isModalVisible`.
- Agregamos el componente `EmojiPicker` en la parte inferior del componente Index.

```javascript
// importamos el componente EmojiPicker
import EmojiPicker from "@/components/EmojiPicker";

// Creamos la nueva variable de estado isModalVisible usando useState
const [isModalVisible, setIsModalVisible] = useState < boolean > false;

// Actualizamos la función para cambiar el valor de la variable de estado isModalVisible y hacer que se vea el Modal.
const onAddSticker = () => {
  setIsModalVisible(true);
};

// Cambiamos el valor de isModalVisible a false para que se oculte el Modal.
const onModalClose = () => {
  setIsModalVisible(false);
};
```

- Si todo va bien `index.tsx` debería estar así:

```javascript
import { View, StyleSheet } from "react-native";
import * as ImagePicker from "expo-image-picker";
import { useState } from "react";

import Button from "@/components/Button";
import ImageViewer from "@/components/ImageViewer";
import IconButton from "@/components/IconButton";
import CircleButton from "@/components/CircleButton";

import EmojiPicker from "@/components/EmojiPicker";

const PlaceholderImage = require("@/assets/images/background-image.png");

export default function Index() {
  const [selectedImage, setSelectedImage] =
    (useState < string) | (undefined > undefined);
  const [showAppOptions, setShowAppOptions] = useState < boolean > false;
  const [isModalVisible, setIsModalVisible] = useState < boolean > false;

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ["images"],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert("You did not select any image.");
    }
  };

  const onReset = () => {
    setShowAppOptions(false);
  };

  const onAddSticker = () => {
    setIsModalVisible(true);
  };

  const onModalClose = () => {
    setIsModalVisible(false);
  };

  const onSaveImageAsync = async () => {
    // we will implement this later
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer
          imgSource={PlaceholderImage}
          selectedImage={selectedImage}
        />
      </View>
      {showAppOptions ? (
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton icon="refresh" label="Reset" onPress={onReset} />
            <CircleButton onPress={onAddSticker} />
            <IconButton
              icon="save-alt"
              label="Save"
              onPress={onSaveImageAsync}
            />
          </View>
        </View>
      ) : (
        <View style={styles.footerContainer}>
          <Button
            theme="primary"
            label="Choose a photo"
            onPress={pickImageAsync}
          />
          <Button
            label="Use this photo"
            onPress={() => setShowAppOptions(true)}
          />
        </View>
      )}
      <EmojiPicker isVisible={isModalVisible} onClose={onModalClose}>
        {/* A list of emoji component will go here */}
      </EmojiPicker>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e",
    alignItems: "center",
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: "center",
  },
  optionsContainer: {
    position: "absolute",
    bottom: 80,
  },
  optionsRow: {
    alignItems: "center",
    flexDirection: "row",
  },
});
```

#### Mostrar la lista de emojis

- Vamos a agregar una lista horizontal de emoji en el contenido del modal.
- Para esto podemos usar una nueva lista llamada `FlatList` de React Native.
- Creamos un nuevo archivo con el nombre `EmojiList.tsx` dentro de la carpeta `components` y agregamos el siguiente código:

```javascript
import { useState } from 'react';
import { StyleSheet, FlatList, Platform, Pressable } from 'react-native';
import { Image, type ImageSource } from 'expo-image';

type Props = {
  onSelect: (image: ImageSource) => void;
  onCloseModal: () => void;
};

export default function EmojiList({ onSelect, onCloseModal }: Props) {
  const [emoji] = useState<ImageSource[]>([
    require("../assets/images/emoji1.png"),
    require("../assets/images/emoji2.png"),
    require("../assets/images/emoji3.png"),
    require("../assets/images/emoji4.png"),
    require("../assets/images/emoji5.png"),
    require("../assets/images/emoji6.png"),
  ]);

  return (
    <FlatList
      horizontal
      showsHorizontalScrollIndicator={Platform.OS === 'web'}
      data={emoji}
      contentContainerStyle={styles.listContainer}
      renderItem={({ item, index }) => (
        <Pressable
          onPress={() => {
            onSelect(item);
            onCloseModal();
          }}>
          <Image source={item} key={index} style={styles.image} />
        </Pressable>
      )}
    />
  );
}

const styles = StyleSheet.create({
  listContainer: {
    borderTopRightRadius: 10,
    borderTopLeftRadius: 10,
    paddingHorizontal: 20,
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'space-between',
  },
  image: {
    width: 100,
    height: 100,
    marginRight: 20,
  },
});

```

- El componente `FlatList` renderiza todas las imágenes emoji utilizando el componente `Image`, envuelto por un componente `Pressable`.
- Más adelante, lo podemos mejorar para que el usuario pueda pulsar un emoji en la pantalla para que aparezca como un sticker en la imagen.
- También toma un array de items proporcionado por la variable array emoji como valor de la prop data.
- La propiedad `renderItem` tomca cada elemento de los datos y devuelve el un elemento de la lista para renderizar.
- Finalmente, agregamos los componentes `Image` y `Pressable para mostrar este elemento.
- La propiedad `horizontal` muestra la lista horizontalmente en lugar de verticalmente.
- La propiedad `showsHorizontalScrollIndicator` se utiliza para mostrar o ocutlar la barra de scrool. En este caso debemos utilizar el módulo `Platform` de React Native para comprobar si al app está corriendo en web.
- Finalmente actualizamos el componente `app/(tabs)/index.tsx` para importar el componente `EmojiList`.
  y reemplaza los comentarios dentro del componente <EmojiPicker> con el siguiente fragmento de código:
