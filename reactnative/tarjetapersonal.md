# React Native

## Tarjeta Personal

- En este proyecto vamos a crear una tarjeta personal.
- La idea es utilizar componentes básicos de React Native para poder crear una app que muestre nuestra información de contacto.
- Para empezar debemos crear el proyecto.

```bash
$ npx create-expo-app@latest tarjeta_personal
```

- Luego de crear el projecto necesitamos resetear el proyecto de Expo para empezar a trabajar.

```bash
$ npm run reset-project
```

- Ahora tenemos un proyecto listo para empezar a trabajar.
- Vamos a trabajar sobre el archivo `app/index.tsx`.
- `index.tsx` es nuestra pantalla principal cuando utilizamos `expo-router` que viene configurado por defecto en un nuevo proyecto expo.
- Lo primero que vamos a hacer es sacar el header de la app para que se vea la pantalla completa.
- Podemos hacer esto modificando el archivo `app/_layout.tsx`.
- Al abrir el archivo nos encontramos con el siguiente código:

```javascript
import { Stack } from "expo-router";

export default function RootLayout() {
  return <Stack />;
}
```

- En este caso `expo-router` establecer que vamos a utilizar un navegador del tipo Stack.
- Para poder sacar el header vamos a tener que agregar la pantalla index de la siguiente manera:

```javascript
import { Stack } from "expo-router";

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="index" />
    </Stack>
  );
}
```

- En este caso tenemos un componente `Stack` que acepta componentes hijos que son `Stack.Screen` para definir pantallas.
- Nuestra pantalla se llama `index` por lo cual establecemos la propiedad `name="index"` para decirle al router que la ruta que queremos modificar es la del archivo `index.tsx`.
- Ahora tenemos que configurar que no queremos ver el header utilizando la prorpiedad `options`.
- `options` es una propiedad que acepta un objeto de configuración.
- Para sacar el header utilizamos la configuración `headerShown` y le establecemos el valor `false`.
- De esta manera sacamos el header para la pantalla `index`.

```javascript
import { Stack } from "expo-router";

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="index" options={{ headerShown: false }} />
    </Stack>
  );
}
```

- Ahora que no tenemos más el header vamos a agregar un `SafeAreaView` para asegurarnos que la app se vea bien en cualquier dispositivo.
- En el archivo `index.tsx` importamos el componente `SafeAreaView` y lo utilizamos como primer componente de nuestra app de la siguiente manera:

```javascript
import { Text, SafeAreaView } from "react-native";

export default function Index() {
  return (
    <SafeAreaView
      style={{
        flex: 1,
      }}
    >
      <Text>Edit app/index.tsx to edit this screen.</Text>
    </SafeAreaView>
  );
}
```

- Podemos ver que en este caso la propiedad style tiene tan solo la propiedad `flex:1` para que este componente ocupe toda la pantalla.
- Ya que vamos a estar armando una nueva aplicación podemos utilizar `StyleSheet` para crear una hoja de estilo y crear nuestro primer estilo.
- Importamos `StyleSheet` de react-native.
- Creamos una nueva variable con el nombre `styles` en la parte de abajo de nuestro archivo.
- Le asignamos a la variable `styles` lo retornado por llamar a `StyleSheet.create({})`.
- `StyleSheet.create` retorna un objeto que podemos utilizar para configurar estilos.
- Creamos una nueva propiedad con el nombre de `container` y le asignamos el mísmo código que está en la propiedad `style` del componente `SafeAreaView`
- Utilizamos la variable `styles` en la propiedad `style` del componente SafeAreaView como `style={styles.container}`.

```javascript
import { Text, SafeAreaView, StyleSheet } from "react-native";

export default function Index() {
  return (
    <SafeAreaView style={}>
      <Text>Edit app/index.tsx to edit this screen.</Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
});
```

- Si todo va bien deberíamos ver el texto inicial en el borde superior izquierdo de la pantalla.
- Dado que el contenido de nuestra aplicación puede crecer vamos a establecer el contenido dentro de un componente `ScrollView` para poder scrollear el contenido de ser necesario.

```javascript
import { Text, SafeAreaView, StyleSheet, ScrollView } from "react-native";

export default function Index() {
  return (
    <SafeAreaView style={styles.contenido}>
      <ScrollView>
        <Text>Edit app/index.tsx to edit this screen.</Text>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
});
```

- Ahora vamos a crear un componente `View` para usar como contenedor del contenido.

```javascript
import { Text, SafeAreaView, StyleSheet, ScrollView, View } from "react-native";

export default function Index() {
  return (
    <SafeAreaView style={styles.contenido}>
      <ScrollView>
        <View>
          <Text>Edit app/index.tsx to edit this screen.</Text>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
});
```

- Creamos una nueva propiedad en el objeto styles con el nombre de `contentContainer`.
- Asignamos el estilo `contentContainer` al componente View de la siguiente forma `style={styles.contentContainer}`.
- Ahora le podemos agregar estilo al contenedor con las siguientes propiedades y valores:

```javascript
{
  flex: 1,
  backgroundColor: 'white',
  alignItems: 'center',
  justifyContent: 'center',
}
```

- Con `flex:1` le decimos a React Native que este compoente va a ocupar todo el espacio que pueda.
- `backgroundColor` nos permite establecer un color para el fondo del contenido. En este caso lo establecemos en `white` para que sea blanco.
- `alignItems` se utiliza para alinear el contenido en flexbox. En este caso utilzamos `center` para establecer que queremos que esté en el medio del componente padre.
- `justifyContent` también se utiliza para alinear contenido en flexbox y también lo establecemos en `center` para que quede en el centro de la pantalla.
- Existe una propiedad llamada `flexboxDirection` que tiene como valor `column` o `row`.
- Cuando `flexboxDirection` está establecido en `column`, como viene por defecto, hace que `justifyContent` alinie las cosas de manera vertical y `alignItems` lo haga de manera horizontal.
- Cuando `flexboxDirection` está establecido en `row`, hace que `justifyContent` alinie las cosas de manera horizontal y `alignItems` lo haga de manera vertical.
- De esta manera vemos como estoas propiedades cambian según la orientación que tenga flexbox.
- Dado que esta es nuestra tarjeta personal vamos a poner nuestro nombre como contenido.
- Modificamos el texto `Edit app/index.tsx to edit this screen.` y lo cambiamos por nuestro nombre y apellido.

```javascript
import { Text, SafeAreaView, StyleSheet, ScrollView, View } from "react-native";

export default function Index() {
  return (
    <SafeAreaView style={styles.contenido}>
      <ScrollView>
        <View style={styles.contentContainer}>
          <Text>Nicolas Isnardi</Text>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
  contentContainer: {
    flex: 1,
    backgroundColor: "white",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

- Ahora le agregamos estilo para que se vea mejor.
- Creamos un nuevo estilo con el nombre de `title`.
- Asignamos el estilo `title` al componente `Text` que muestra nuestro nombre.
- Le asignamos las siguientes propiedades de estilo:

```javascript
{
  fontSize: 30,
  fontWeight: 'bold'
}
```

- La propiedad`fontSize` nos permite establecer el tamaño de la tipografía. En este caso lo hacemos en 30.
- `fontWeight` nos permite establecer si queremos que la tipografía esté en negrita o no.
  Utilizando el valor `bold` establecemos que el texto tiene que estar en negrita.

```javascript
import { Text, SafeAreaView, StyleSheet, ScrollView, View } from "react-native";

export default function Index() {
  return (
    <SafeAreaView style={styles.contenido}>
      <ScrollView>
        <View style={styles.contentContainer}>
          <Text style={styles.title}>Nicolas Isnardi</Text>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
  contentContainer: {
    flex: 1,
    backgroundColor: "white",
    alignItems: "center",
    justifyContent: "center",
  },
  title: { fontSize: 30, fontWeight: "bold" },
});
```

- Ahora deberíamos ver nuestro nombre en negrita y tipografía mucho más grande.
- Esta tarjeta quedaría muy linda con un banner de fondo en la parte superior.
- Para poder crear un banner podemos utilizar el componente `Image`.
- Dado que no tenemos ningún asset podemos utilizar una ruta remota.
- Importamos el componente `Image` de react-native.
- Agregamos un componente `Image` arriba del componente `Text`.
- Vamos a utilizar la ruta: `https://itspectrumsolutions.com/wp-content/uploads/2024/03/reactnative.jpg` como source de nuestro componente.
- Dado que es una imágen remota tenemos que establecer la propiedad `source={{}}` con un objeto y establecer la propiedad `uri` con la dirección de la imágen.
- También al ser una imágen remota sabemos que React Native no tiene forma de calcular el tamaño de la misma por lo cual debemos utilizar la propiedad de estilo `width` y establecer el `100%` de la pantalla.
- Hay una propiedad especial de estilo que se llama `aspectRatio` que nos permite establecer un valor. En este caso podemos utilizar `16/9`.

```javascript
import {
  Text,
  SafeAreaView,
  StyleSheet,
  ScrollView,
  View,
  Image,
} from "react-native";

export default function Index() {
  return (
    <SafeAreaView style={styles.contenido}>
      <ScrollView>
        <View style={styles.contentContainer}>
          <Image
            source={{
              uri: "https://itspectrumsolutions.com/wp-content/uploads/2024/03/reactnative.jpg",
            }}
            style={{ width: "100%", aspectRatio: 16 / 9 }}
          />
          <Text style={styles.title}>Nicolas Isnardi</Text>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
  contentContainer: {
    flex: 1,
    backgroundColor: "white",
    alignItems: "center",
    justifyContent: "center",
  },
  title: { fontSize: 30, fontWeight: "bold" },
});
```

- Ahora que vemos que todo funciona bien podemos hacer un refactor y mover el estilo al objeto de estilo.
- Creamos un estilo que se llame banner y copiamos y pegamos el estilo que tiene el banner.

```javascript
import {
  Text,
  SafeAreaView,
  StyleSheet,
  ScrollView,
  View,
  Image,
} from "react-native";

export default function Index() {
  return (
    <SafeAreaView style={styles.contenido}>
      <ScrollView>
        <View style={styles.contentContainer}>
          <Image
            source={{
              uri: "https://itspectrumsolutions.com/wp-content/uploads/2024/03/reactnative.jpg",
            }}
            style={styles.banner}
          />
          <Text style={styles.title}>Nicolas Isnardi</Text>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
  contentContainer: {
    flex: 1,
    backgroundColor: "white",
    alignItems: "center",
    justifyContent: "center",
  },
  title: { fontSize: 30, fontWeight: "bold" },
  banner: { width: "100%", aspectRatio: 16 / 9 },
});
```

- Ahora podemos agregar alguna imágen nuestra que quede bien para la tarjeta.
- Buscá alguna foto tuya que recortala para que quede cuadrada.
- Una vez que tenes la foto copiala a la carpeta `assets/images/` con el nombre `yo.png` (png o el formato que tengas).
- Vamos a crear otro componente `Image` para agregar nuestra imagen.
- Dado que esta es una imágen local podemos utilizar `require` y el path a nuestra foto `@/assets/images/yo.png`.
- Al poner la foto puede ser grande o chica y se va a mostrar según la imágen que usemos.
- Agreguemos estilo para que se vea mejor creando una nueva propiedad de estilo con el nombre `imagenPersonal`.
- Asignar a la nueva imágen el estilo `imagenPersonal` utilizando `styles` como hicimos en los otros componentes.
- Establecer el siguiente estilo a la propiedad `imagenPersonal`.

```javascript
{
  width: 200,
  height: 200,
  borderRadius: 100,
  borderWidth: 5,
  borderColor: "white",
  marginTop: -100,
},
```

- Si bien la imágen es local y React Native puede obtener el tamaño de la foto vamos a utilizar `width & height` para establecer el ancho y el alto de la imágen respectivamente. Le establecemos un valor de 200 a cada una de las propiedades.
- Luego para poder hacer que la imágen se vea como un círculo podemos establecer la propiedad `borderRadius` que hace que los bordes sean redondeados.
- Utilizamos un truquito de establcer el `borderRadius` a la mitad de valor que el ancho y alto para que se vea como un circulo. En este caso establecemos el valor 100.
- `borderWidth` permite establecer el valor del ancho del borde. Establecemos 5 como valor.
- `borderColor` permite establecer el color del border. Para que funcione debemos utilizar un ancho de borde y establecer el color. En este caso establecemos `white` para ver un lindo border blanco.
- Para poder terminar de generar un efecto lindo podemos mover la foto un poco de su posición para que quede superpuesta al banner utilizando `marginTop` y le asignamos un márgen negativo para mover la imágen para arriba. Establecer el valor `-100`.
- Si todo va bien deberíamos ver la imágen como un círculo y sobre el banner.
- Dado que es nuestra tarjeta personal vamos a crear uno iconos para mostrar nuestras redes socioales.
- Para esto vamos a tener que utilizar un componente nuevo que nos da Expo que se llam `FontAwesome6` del modulo `@expo/vector-icons`.
- El componente `FontAwesome6` tiene 3 propiedades:
  - `name`: es el nombre del icono que queremos mostrar.
  - `size`: nos permite establecer el tamaño del icono.
  - `color`: establece el color del icono.
- Para buscar el nombre de los iconos podemos utilizar el siguiente [sitio de expo](https://icons.expo.fyi/Index).

```javascript
<FontAwesome6 name="" size={} color="" />
```

- Debajo del componente que tiene el nombre agregamos otro `View` como contendor de nuestros iconos.
- Dentro del View vamos a poner 5 componentes de `FontAwesome6`.
- Al View le vamos a poner el siguiente estilo:

```javascript
{
  flexDirection: 'row',
  marginVertical: 10,
  gap: 10
}
```

- `flexboxDirection` establece que dirección tiene `flexbox` y en este caso vamos a poner un icono al lado del otro por eso utilizamos `row`.
- Luego utilizamos `gap` para distanciar los íconos uno del otro con el valor 10.
- Fianlmente establecemos un margen vertical utilizando `marginVertical` de 10 para distanciar los iconos del nombre.
- Creamos un nuevo estilo con el nombre `contenedorIconos` y asignamos el nuevo estilo.
- También tenemos que asignar `styles.contenedorIconos` al componente `View` en la propiedad `style`.
- Para los iconos utilizamos las siguientes propiedades:
  - `size` establecemos el valor en 24.
  - `color` vamos a utilizar `darkblue` para que se vean en azul oscuro.
  - `name`: a cada icono debemos darle un nombre diferente para que muestre diferentes iconos de redes sociales.
    - github
    - x-twitter
    - at
    - instagram
    - facebook
- También podemos cambiarle el color de texto al nombre agregando la propiedad `color: 'darkblue'` al estilo `title`.

```javascript
import {
  Text,
  SafeAreaView,
  StyleSheet,
  ScrollView,
  View,
  Image,
} from "react-native";
import { FontAwesome6 } from "@expo/vector-icons";

export default function Index() {
  return (
    <SafeAreaView style={styles.contenido}>
      <ScrollView>
        <View style={styles.contentContainer}>
          <Image
            source={{
              uri: "https://itspectrumsolutions.com/wp-content/uploads/2024/03/reactnative.jpg",
            }}
            style={styles.banner}
          />
          <Image
            source={require("@/assets/images/yo.png")}
            style={styles.imagenPersonal}
          />
          <Text style={styles.title}>Nicolas Isnardi</Text>

          <View style={styles.contenedorIconos}>
            <FontAwesome6 name="github" size={24} color="darkblue" />
            <FontAwesome6 name="x-twitter" size={24} color="darkblue" />
            <FontAwesome6 name="at" size={24} color="darkblue" />
            <FontAwesome6 name="instagram" size={24} color="darkblue" />
            <FontAwesome6 name="facebook" size={24} color="darkblue" />
          </View>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
  contentContainer: {
    flex: 1,
    backgroundColor: "white",
    alignItems: "center",
    justifyContent: "center",
  },
  title: { fontSize: 30, fontWeight: "bold", color: "darkblue" },
  banner: { width: "100%", aspectRatio: 16 / 9 },
  imagenPersonal: {
    width: 200,
    height: 200,
    borderRadius: 100,
    borderWidth: 5,
    borderColor: "white",
    marginTop: -100,
  },
  contenedorIconos: { flexDirection: "row", marginVertical: 10, gap: 10 },
});
```

- También debemos buscar alguna forma de que nos manden un mail y para eso podemos utilizar 2 componentes de React Native.
- Utilizamos `Button` para que el usuario pueda presionar.
- Vamos a tener que utilizar el evento `onPress` para manejar que alquien haga press en el boton.
- Luego al presionar deberíamos abrir la app de correo.
- Para esto podemos utilizar el componente que nos da `react-native` llamado `Linking` y el método `openURL`.
- Pasamos `mailto:` y tu dirección de email. Ejemeplo `mailto:nicolasisnardi@gmail.com`.
- Como title del botón podemos utilizar el string `Contacto`.
- Importemos el `Button` de `react-native`.
- Ponemos el componente `Button` debajo de los iconos.
- Creamos una nueva función que se llame `onContactoHandler` y le asignamos un arrow function.
- Luego tenemos que llamar a `Linking.openURL` y pasarle el mailto como parámetro.
- En el dispositivo esto abre el cliente de mail que tengan.
- En el simulador es posible que no haga nada.

```javascript
import {
  Text,
  SafeAreaView,
  StyleSheet,
  ScrollView,
  View,
  Image,
  Button,
  Linking,
} from "react-native";
import { FontAwesome6 } from "@expo/vector-icons";

export default function Index() {
  const onContactoHandler = () => {
    console.log("mailto:nicolasisnardi@gmail.com");

    Linking.openURL("mailto:nicolasisnardi@gmail.com");
  };

  return (
    <SafeAreaView style={styles.contenido}>
      <ScrollView>
        <View style={styles.contentContainer}>
          <Image
            source={{
              uri: "https://itspectrumsolutions.com/wp-content/uploads/2024/03/reactnative.jpg",
            }}
            style={styles.banner}
          />
          <Image
            source={require("@/assets/images/yo.png")}
            style={styles.imagenPersonal}
          />
          <Text style={styles.title}>Nicolas Isnardi</Text>

          <View style={styles.contenedorIconos}>
            <FontAwesome6 name="github" size={24} color="darkblue" />
            <FontAwesome6 name="x-twitter" size={24} color="darkblue" />
            <FontAwesome6 name="at" size={24} color="darkblue" />
            <FontAwesome6 name="instagram" size={24} color="darkblue" />
            <FontAwesome6 name="facebook" size={24} color="darkblue" />
          </View>

          <Button title="Conctacto" onPress={onContactoHandler} />
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
  contentContainer: {
    flex: 1,
    backgroundColor: "white",
    alignItems: "center",
    justifyContent: "center",
  },
  title: { fontSize: 30, fontWeight: "bold", color: "darkblue" },
  banner: { width: "100%", aspectRatio: 16 / 9 },
  imagenPersonal: {
    width: 200,
    height: 200,
    borderRadius: 100,
    borderWidth: 5,
    borderColor: "white",
    marginTop: -100,
  },
  contenedorIconos: { flexDirection: "row", marginVertical: 10, gap: 10 },
});
```

- Ahora podemos poner alguna breve descripción de nosotros mismos como una BIO.
- Para eso vamos a utilizar un componente `Text`.
- Creamos un nuevo estilo que se llame `bio` y le ponemos el siguiente estilo:

```javascript
{
  padding: 10,
  fontSize: 12,
  lineHeight: 18
}
```

- Agregams `bio` al nuevo componente Text en la propiedad `style` usando el objeto `styles`.
- Agregá algún texto que te describa de al menos 3, 4 lineas. Escribí lindas cosas sobre vos!
- Creamos otro componente de texto con el contenido `Experiencia`.
- Creamos un nuevo estilo con el nombre `experiencia` y le asignamos el siguiente estilo:

```javascript
{
  fontWeight: "bold",
  fontSize: 18,
  marginTop: 20,
  color: "darkblue",
}
```

- Nuestro código debería estar así:

```javascript
import {
  Text,
  SafeAreaView,
  StyleSheet,
  ScrollView,
  View,
  Image,
  Button,
  Linking,
} from "react-native";
import { FontAwesome6 } from "@expo/vector-icons";

export default function Index() {
  const onContactoHandler = () => {
    console.log("mailto:nicolasisnardi@gmail.com");

    Linking.openURL("mailto:nicolasisnardi@gmail.com");
  };

  return (
    <SafeAreaView style={styles.contenido}>
      <ScrollView>
        <View style={styles.contentContainer}>
          <Image
            source={{
              uri: "https://itspectrumsolutions.com/wp-content/uploads/2024/03/reactnative.jpg",
            }}
            style={styles.banner}
          />
          <Image
            source={require("@/assets/images/yo.png")}
            style={styles.imagenPersonal}
          />
          <Text style={styles.title}>Nicolas Isnardi</Text>

          <View style={styles.contenedorIconos}>
            <FontAwesome6 name="github" size={24} color="darkblue" />
            <FontAwesome6 name="x-twitter" size={24} color="darkblue" />
            <FontAwesome6 name="at" size={24} color="darkblue" />
            <FontAwesome6 name="instagram" size={24} color="darkblue" />
            <FontAwesome6 name="facebook" size={24} color="darkblue" />
          </View>

          <Button title="Conctacto" onPress={onContactoHandler} />
          <Text style={styles.bio}>
            Dirvertido programador que actualmente vive en Canadá. Me gusta
            mucho programar en React Native y enseñar esta tecnología.
          </Text>
          <Text style={styles.experiencia}>Experiencia</Text>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  contenido: {
    flex: 1,
  },
  contentContainer: {
    flex: 1,
    backgroundColor: "white",
    alignItems: "center",
    justifyContent: "center",
  },
  title: { fontSize: 30, fontWeight: "bold", color: "darkblue" },
  banner: { width: "100%", aspectRatio: 16 / 9 },
  imagenPersonal: {
    width: 200,
    height: 200,
    borderRadius: 100,
    borderWidth: 5,
    borderColor: "white",
    marginTop: -100,
  },
  contenedorIconos: { flexDirection: "row", marginVertical: 10, gap: 10 },
  bio: { padding: 10, fontSize: 12, lineHeight: 18 },
  experiencia: {
    fontWeight: "bold",
    fontSize: 18,
    marginTop: 20,
    color: "darkblue",
  },
});
```

- Para compartir toda nuestra experiencia vamos a crear una nueva lista `ScrollView`.
- Dentro de la lista vamos a poner nuestros trabajos.
