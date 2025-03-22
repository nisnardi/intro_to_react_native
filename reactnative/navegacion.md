# React Native

## Navegación - Expo Router

- `expo-router` es un sistema de navegación para React Native (Expo) basado en archivos.
- Permite organizar la navegación utilizando una estructura de carpetas.
- La navegación está determinada por la estructura de archivos y carpetas dentro del directorio `app/`.
- **Rutas anidadas**: podemos crear pantallas dentro de subdirectorios para estructurar la navegación.
- **Rutas Dinámicas**: también podemos crear pantallas que acepten parámetros usando corchetes ([id].tsx) en los nombres de archivos.
- `_layout.tsx` nos permite configurar las pantallas y estructura de navegación. También es un buen lugar para agregar providers como pueden ser de Redux, Theme o estilos para que lleguen a todos los componentes de nuestra aplicación.
- `Link` es un componente que nos da expo-router para navegar de una pantalla a la otra. Utiliza la propiedad `href` para saber a donde ir. Las rutas en expo-router están tipadas lo que significa que TypeScript y expo-router nos ayudan a no equivocarnos a la hora de definir a donde navegar.

### Navegación Simple

- `Stack` proporciona una forma de transición entre pantallas en la que cada nueva pantalla se coloca encima de una pila.
- Creamos un sistema de Navegación `Stack` básico.

```bash
app/
  |_ _layout.tsx
  |_ about.tsx
  |_ index.tsx
```

- En este ejemplo vamos a crear 2 Pantallas o Páginas como las llama expo-router.
- `index` y `about` están en el mismo navegador ya que están al mismo nivel de estructura de archivos y definidos en `_layout.tsx`.
- `index.tsx` matchea con la ruta `/` donde es el documento raíz de la ruta principal.
- `about.tsx` matchea con la ruta `/about` donde se utiliza el mismo nombre de ruta / archivo pero en la raíz de la ruta principal.

```javascript
// app/_layout.tsx
import { Stack } from "expo-router";

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="index" options={{ title: "Root Layout - Home" }} />
      <Stack.Screen name="about" options={{ title: "Root Layout - Other" }} />
    </Stack>
  );
}
```

- Si bien expo-router puede definir rutas usando sólo los archivos `_layout.tsx` nos permite definir las rutas y configurarlas.
- En este ejemplo estamos usando `Stack.Screen` para definir 2 componentes rutas con el nombre de `index` y `about`.
- También ambas rutas usan la propiedad `options` para definir propiedades sobre como tienen que funcionar estas pantallas.
- Usando `options.title` podemos establecer el título de la pantalla que se verá en el header de la pantalla.
- Ahora podemos crear las pantallas:

```javascript
// app/index.tsx
import { Link } from "expo-router";
import { Text, View, StyleSheet } from "react-native";

export default function Index() {
  return (
    <View style={styles.container}>
      <Link href="/about" dismissTo>
        Navegar a About
      </Link>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- `Link`: es un componente que nos da expo-router y que tiene una propiedad `href` que nos permite pasarle como valor la ruta donde queremos navegar.
- `index.tsx` usa `Link` para navegar desde la pantalla principal a `about.tsx`.
- Link usa la propiedad `href` y le pasamos el nombre de la ruta a la que queremos navegar.
- Ahora creamos la pantalla `about.tsx`:

```javascript
import { Link } from "expo-router";
import { View, StyleSheet } from "react-native";

export default function About() {
  return (
    <View style={styles.container}>
      <Link href="/">Navegar a Home</Link>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- `about.tsx` es bien parecida a `index.tsx` ya que sólo tiene un link para navegar a `index.tsx`.
- Usamos nuevamente el componente `Link` y la propiedad `href` para establecer a donde queremos navegar.
- En este caso como queremos navegar a la raíz de nuestro sistema de navegación usamos `/` para navegar a `index.tsx`.
- Otra forma de navegar de una pantalla a la otra es usando el objeto `router` que nos da expo-router.

```javascript
import { View, StyleSheet, Button } from "react-native";
import { Link, router } from "expo-router";

export default function About() {
  const navegarAHome = () => {
    router.navigate("/");
  };

  return (
    <View style={styles.container}>
      <Link href="/">Navegar a Home</Link>
      <Button
        title="Navegar a Home de manera imperativa (usando router)"
        onPress={navegarAHome}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- Por medio del objeto router podemos navegar a otras pantallas usando el método `navigate` y pasando el nombre de la ruta como parámetro.
- router tiene los siguientes métodos que podemos usar para navegar:
- **push**: navega a una nueva pantalla y la agrega al navigation Stack. Añade la nueva ruta al historial, para que puedas volver a la página anterior.
- **navigate**: funciona de manera similar a `router.push`, pero si la ruta ya existe en el Stack, no crea una entrada duplicada y sustituye la entrada actual en lugar de añadir una nueva.
- **replace**: reemplaza la ruta actual en Stack de navegación sin añadir una nueva entrada. Esto significa que después de llamar a `router.replace`, no se puede volver a la pantalla anterior utilizando `router.back()`.
- **dismissTo**: elimina todas las pantallas situadas encima de la ruta especificada y vuelve a navegar hasta ella. Si la pantalla no está en el historial, navega hasta esa ruta en su lugar.

#### ⚡ ¿Cuándo usar qué?

| Caso práctico                                                                             | Método                         |
| ----------------------------------------------------------------------------------------- | ------------------------------ |
| Añadir una nueva pantalla a la pila del historial (posibilidad de navegación hacia atrás) | `router.push("/profile")`      |
| Navegar sin duplicar una pantalla en el historial                                         | `router.navigate("/profile")`  |
| Sustituir la pantalla actual por otra                                                     | `router.replace("/dashboard")` |
| Garantizar que un usuario vuelva a una pantalla específica, eliminando todas las demás    | `router.dismissTo("/home")`    |

```javascript
// Usando router
router.push("/profile");
router.navigate("/profile");
router.replace("/profile");
router.dismissTo("/profie");

// Usando Link
<Link push href="/profile">
  Profile
</Link>;

<Link href="/profile">Profile</Link>;

<Link replace href="/profile">
  Profile
</Link>;

<Link dismissTo href="/profile">
  Profile
</Link>;
```

- También usando `router` podemos volver para atras si lo necesitamos utilizando las siguientes propiedades:
  - **back**: navega a la pantalla anterior.
  - **canGoBack**: comprueba si hay una ruta anterior en el Stack de navegación. Devuelve `true` si el usuario puede volver atrás y `false` si no hay historial al que volver.
- Modificamos la pantalla `about.tsx` para agregar un botón de volver:

```javascript
import { View, StyleSheet, Button } from "react-native";
import { Link, router } from "expo-router";

export default function About() {
  const volver = () => {
    if (router.canGoBack()) {
      router.back();
    } else {
      router.navigate("/");
    }
  };

  return (
    <View style={styles.container}>
      <Link href="/">Navegar a Home</Link>
      <Button title="Volver a pantalla anterior" onPress={volver} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- Para poder ver el historial en acción agregamos una pantalla nueva con el nombre de `profile.tsx`.

```bash
app/
  |_ _layout.tsx
  |_ about.tsx
  |_ index.tsx
  |_ profile.tsx
```

```javascript
// app/profile.tsx
import { View, StyleSheet, Button } from "react-native";
import { Link, router } from "expo-router";
import { useNavigationState } from "@react-navigation/native";

export default function Profile() {
  const routes = useNavigationState((state) => state.routes);

  const navegarAHome = () => {
    console.log(routes);
    router.navigate("/");
  };

  return (
    <View style={styles.container}>
      <Link href="/">Navegar a Home</Link>
      <Button
        title="Navegar a Home de manera imperativa (usando router)"
        onPress={navegarAHome}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- Para poder ver el historial tenemos que importar `useNavigationState` de `@react-navigation/native` que es el paquete base que usa `expo-router`.
- Usando el hook `useNavigationState((state) => state.routes)` le pedimos al navegador que nos de las rutas usadas.
- De esta forma al presionar el botón podemos ver como las rutas usan un `[]` para ir manejando el historial.
- Podes cambiar los diferentes métodos del router para ver como cambia el historial.

### Stacks anidados

- En aplicaciones mobile es fácil caer en tener navegadores anidados.
- Si queremos crear una nueva sección por ejemplo con el nombre settings y que tenga una pantalla inicial y una del usuario.
- Agregamos una carpeta dentro de `/app` con el nombre de `settings`.
- Agregamos un nuevo archivo `_layout.tsx` dentro de la carpeta `settings`.
- Agregamos dos nuevas rutas dentro de la carpeta settings con el nombre `index.tsx` y `usuario.tsx`.

```bash
app/
  |_ settings/
    |_ index.tsx
    |_ usuario.tsx
  |_ _layout.tsx
  |_ about.tsx
  |_ index.tsx
  |_ profile.tsx
```

```javascript
// app/settings/_layout.tsx
import { Stack } from "expo-router";

export default function SettingsLayout() {
  return (
    <Stack>
      <Stack.Screen
        name="index"
        options={{ title: "Settings Layout - Index" }}
      />
      <Stack.Screen
        name="usuario"
        options={{ title: "Settings Layout - Usuario" }}
      />
    </Stack>
  );
}
```

- Creamos 2 nuevas rutas `index` y `usuario` en un nuevo Stack con el nombre `SettingsLayout`.
- Ahora creamos las dos pantallas nuevas:

```javascript
// app/settings/index.tsx
import { Link } from "expo-router";
import { View, StyleSheet } from "react-native";

export default function Index() {
  return (
    <View style={styles.container}>
      <Link href="/">Ir al Root navigator Index</Link>
      <Link href="/settings/usuario">Ir al Settings Usuario</Link>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- Desde esta ruta podemos navegar al `/` para ir a `app/index.tsx`.
- También podemos navegar dentro del `SettingsLayout` usando `/settings/usuario`.

```javascript
// app/settings/usuario.tsx
import { Link, useRootNavigationState } from "expo-router";
import { View, StyleSheet, Button } from "react-native";
import { useNavigationState } from "@react-navigation/native";

export default function Usuario() {
  const routes = useNavigationState((state) => state.routes);
  const rootState = useRootNavigationState();

  const verHistorial = () => {
    console.log("Rutas del Navegador actual:", routes);
    console.log("Rutas del Navegador Root:", JSON.stringify(rootState.routes));
  };

  return (
    <View style={styles.container}>
      <Link href="/">Ir al Root navigator Index</Link>
      <Link href="./index">Ir al Settings Index</Link>
      <Button title="Ver historial / segmentos" onPress={verHistorial} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- Si refrescamos el servidor de Metro podemos volver al `index.tsx` principal.
- Navegamos `index.tsx` -> `/settings/index.tsx` -> `/settings/usuario.tsx`.
- Podemos ver que al navegar dentro del stack anidado vemos un segundo header.
- El header se puede sacar por medio de la configuración de las rutas.
- Lo importante es ver que estos 2 stack están anidados teniendo `Root Layout y Settings Layout`.
- Si presionamos el botón de `Ver historial` vemos los siguientes datos:

```json
Rutas del Navegador actual:
[
  {
    "key": "index-lhuGIWUVzD_SfbWgQJk4h",
    "name": "index",
    "params": {

    },
    "path": undefined
  },
  {
    "key": "usuario-wLp19m3-fdEVPD23JPRPf",
    "name": "usuario",
    "params": {

    },
    "path": undefined
  }
]

Rutas del Navegador Root:

[
  {
    "name": "index",
    "path": "",
    "key": "index-eOMMojgEKxwfLz7s9EvM_"
  },
  {
    "key": "settings-b8IlcWl_28zKCyWEU6W5p",
    "name": "settings",
    "state": {
      "stale": false,
      "type": "stack",
      "key": "stack-a4uAJhSFJlkUm0-OhiAq9",
      "index": 1,
      "routeNames": [
        "index",
        "usuario"
      ],
      "routes": [
        {
          "name": "index",
          "params": {

          },
          "key": "index-lhuGIWUVzD_SfbWgQJk4h"
        },
        {
          "key": "usuario-wLp19m3-fdEVPD23JPRPf",
          "name": "usuario",
          "params": {

          }
        }
      ],
      "preloadedRoutes": [

      ]
    }
  }
]
```

- De esta manera vemos como el navegador actual tiene 2 rutas en el historial `[index, usuario]`.
- El navegador principal tiene la ruta de `index` principal y después 2 rutas más de haber navegado a `settings/index` primer y luego a `settings/usuario`.
- Con esto medio que entendemos como funciona un Stack anidado.

### Rutas dinámicas

- Hasta ahora vimos como navegar de una pantalla a la otra pero nunca compartimos datos entre ellas.
- Es posible pasar parámetros a una ruta al navegar.
- `expo-router` usa rutas con nombre `[nombredeparametro].tsx`
- Por ejemplo podemos pasarle un valor a settings usando una ruta dinámica:
- Creamos un nuevo archivo con el siguiente nombre `/apps/settings/[id].tsx` con el siguiente código:

```javascript
import { Link, useLocalSearchParams } from "expo-router";
import { View, StyleSheet, Text } from "react-native";

export default function SettingsWithId() {
  const { id } = useLocalSearchParams();
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Settings con ID: {id}</Text>
      <Link href="/settings">Volver</Link>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    fontSize: 20,
    fontWeight: "bold",
  },
});
```

- Para navegar a esta pantalla podemos hacerlo de dos formas:
  - Usando Link y agregar el valor esperado en el `href` como `/settings/10` y pasamos 10 como valor.
  - Link también acepta un objeto como valor de `href`. Este objeto tiene la siguiente forma:

```javascript
href={{
  pathname: '/settings/[id]',
  params: { id: 10 },
}}
```

- Modificamos `settings/index.tsx` para agregar 2 nuevo Links y navegar a `settings/[id].tsx`.

```javascript
import { Link } from "expo-router";
import { View, StyleSheet } from "react-native";

export default function Index() {
  return (
    <View style={styles.container}>
      <Link href="/">Ir al Root navigator Index</Link>
      <Link href="/settings/usuario">Ir al Settings Usuario</Link>
      <Link href="/settings/10">Pasamos el ID 10</Link>
      <Link
        href={{
          pathname: "/settings/[id]",
          params: {
            id: 10,
          },
        }}
      >
        Pasamos el ID 10 con params
      </Link>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- En esta pantalla vemos dos formas de navegar a la pangalla `settings/[id].tsx` usando un string o un objeto como valor de la propiedad `href`.
- También podemos probar abrir el browser para ver que URL usa. Ejemplo: `http://localhost:8081/settings/10`.
- Modificamos `settings/_layout.tsx` para mostrar un header mejor que `[id]`.

```javascript
import { Stack } from "expo-router";

export default function SettingsLayout() {
  return (
    <Stack>
      <Stack.Screen
        name="index"
        options={{ title: "Settings Layout - Index" }}
      />
      <Stack.Screen
        name="usuario"
        options={{ title: "Settings Layout - Usuario" }}
      />
      <Stack.Screen name="[id]" options={{ title: "Settings Layout - ID" }} />
    </Stack>
  );
}
```

- También podemos ver como navegar usando `router` y pasar parámetros modificando `settings/index.tsx` de la siguiente manera:

```javascript
import { Link, router } from "expo-router";
import { View, StyleSheet, Button } from "react-native";

export default function Index() {
  return (
    <View style={styles.container}>
      <Link href="/">Ir al Root navigator Index</Link>
      <Link href="/settings/usuario">Ir al Settings Usuario</Link>
      <Link href="/settings/10">Pasamos el ID 10</Link>
      <Link
        href={{
          pathname: "/settings/[id]",
          params: {
            id: 10,
          },
        }}
      >
        Pasamos el ID 10 con params
      </Link>
      <Button
        title="Pasamos el ID 10"
        onPress={() =>
          router.navigate({
            pathname: "/settings/[id]",
            params: {
              id: 10,
            },
          })
        }
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- Podemos ver en el componente `Button` como podemos usar `router.navigate` y pasarle como parámetro un objeto con las propiedades pathname y params.
- Si necesitamos pasar más parámetros a una ruta podemos agregar propiedades:valor al objeto params.
- Modificamos `settings/index.tsx` y también `settings/[id].tsx` para mostrar otro parámetro:

```javascript
import { Link, router } from "expo-router";
import { View, StyleSheet, Button } from "react-native";

export default function Index() {
  return (
    <View style={styles.container}>
      <Link href="/">Ir al Root navigator Index</Link>
      <Link href="/settings/usuario">Ir al Settings Usuario</Link>
      <Link href="/settings/10">Pasamos el ID 10</Link>
      <Link
        href={{
          pathname: "/settings/[id]",
          params: {
            id: 10,
          },
        }}
      >
        Pasamos el ID 10 con params
      </Link>
      <Button
        title="Pasamos el ID 10"
        onPress={() =>
          router.navigate({
            pathname: "/settings/[id]",
            params: {
              id: 10,
              name: "Nicolas",
            },
          })
        }
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- Agregamos `name` con el valor `Nicolas` a los parámetros:

```javascript
params: {
  id: 10,
  name: "Nicolas",
},
```

- Ahora podemos recibir este parámetro en `settings/[id].tsx`:

```javascript
import { Link, router } from "expo-router";
import { View, StyleSheet, Button } from "react-native";

export default function Index() {
  return (
    <View style={styles.container}>
      <Link href="/">Ir al Root navigator Index</Link>
      <Link href="/settings/usuario">Ir al Settings Usuario</Link>
      <Link href="/settings/10">Pasamos el ID 10</Link>
      <Link
        href={{
          pathname: "/settings/[id]",
          params: {
            id: 10,
          },
        }}
      >
        Pasamos el ID 10 con params
      </Link>
      <Button
        title="Pasamos el ID 10"
        onPress={() =>
          router.navigate({
            pathname: "/settings/[id]",
            params: {
              id: 10,
              name: "Nicolas",
            },
          })
        }
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

```javascript
import { Link, useLocalSearchParams } from "expo-router";
import { View, StyleSheet, Text } from "react-native";

export default function SettingsWithId() {
  const { id, name } = useLocalSearchParams();
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Settings con ID: {id}</Text>
      {name !== undefined ? (
        <Text style={styles.text}>Nombre: {name}</Text>
      ) : null}

      <Link href="/settings">Volver</Link>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    fontSize: 20,
    fontWeight: "bold",
  },
});
```

- Ahora si vemos en la Web como pasa estos parámetros vemos la siguiente URL: `http://localhost:8081/settings/10?name=Nicolas`.
- Al definir el parámetro como [id] se ve como `/id` mientras que `name` pasa el valor como query string.
- Ver las rutas en el navegador ayuda a visualizar pero también entender que es lo que hace `expo-router` ya que las direcciones están adaptadas / pensadas para que funcionen en Web y no solo en Android o iOS.

### Abrir una pantalla como Modal

- En algunos casos necesitamos abrir una pantalla como modal.
- Expo router nos permite definir las rutas y usar la propiedad `options={{presentation: "modal"}}` para establecer si la ruta es un modal o no.
- Agregamos una nueva pantalla en `app/modal.tsx`.

```javascript
import { Link, router } from "expo-router";
import { View, StyleSheet, Text } from "react-native";

export default function Modal() {
  const isPresented = router.canGoBack();

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Modal</Text>
      {isPresented && <Link href="../">Volver (Dismiss modal)</Link>}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    fontSize: 20,
    fontWeight: "bold",
  },
});
```

- En esta pantalla mostramos un mensaje de que estamos dentro del modal.
- Si el usuario puede volver para atras ya que navega de otra pantalla entonces usamos `const isPresented = router.canGoBack()` para validarlo.
- Si existe la posibilidad de volver entonces podmos usar `../` para decirle al Modal que se cierre.
- Cualquier navegación que pongamos en el Modal va a navegar dentro del modal.
- Agregamos el Modal actualizando `apps/_layout.tsx`:

```javascript
import { Stack } from "expo-router";

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="index" options={{ title: "Root Layout - Home" }} />
      <Stack.Screen name="about" options={{ title: "Root Layout - About" }} />
      <Stack.Screen
        name="profile"
        options={{ title: "Root Layout - Profile" }}
      />
      <Stack.Screen
        name="settings"
        options={{ title: "Root Layout - Settings" }}
      />
      <Stack.Screen
        name="modal"
        options={{
          presentation: "modal",
        }}
      />
    </Stack>
  );
}
```
