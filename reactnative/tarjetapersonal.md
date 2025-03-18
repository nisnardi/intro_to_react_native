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
    marginBottom: 10,
  },
});
```

- Dentro de la lista vamos a poner nuestros trabajos.
- Debajo del título de experiencia vamos a crear unas tarjetas con nuestras experiencias laborales.
- Para eso vamos a crear un contenedor con un componente `View` y le agregamos el siguiente estilo en linea (dentro de la propiedad style):

```javascript
{
  flex: 1,
  flexDirection: "row",
  alignItems: "flex-start",
  gap: 10,
  borderBottomColor: "#ddd",
  borderBottomWidth: 1,
  padding: 10,
}
```

- Establecemos `flexDirection: 'row` para decirle a flexbox que los próximos hijos tienen que estar uno al lado del otro de manera horizontal.
- Por medio de `alignItems: "flex-start"` le decimos a flexbox que alinie los componentes empezando de izquierda a derecha (porque tiene flex direction row).
- Con `gap` establecemos la distancia entre lo que va a ser una imágen y texto.
- Le agregamos un border inferior por medio de `borderBottomColor & borderBottomWidth` y le asignamos un color gris y un ancho de 1 pixel.
- Y finalmente le agregamos `padding: 10` para establecer un poco de aire o margen interno.

```javascript
<View
  style={{
    flex: 1,
    flexDirection: "row",
    alignItems: "flex-start",
    gap: 10,
    borderBottomColor: "#ddd",
    borderBottomWidth: 1,
    padding: 10,
  }}
></View>
```

- Dentro del view vamos a agregar un componente imagen.
- La idea es mostrar algún logo de la empresa donde trabajamos.
- Se puede sacar de Linkedin si la empresa está ahí o poner cualquier cosa.
- Creamos un componente `Image` con el siguiente estilo:

```javascript
{
  width: 80,
  height: 80
}
```

- Con esto establecemos que la imágen va a ser un cuadrado de 80 x 80.
- Ahora debemos establece la ruta del la imágen.
- Podemos utilizar la de ComIT con la siguiente URL: `https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c`
- Asignamos a la Imagen un objeto a la propiedad `source` donde la `uri` es la de ComIT.

```javascript
<Image
  style={{ width: 80, height: 80 }}
  source={{
    uri: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
  }}
/>
```

- Con esto se debería ver la imágen en nuestro componente.
- Ahora vamso a crear el detalle y para eso vamos a crearle su propia sección con un componente `View` y le asignamos el siguiente estilo:

```javascript
{
  flex: 1,
  flexDirection: "column"
}
```

- Nos debería quedar una estructura como esta:

```javascript
<View
  style={{
    flex: 1,
    flexDirection: "row",
    alignItems: "flex-start",
    gap: 10,
    borderBottomColor: "#ddd",
    borderBottomWidth: 1,
    padding: 10,
  }}
>
  <Image
    style={{ width: 80, height: 80 }}
    source={{
      uri: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
    }}
  />
  <View style={{ flex: 1, flexDirection: "column" }}></View>
</View>
```

- Acá vemos como se va formando esta nueva estructura donde tenemos un componente `View` padre que dentro tiene un Image y a la vez otra sección `View`.
- Los componentes internos se van a alinear uno al lado del otro pero para verlo tenemos que poner algún texto u otro componente.
- Creamos 5 componentes Text dentro del `View` que creamos en el paso anterior.

```javascript
<View style={{ flex: 1, flexDirection: "column" }}>
  <Text>Posición</Text>
  <Text>Empresa</Text>
  <Text>Fecha</Text>
  <Text>Locación</Text>
  <Text>Tecnologías</Text>
</View>
```

- Cada uno de estos textos van a tener información relevante a tu experiencia.
- Si por ahora no trabajaste en tecnolgía podes poner información sobre otros trabajos y adaptarlo.
- Agreguemos estilos para que los textos se vean mejor.
- Por cada tipo de texto vamos a crear un nuevo estilo en linea con los siguientes valores:
  - Posición: `{ fontWeight: "bold", fontSize: 14 }`.
  - Empresa: `{ fontSize: 12, lineHeight: 18 }`.
  - Fecha: `{ fontSize: 12, color: "#808080", lineHeight: 18 }`.
  - Locación: `{ fontSize: 12, color: "#808080", lineHeight: 18, marginBottom: 10}`.
  - Tecnologías: `{fontSize: 12,fontWeight: "bold",lineHeight: 18}`.
- Si todo va bien te debería quedar algo parecido a:

```javascript
<View
  style={{
    flex: 1,
    flexDirection: "row",
    alignItems: "flex-start",
    gap: 10,
    borderBottomColor: "#ddd",
    borderBottomWidth: 1,
    padding: 10,
  }}
>
  <Image
    style={{ width: 80, height: 80 }}
    source={{
      uri: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
    }}
  />
  <View style={{ flex: 1, flexDirection: "column" }}>
    <Text style={{ fontWeight: "bold", fontSize: 14 }}>Posición</Text>
    <Text style={{ fontSize: 12, lineHeight: 18 }}>Empresa</Text>
    <Text style={{ fontSize: 12, color: "#808080", lineHeight: 18 }}>
      Fecha
    </Text>
    <Text
      style={{
        fontSize: 12,
        color: "#808080",
        lineHeight: 18,
        marginBottom: 10,
      }}
    >
      Locación
    </Text>
    <Text
      style={{
        fontSize: 12,
        fontWeight: "bold",
        lineHeight: 18,
      }}
    >
      Tecnologías
    </Text>
  </View>
</View>
```

- Ahora puedes completar estos textos con tu información y deberías ver una tarjeta en pantalla con los datos.
- Una práctica buena ahora sería tratar de crear 2, 3, 4 componentes de esto para ver como quedan.
- Podes hacer copy and paste y preparate para que el código sea largo y que se te pueda romper.
- Es un buen momento para hacer un `git commit` antes de seguir :).
- Hacemos esta práctica para darnos cuenta que esto debería estar en otro archivo y que tiene que haber una mejor forma de manejar componentes.
- Como ya tenemos nuestra pantalla inicial ahora vamos a hacer un refactor para cambiar / mejorar el código.
- Creamos una nueva carpeta con el nombre `components` a la altura de la carpeta `app`.
- Dentro de la carpeta `components` vamos a crear un nuevo archivo con el nombre `TarjetaExperiencia.tsx`.
- Creamos un componente vacío con la tarjeta.

```javascript
import React from "react";
import { View, Text } from "react-native";

export const TarjetaExperiencia = () => {
  return (
    <View>
      <Text>Tarjeta Experiencia</Text>
    </View>
  );
};
```

- Ahora vamos a copiar todo el código de la tarjeta desde el `View` que tiene todos los otros componentes adentro.
- Se va a romper el código, van a faltar imports y todo eso pero ya lo vamos a arreglar.
- Lo primero que React Native se queja es que nos falta importar `Image` por lo cual lo podemos hacer en donde importamos `View and Text`.
- Con eso solo ya tenemos el componente en mejor estado.
- El componente `TarjetaExperiencia` debería quedar algo así:

```javascript
import React from "react";
import { View, Text, Image } from "react-native";

export const TarjetaExperiencia = () => {
  return (
    <View
      style={{
        flex: 1,
        flexDirection: "row",
        alignItems: "flex-start",
        gap: 10,
        borderBottomColor: "#ddd",
        borderBottomWidth: 1,
        padding: 10,
      }}
    >
      <Image
        style={{ width: 80, height: 80 }}
        source={{
          uri: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
        }}
      />
      <View style={{ flex: 1, flexDirection: "column" }}>
        <Text style={{ fontWeight: "bold", fontSize: 14 }}>Posición</Text>
        <Text style={{ fontSize: 12, lineHeight: 18 }}>Empresa</Text>
        <Text style={{ fontSize: 12, color: "#808080", lineHeight: 18 }}>
          Fecha
        </Text>
        <Text
          style={{
            fontSize: 12,
            color: "#808080",
            lineHeight: 18,
            marginBottom: 10,
          }}
        >
          Locación
        </Text>
        <Text
          style={{
            fontSize: 12,
            fontWeight: "bold",
            lineHeight: 18,
          }}
        >
          Tecnologías
        </Text>
      </View>
    </View>
  );
};
```

- Todo muy lindo pero perdimos el contenido de la tarjeta en nuestra pantalla principal.
- Esto pasa porque todavía no importamos y renderizamos el nuevo componente.
- Para hacer esto hacemos un import de `TarjetaExperiencia` en el archivo `index.tsx`.
- Luego tenemos que agregar el nuevo componente donde estaba el código anterior de la siguiente manera <TarjetaExperiencia />
- Si agregamos bien la tarjeta deberíamos ver en pantalla lo mismo que veíamos antes de sacarlo.
- Podemos trabajar un poco más en el componente `TarjetaExperiencia` para limpiar un poco el código y hacerlo más dinámico.
- Primero vamos a sacar todos los estilos y ponerlos en un nuevo objeto de estilo usando `StyleSheet`.
- Importamos `StyleSheet` en el componente `TarjetaExperiencia`.
- Creamos la variable `styles` y le asignamos `StyleSheet.create({})` como hicimos con el componente `index`.
- Primero creamos un estilo `contenedor` y le asignamos el estilo del `View` que tiene toda la tarjeta.
- Asignamos `styles.contenedor` a la propiedad `style` del componente `View`.

```javascript
// Esto es sólo un ejemplo de como debería quedar el componente View.
<View style={styles.contenedor}>

// Este código está abajo de todo en tu archivo
const styles = StyleSheet.create({
  contenedor: {
    flex: 1,
    flexDirection: "row",
    alignItems: "flex-start",
    gap: 10,
    borderBottomColor: "#ddd",
    borderBottomWidth: 1,
    padding: 10,
  },
});
```

- Ahora podemos seguir haciendo estos mismos pasos para cada componente `Text`.
- Vamos a crear una propiedad del objeto estilo con el nombre que tiene cada texto sin acentos ni nada ya que son variables de JavaScript.
- Pegamos el estilo que tiene cada `Text` en la propiedad `style` dentro del objeto `styles`.
- Luego remplazamos el valor de la propiedad `style` de cada componente `Text` por el valor correspondiente en `styles.nombre_de_tu_text`.

```javascript
<Text style={styles.posicion}>Posición</Text>
<Text style={styles.empresa}>Empresa</Text>
<Text style={styles.fecha}>Fecha</Text>
<Text style={styles.locacion}>Locación</Text>
<Text style={styles.tecnologias}>Tecnologiás</Text>
```

- Ahora podemos mover el estilo del contenedor de los `Text` para seguir limpiando el código y separar contenido de atributos visuales.
- El gran problema es que nombre ponerle a este estilo?.
- Creamos un nuevo estilo con el nombre de `contenedorDeContenido` y le asignamos el estilo que tiene el `View` que es padre de todos los `Text`.

```javascript
<View style={styles.contenedorDeContenido}>
  <Text style={styles.posicion}>Posición</Text>
  <Text style={styles.empresa}>Empresa</Text>
  <Text style={styles.fecha}>Fecha</Text>
  <Text style={styles.locacion}>Locación</Text>
  <Text style={styles.tecnologias}>Tecnologiás</Text>
</View>;

const styles = StyleSheet.create({
  contenedor: {
    flex: 1,
    flexDirection: "row",
    alignItems: "flex-start",
    gap: 10,
    borderBottomColor: "#ddd",
    borderBottomWidth: 1,
    padding: 10,
  },
  contenedorDeContenido: { flex: 1, flexDirection: "column" },
  posicion: { fontWeight: "bold", fontSize: 14 },
  empresa: { fontSize: 12, lineHeight: 18 },
  fecha: { fontSize: 12, color: "#808080", lineHeight: 18 },
  locacion: {
    fontSize: 12,
    color: "#808080",
    lineHeight: 18,
    marginBottom: 10,
  },
  tecnologias: {
    fontSize: 12,
    fontWeight: "bold",
    lineHeight: 18,
  },
});
```

- Genial, esto va tomando forma!!! Vamooooooooo.
- El único estilo que queda es el de la imágen, podemos también mover el estilo al objeto con estilos.
- Creamos un nuevo estilo con el nombre `logo` y le asignamos el estilo que tiene el componente `Image`.

```javascript
import React from "react";
import { View, Text, Image, StyleSheet } from "react-native";

export const TarjetaExperiencia = () => {
  return (
    <View style={styles.contenedor}>
      <Image
        style={styles.logo}
        source={{
          uri: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
        }}
      />
      <View style={styles.contenedorDeContenido}>
        <Text style={styles.posicion}>Posición</Text>
        <Text style={styles.empresa}>Empresa</Text>
        <Text style={styles.fecha}>Fecha</Text>
        <Text style={styles.locacion}>Locación</Text>
        <Text style={styles.tecnologias}>Tecnologiás</Text>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  contenedor: {
    flex: 1,
    flexDirection: "row",
    alignItems: "flex-start",
    gap: 10,
    borderBottomColor: "#ddd",
    borderBottomWidth: 1,
    padding: 10,
  },
  logo: { width: 80, height: 80 },
  contenedorDeContenido: { flex: 1, flexDirection: "column" },
  posicion: { fontWeight: "bold", fontSize: 14 },
  empresa: { fontSize: 12, lineHeight: 18 },
  fecha: { fontSize: 12, color: "#808080", lineHeight: 18 },
  locacion: {
    fontSize: 12,
    color: "#808080",
    lineHeight: 18,
    marginBottom: 10,
  },
  tecnologias: {
    fontSize: 12,
    fontWeight: "bold",
    lineHeight: 18,
  },
});
```

- Hermoso! miren como va quedando ese componente, super limpio!
- Si bien hicimos un montón de trabajo buen todavía nos quedan un par de cosas.
- Podemos crear una constante con el tamaño de la imagen ya que es un valor que se repite y no cambia.
- En la parte superior, afuera de la declaración del componente creamos una variable con el nombre `SIZE` y le asignamos 80.
- Luego cambiamos el valor en el estilo del logo.

```javascript
// En la parte superior de tu componente entre la declaración del componente y los imports.
const SIZE = 80;

// En el objeto estilo
logo: { width: SIZE, height: SIZE },
```

- Ahora nos queda hacer el componente dinámico.
- Sólo nos queda hacer este componente dinámico.
- Para eso vamos a crear un objeto debajo de la variable SIZE con el nombre de experiencia.
- El objeto tiene la siguiente forma y valores:

```javascript
const experiencia = {
  logo: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
  posicion: "Posición",
  empresa: "Empresa",
  fecha: "Fecha",
  locacion: "Locación",
  tecnologias: "Tecnologiás",
};
```

- Finalmente vamos a remplazar los valores de los componentes por los valores del objeto `experiencia`.

```javascript
import React from "react";
import { View, Text, Image, StyleSheet } from "react-native";

const SIZE = 80;

const experiencia = {
  logo: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
  posicion: "Posición",
  empresa: "Empresa",
  fecha: "Fecha",
  locacion: "Locación",
  tecnologias: "Tecnologiás",
};

export const TarjetaExperiencia = () => {
  return (
    <View style={styles.contenedor}>
      <Image
        style={styles.logo}
        source={{
          uri: experiencia.logo,
        }}
      />
      <View style={styles.contenedorDeContenido}>
        <Text style={styles.posicion}>{experiencia.posicion}</Text>
        <Text style={styles.empresa}>{experiencia.empresa}</Text>
        <Text style={styles.fecha}>{experiencia.fecha}</Text>
        <Text style={styles.locacion}>{experiencia.locacion}</Text>
        <Text style={styles.tecnologias}>{experiencia.tecnologias}</Text>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  contenedor: {
    flex: 1,
    flexDirection: "row",
    alignItems: "flex-start",
    gap: 10,
    borderBottomColor: "#ddd",
    borderBottomWidth: 1,
    padding: 10,
  },
  logo: { width: SIZE, height: SIZE },
  contenedorDeContenido: { flex: 1, flexDirection: "column" },
  posicion: { fontWeight: "bold", fontSize: 14 },
  empresa: { fontSize: 12, lineHeight: 18 },
  fecha: { fontSize: 12, color: "#808080", lineHeight: 18 },
  locacion: {
    fontSize: 12,
    color: "#808080",
    lineHeight: 18,
    marginBottom: 10,
  },
  tecnologias: {
    fontSize: 12,
    fontWeight: "bold",
    lineHeight: 18,
  },
});
```

- Excelente, esto va quedando cada ver mejor.
- Ahora.. Ahora.. un cambio más!!! Y si, no nos vamos a quedar acá!!
- Que tal si en lugar de utilizar este objeto experiencia no le pasamos al componente estos valores por.. PROPS!!!

```javascript
export const TarjetaExperiencia = ({
  logo,
  posicion,
  empresa,
  fecha,
  locacion,
  tecnologias,
}) => {
```

- Luego remplazamos estos valores por las propiedades del objeto experiencia:

```javascript
import React from "react";
import { View, Text, Image, StyleSheet } from "react-native";

const SIZE = 80;

const experiencia = {
  logo: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
  posicion: "Posición",
  empresa: "Empresa",
  fecha: "Fecha",
  locacion: "Locación",
  tecnologias: "Tecnologiás",
};

export const TarjetaExperiencia = ({
  logo,
  posicion,
  empresa,
  fecha,
  locacion,
  tecnologias,
}) => {
  return (
    <View style={styles.contenedor}>
      <Image
        style={styles.logo}
        source={{
          uri: logo,
        }}
      />
      <View style={styles.contenedorDeContenido}>
        <Text style={styles.posicion}>{posicion}</Text>
        <Text style={styles.empresa}>{empresa}</Text>
        <Text style={styles.fecha}>{fecha}</Text>
        <Text style={styles.locacion}>{locacion}</Text>
        <Text style={styles.tecnologias}>{tecnologias}</Text>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  contenedor: {
    flex: 1,
    flexDirection: "row",
    alignItems: "flex-start",
    gap: 10,
    borderBottomColor: "#ddd",
    borderBottomWidth: 1,
    padding: 10,
  },
  logo: { width: SIZE, height: SIZE },
  contenedorDeContenido: { flex: 1, flexDirection: "column" },
  posicion: { fontWeight: "bold", fontSize: 14 },
  empresa: { fontSize: 12, lineHeight: 18 },
  fecha: { fontSize: 12, color: "#808080", lineHeight: 18 },
  locacion: {
    fontSize: 12,
    color: "#808080",
    lineHeight: 18,
    marginBottom: 10,
  },
  tecnologias: {
    fontSize: 12,
    fontWeight: "bold",
    lineHeight: 18,
  },
});
```

- Todo muy lindo pero se fueron todos los valores de la pantalla.
- Esto es porque tenemos que pasarle los valores al componente utilizando las propiedades desde el componente `index`.
- Cortamos el objeto `experiencia` y lo pegamos en el componente index en la parte superior abajo de los imports.
- Luego tenemos que pasarle al componente `TarjetaExperiencia` cada una de las propiedades que espera.

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

// Importamos el componente
import { TarjetaExperiencia } from "@/components/TarjetaExperiencia";

// Movemos el objeto con la data
const experiencia = {
  logo: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
  posicion: "Posición",
  empresa: "Empresa",
  fecha: "Fecha",
  locacion: "Locación",
  tecnologias: "Tecnologiás",
};

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
          {
            // Utilizamos el componente pasando los datos
          }
          <TarjetaExperiencia
            logo={experiencia.logo}
            posicion={experiencia.posicion}
            empresa={experiencia.empresa}
            fecha={experiencia.fecha}
            locacion={experiencia.locacion}
            tecnologias={experiencia.tecnologias}
          />
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
  contenedorIconos: { flexDirection: "row", marginVertical: 10, gap: 15 },
  bio: { fontSize: 12, lineHeight: 18 },
  experiencia: {
    fontWeight: "bold",
    fontSize: 18,
    marginTop: 20,
    color: "darkblue",
    marginBottom: 10,
  },
});
```

- Ya tenemos todo como para terminar este proyecto.
- Nos falta poder mostrar más de una experiencia.
- Para eso vamos a cambiar el objeto experiencia por una colección de experiencias.
- Creamos una variable `experiencias` y le asignamos un array.
- Dentro de la asignación de la variable `experiencias` le vamos a agregar el objeto experiencia.

```javascript
const experiencias = [
  {
    logo: "https://media.licdn.com/dms/image/v2/C560BAQFoMbh8Jawjhg/company-logo_100_100/company-logo_100_100/0/1631338342207?e=1749081600&v=beta&t=6fgq4Zi_lslt6EwSEinoOUmyLfOT2qaNu9C_ny94y9c",
    posicion: "Profesor React Native",
    empresa: "ComIt",
    fecha: "Enero 2025 - Actualidad",
    locacion: "Latam",
    tecnologias: "React Native, Redux, JavaScript, TypeScript, Jest, Maestro",
  },
];
```

- Luego tenemos que iterar esta nueva colección creando un nuevo componente `TarjetaExperiencia` por cada item de la colección experiencias.
- Podemos hacer esto creando una función que se llame `renderExperiencias` en la cual vamos a retornar el resultado de iterar la colección con map y pasar los valores del item como propiedades del componente.

```javascript
const renderExperiencias = () =>
  experiencias.map((experiencia, index) => {
    return (
      <TarjetaExperiencia
        key={`${index}-${experiencia.empresa}-${experiencia.posicion}`}
        logo={experiencia.logo}
        posicion={experiencia.posicion}
        empresa={experiencia.empresa}
        fecha={experiencia.fecha}
        locacion={experiencia.locacion}
        tecnologias={experiencia.tecnologias}
      />
    );
  });
```

- Creamos la función y devolvemos el resultado de utilizar `map` para recorrer la colección de `experiencias`.
- Dado que cada item de la colección es una `experiencia` podemos utilizar esos valores para crear un nuevo componente y pasar los datos como propiedades.
- Como estamos iterando una colección necesitamos decirle a React Native que `key` utilizar.
- Creamos una key utilizando el valor de la variable `index` que nos da map junto con el puesto y la empresa.
- Esto hace la key bastante único.
- Ahora queda agregar más experiencias a la colección y dejar que React y React Native hagan su magia.
- Agrega algunas experiencias nuevas o las que te gustarían tener.
- Dado que la colección `experiencias` ocupa mucho lugar en el código vamos a moverlo a su propio móddulo y exportarlo.
- Creamos una nueva carpeta con el nombre `data` y dentro creamos un archivo con el nombre `experiencia.ts`
- Cortamos y pegamos el código actual en el archivo nuevo.

```javascript
// data/experiencias.ts
export const experiencias = [
  // Tus experiencias
];
```

- Una vez creado el archivo y poner nuestra experiencia vamos a importar el archivo de datos en la pantalla `index.ts`.

```javascript
// Agregamos el siguiente import en el archivo index.tsx
import { experiencias } from "@/data/experiencias";
```

- Dado que importamos la colección deberíamos ver la aplicación corriendo bien de nuevo.
- Y que tal si le agregamos un poco de TypeScript a nuestro código.
- Sabemos la forma que tiene el objeto `experiencia` y sabemos que la colección `experiencias` tiene items del mismo tipo.

```javascript
// experiencias.ts
interface Experiencia {
  logo: string;
  posicion: string;
  empresa: string;
  fecha: string;
  locacion: string;
  tecnologias: string;
}

export const experiencias: Experiencia[] = [
  // Tus experiencias
];
```

- Podemos crear una interface con el nombre `Experiencia` donde definimos todas las propiedades como `string`.
- Una vez que tenemos la interface podemos decirle a `TS` que la colección experiencias es del tipo `Experiencia[]` para que sepa que cada item es una `Experiencia`.
- También podemos definir las propiedades del componente `TarjetaExperiencia`.
- Agreguemos la estructura de las propiedades.

```javascript
// components/TarjetaExperiencia.tsx
interface TarjetaExperiencia {
  logo: string;
  posicion: string;
  empresa: string;
  fecha: string;
  locacion: string;
  tecnologias: string;
}
```

- De la siguiente forma podemos decirle a `TS` cuales es la estructura de sus propiedades:

```javascript
export const TarjetaExperiencia = ({
  logo,
  posicion,
  empresa,
  fecha,
  locacion,
  tecnologias,
}: TarjetaExperiencia) => {
  // Código del componente
};
```

- Por medio de `: TipoDeDato` le decimos a TS que este componente tiene las siguientes propiedades.
- De esta forma TypeScript sabe como ayudarnos a la hora de escribir código en nuestro componente o como utilizarlo.
- Para seguir limpiando el componente `index.tsx` podríamos sacar la sección de los iconos a su propio componente.
- Creamos un nuevo archivo dentr de la carpeta `componentes` con el nombre de `Iconos.tsx`.

```javascript
// components/Iconos.tsx
import React from "react";
import { View, StyleSheet } from "react-native";
import { FontAwesome6 } from "@expo/vector-icons";

export const Iconos = () => {
  return (
    <View style={styles.contenedorIconos}>
      <FontAwesome6 name="github" size={24} color="darkblue" />
      <FontAwesome6 name="x-twitter" size={24} color="darkblue" />
      <FontAwesome6 name="at" size={24} color="darkblue" />
      <FontAwesome6 name="instagram" size={24} color="darkblue" />
      <FontAwesome6 name="facebook" size={24} color="darkblue" />
    </View>
  );
};

const styles = StyleSheet.create({
  contenedorIconos: { flexDirection: "row", marginVertical: 10, gap: 15 },
});
```

- Movemos el código del componente `index.tsx` al nuevo componente.
- Luego tenemos que importar el componente `Iconos` en nuestra pantalla y utilizarlo.

```javascript
// app/index.tsx
import { Iconos } from "@/components/Iconos";

// Dentro del componente Index
<Iconos />;
```

- Agregamos el componente `Index` donde estában los iconos antes.
- La aplicación debería seguir funcionando como siempre.
- Podemos borrar las dependencias que no se utilizan en `index.tsx` como `FontAwesome6`.
- Para finalizar vamos a agregar una funcionalidad donde definimos que hacer cuando el usuario presione cada uno de los iconos.
- Vamos a utilizar un concepto que ya conocemos trabajando en el archivo / componente `components/Iconos.tsx`.
- React Native tiene un componente que se llama `Pressable` que nos permite agregar manejadores de eventos `press`.
- Importamos Pressable de react-native.
- Creamos un componente `Pressable` para que sea padre de cada componente `FontAwesome6`.
- Le agregamos una propiedad `onPress` y le asignamos una arrow function.

```javascript
(
  <Pressable onPress={() => {}}>
    <FontAwesome6 name="github" size={24} color="darkblue" />
  </Pressable>
)``;
```

- Hacer esto por cada componente `FontAwesome6`.
- Luego podemos definir que este componente va a recibir una función como propiedad para manejar el evento press de cada icono.

```javascript
export const Iconos = ({
  onGithubPress,
  onTwitterPress,
  onAtPress,
  onInstagramPress,
  onFacebookPress,
}: IconosProps) => {
  // Código del componente
};
```

- Dado que definimos las propiedades podemos remplazar las arrow functions por el event handler correspondiente.

```javascript
<Pressable onPress={onGithubPress}>
  <FontAwesome6 name="github" size={24} color="darkblue" />
</Pressable>
<Pressable onPress={onTwitterPress}>
  <FontAwesome6 name="x-twitter" size={24} color="darkblue" />
</Pressable>
<Pressable onPress={onAtPress}>
  <FontAwesome6 name="at" size={24} color="darkblue" />
</Pressable>
<Pressable onPress={onInstagramPress}>
  <FontAwesome6 name="instagram" size={24} color="darkblue" />
</Pressable>
<Pressable onPress={onFacebookPress}>
  <FontAwesome6 name="facebook" size={24} color="darkblue" />
</Pressable>
```

- Como tiene que hacer podemos agregar tipos de datos a nuestro componente `Iconos` de la siguiente manera:

```javascript
interface IconosProps {
  onGithubPress: () => void;
  onTwitterPress: () => void;
  onAtPress: () => void;
  onInstagramPress: () => void;
  onFacebookPress: () => void;
}
export const Iconos = ({
  onGithubPress,
  onTwitterPress,
  onAtPress,
  onInstagramPress,
  onFacebookPress,
}: IconosProps) => {
  // Código del componente
};
```

- En este caso las propiedades que va a recibir este componente son funciones que al ser ejecutadas no retornan ningún valor.
- Es por esto que podemos utilizar `propiedad: () => void` como definición de cada event handler que queremos pasar como propiedad.
- Luego agregamos `IconosProps` como tipo de estructura de las propiedades del componente `Iconos`.
- Seguro VS Code está mostrando un error o linea roja debajo del componente `Iconos` en el componente `index.tsx` ya que nos pide que le pasemos las propiedades esperadas.
- Vamos a agregar una función por cada event handler en el componente `index.tsx`.

```javascript
const onGithubPressHandler = () => {
  console.log("Github");
};
const onTwitterPressHandler = () => {
  console.log("Twitter");
};
const onAtPressHandler = () => {
  console.log("Mail");
};
const onInstagramPressHandler = () => {
  console.log("Instagram");
};
const onFacebookPressHandler = () => {
  console.log("Facebook");
};
```

- Ya que tenemos la definición las podemos pasar como propiedades del componente `Iconos`.
- La idea es que cuando el usuario presione en cada icono se vea el mensaje en pantalla.
- Tenemos todo configurado sólo nos queda utilizar `Linking.openURL` para abrir cada sitio.
- Busca en el navegador cual es la URL de tu profile de cada red social.
- Para el mail vamos a utilizar el mismo código que tenemos en el botón contacto.

```javascript
const onGithubPressHandler = () => {
  Linking.openURL("URL GITHUB");
};
const onTwitterPressHandler = () => {
  Linking.openURL("URL TWITTER");
};
const onAtPressHandler = () => {
  Linking.openURL("mailto:tuemail@dominio.com");
};
const onInstagramPressHandler = () => {
  Linking.openURL("URL INSTAGRAM");
};
const onFacebookPressHandler = () => {
  Linking.openURL("URL FACEBOOK");
};
```

- Ahora cuando el usuario presiona cada uno de los iconos el dispositivo abre un browser o navegador y navega al sitio indicado.
- Hay una buena práctica que es comunicar al usuario cuando pasa algo.
- Es por esto que podemos configurar al componente `Pressable` para que muestre alguna reacción cuando el usuario presiona el icono.

```javascript
<Pressable onPress={onGithubPress}>
  {({ pressed }) => (
    <FontAwesome6
      name="github"
      size={24}
      color={pressed ? "blue" : "darkblue"}
    />
  )}
</Pressable>
```

- Pressable tiene una sintáxis medio rara donde le podemos pasar una función como child con un parámetro.
- Este parámetro es un valor booleano (true / false) que nos dice si el Pressable fue presionado.
- Con esto podemos cambiar tanto el estilo del `Pressable` como algo en su hijo.
- En nuestro caso podemos modificar el color del icono.
- De esta forma cuando el usuario presiona el icono ve algún tipo de reacción que dice que algo va a pasar.
- Agrega esta funcionalidad para cada icono.
- Al finalizar esta tarea podemos ver que todos los iconos tienen el mismo tamaño, colores, utilizan un callback.
- Que tal si lo extraemos en su propio componente? Buena idea!!!
- Creamos otro componente con el nombre de `Icono.tsx` en la carpeta `components`.

```javascript
// components/Icono.tsx
import React from "react";
import { Pressable } from "react-native";
import { FontAwesome6 } from "@expo/vector-icons";

interface IconoProps {
  icon: "github" | "x-twitter" | "at" | "instagram" | "facebook";
  size: number;
  color: string;
  activeColor: string;
  onPress: () => void;
}

export const Icono = ({
  icon,
  size,
  color,
  activeColor,
  onPress,
}: IconoProps) => {
  return (
    <Pressable onPress={onPress}>
      {({ pressed }) => (
        <FontAwesome6
          name={icon}
          size={size}
          color={pressed ? activeColor : color}
        />
      )}
    </Pressable>
  );
};
```

- En este componente utilizamos el código que teníamos para cada uno de los iconos.
- Dado que las propiedades son las mismas podemos crear un tipo de estructura que se llame `IconoProps`.
- Para la propiedad `icono` utilizamos algunos nombres de icono para limitar las opciones, sino podemos utilizar string.
- Luego agregamos el tipo de propiedades del componente con `: IconoProps`.
- Finalmente utilizamos las propiedades en el componente.
- En el componente `Iconos.tsx` debemos importar el `Icono` y utilizarlo para cada botón.

```javascript
import React from "react";
import { View, StyleSheet, Pressable } from "react-native";
import { Icono } from "@/components/Icono";

interface IconosProps {
  onGithubPress: () => void;
  onTwitterPress: () => void;
  onAtPress: () => void;
  onInstagramPress: () => void;
  onFacebookPress: () => void;
}

export const Iconos = ({
  onGithubPress,
  onTwitterPress,
  onAtPress,
  onInstagramPress,
  onFacebookPress,
}: IconosProps) => {
  return (
    <View style={styles.contenedorIconos}>
      <Icono
        icon="github"
        size={24}
        color="darkblue"
        activeColor="blue"
        onPress={onGithubPress}
      />
      <Icono
        icon="x-twitter"
        size={24}
        color="darkblue"
        activeColor="blue"
        onPress={onTwitterPress}
      />
      <Icono
        icon="at"
        size={24}
        color="darkblue"
        activeColor="blue"
        onPress={onAtPress}
      />
      <Icono
        icon="instagram"
        size={24}
        color="darkblue"
        activeColor="blue"
        onPress={onInstagramPress}
      />
      <Icono
        icon="facebook"
        size={24}
        color="darkblue"
        activeColor="blue"
        onPress={onFacebookPress}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  contenedorIconos: { flexDirection: "row", marginVertical: 10, gap: 15 },
});
```

- Se ve claramente que `size, color y activeColor` son los mismos valores para todos por lo cual los podemos utilizar como valors por defecto.

```javascript
// components/Iconos.tsx
import React from "react";
import { View, StyleSheet, Pressable } from "react-native";
import { Icono } from "@/components/Icono";

interface IconosProps {
  onGithubPress: () => void;
  onTwitterPress: () => void;
  onAtPress: () => void;
  onInstagramPress: () => void;
  onFacebookPress: () => void;
}

export const Iconos = ({
  onGithubPress,
  onTwitterPress,
  onAtPress,
  onInstagramPress,
  onFacebookPress,
}: IconosProps) => {
  return (
    <View style={styles.contenedorIconos}>
      <Icono icon="github" onPress={onGithubPress} />
      <Icono icon="x-twitter" onPress={onTwitterPress} />
      <Icono icon="at" onPress={onAtPress} />
      <Icono icon="instagram" onPress={onInstagramPress} />
      <Icono icon="facebook" onPress={onFacebookPress} />
    </View>
  );
};

const styles = StyleSheet.create({
  contenedorIconos: { flexDirection: "row", marginVertical: 10, gap: 15 },
});
```

- Sacamos las propiedades repetidas y las movemos a la definición del componente icono como propiedades por default.

```javascript
// components/Iconos.tsx
import React from "react";
import { Pressable } from "react-native";
import { FontAwesome6 } from "@expo/vector-icons";

interface IconoProps {
  icon: "github" | "x-twitter" | "at" | "instagram" | "facebook";
  size?: number;
  color?: string;
  activeColor?: string;
  onPress: () => void;
}

export const Icono = ({
  icon,
  size = 24,
  color = "darkblue",
  activeColor = "blue",
  onPress,
}: IconoProps) => {
  return (
    <Pressable onPress={onPress}>
      {({ pressed }) => (
        <FontAwesome6
          name={icon}
          size={size}
          color={pressed ? activeColor : color}
        />
      )}
    </Pressable>
  );
};
```

- Dado que las propiedades ahora son opcionales podemos definirlas utilizando `?` en TypeScript.
- Agregamos el valor por default para las propiedades `size=24`, `color="darkblue"` y `activeColor="blue"`
- Si queremos podemos pasar otro color o tamaño al utilizar el `Icon` pero sino se utilizan los valores por default.
- Podes aprender más sobre `Pressable` leyendo la [documentación oficial](https://reactnative.dev/docs/pressable)
- Con esto damos por terminado nuestro primer proyecto aprendiendo un montón de cosas en el camino!
- Congrats!!!

![Congrats](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExaDkycjNzNHZyNmE5bnp2emhhdWRzYXhzZzlpYmc3dTFpM2dkZjkybiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/jJQC2puVZpTMO4vUs0/giphy.gif)

![App de ejemplo](https://github.com/nisnardi/rn_tarjeta_personal)
