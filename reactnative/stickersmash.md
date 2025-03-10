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

### USar un selector de imágenes
