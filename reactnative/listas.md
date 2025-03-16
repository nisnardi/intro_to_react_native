# React Native

## Listas

- React Native proporciona un conjunto de componentes para presentar listas de datos.
- Como regla general vas a querer usar `FlatList` o `SectionList`.
- Creamos un nuevo projecto con el nombre de `lista` y reseteamos el proyecto Expo para dejar todo listo para trabajar.

```bash
npx create-expo-app listas && cd listas && npm run reset-project && npx expo
```

### FlatList

- El componente `FlatList` muestra una lista de scroll de datos que cambian, pero con una estructura similar.
- `FlatList` funciona bien para listas largas, donde el número de elementos puede cambiar con el tiempo.
- A diferencia de `ScrollView` que es más genérico, `FlatList` sólo muestra los elementos que aparecen en pantalla, no todos los elementos a la vez. (Lista virtual).
- El componente `FlatList` requiere dos props: `data y renderItem`.
  - `data`: es la fuente de información de datos.
  - `renderItem`: es una función que toma un elemento de la propiedad `data` y devuelve un componente para renderizar.

```javascript
<FlatList
  data={[]}
  renderItem={({ item }) => (
    <View>
      <Text>{item}</Text>
    </View>
  )}
/>
```

- `data` acepta un array de cualquier tipo como valor.
- `renderItem` acepta un `callback` que retorna un componente que se va a renderizar por cada item.
- `{item}` lo usamos para destructurar el parámetro que se le pasa a esta función que tiene la forma de `parametro.item` para poder utilizarlo en nuestro componente.

```javascript
import { Text, View, FlatList, StyleSheet } from "react-native";

export default function Index() {
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  return (
    <View style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={({ item }) => (
          <View>
            <Text>{item.name}</Text>
          </View>
        )}
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

- Creamos un array de alumnos y cada elemento alumno se renderiza como un componente de texto mostrando el nombre.
- Dado que React necesita un `key` tenemos dos opciones:
  - Agregar una propiedad `key` a los elementos de la colección.
  - Agregar una propiedad `keyExtractor` a la lista donde especificamos una función de como obtener la `key` de cada elemento.
- Por ejemplo si sabemos que el nombre de cada alumno es único podemos utilizar el nombre como `key`.
- `keyExtractor` también nos da el `index` de cada elemento que también lo podemos utilizar.

```javascript
<FlatList
  data={alumnos}
  renderItem={({ item }) => (
    <View>
      <Text>{item.name}</Text>
    </View>
  )}
  keyExtractor={(item, index) => `${item.name}-${index}`}
/>
```

- FlatList nos da muchas cosas para poder utilizar como:
  - Funciona `cross-platform`para cualquier plataforma.
  - Se puede utilizar la propiedad `horizontal` que acepta un valor `boolean` para hacer que se renderize de manera `horizontal` en lugar de `vertical`.
  - Se puede llamar a una función para saber cuando un elemento está visible, ya que esta lista no renderiza todos los elementos juntos.
  - Podemos agregar un componente Header utilizando la propiedad `ListHeaderComponent`.
  - Tambien podemos agregarle un footer utilizando la propiedad `ListFooterComponent`.
  - `ItemSeparatorComponent` nos permite establecer un componente para separar elementos. Esto nos viene super últil ya que no toma en cuenta el primer y último elemento.
  - Otra gran feature es que nos permite hacer un `Pull to Refresh` que significa que podemos hacer `pull` en la lista para refrescar el contenido.
  - También podemos mostrar un componente de carga o loading cuando `paginamos` la lista para mostrar más elementos.
  - `FlatList` también nos permite scrollear a un índice de la lista cuando lo necesitamos.
  - Podemos mostrar los datos o items en forma de comuna en lugar de una sola fila.
- Como podemos ver FlatList es sumamene útil y flexible.

#### Lista Horizontal

- Para poder utilizar la lista de manera horizontal debemos setear la propiedad `horizontal` en `true`.

```javascript
import { Text, View, FlatList, StyleSheet } from "react-native";

export default function Index() {
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  return (
    <View style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
          </View>
        )}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        horizontal
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
  item: {
    borderWidth: 1,
    borderColor: "blue",
    padding: 10,
    height: 100,
    width: 100,
    alignItems: "center",
    justifyContent: "center",
    marginRight: 20,
  },
});
```

#### Agregando un separador

- Para poder separar los componentes podemos utilizar la propiedad `ItemSeparatorComponent` que acepta un componente que va a ser renderizado entre items.

```javascript
import { Text, View, FlatList, StyleSheet, SafeAreaView } from "react-native";

export default function Index() {
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
          </View>
        )}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },

  item: {
    padding: 20,
    alignItems: "center",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#DDD" },
});
```

#### Mostrando datos en columnas

- En algunos casos vamos a necesitar utilizar `FlatList` como una grilla y para eso podemos usar la propiedad `numColumns={cantidadDeColumnas}` que toma un número como valor para especificar la cantidad de columnas.
- Por ejemplo podemos utilizar `numColumns={2}` para mostrar una lista a 2 columnas.
- Al cambiar esta propiedad React puede tirar un error pero al refrescar va a andar bien.

```javascript
import { Text, View, FlatList, StyleSheet, SafeAreaView } from "react-native";

export default function Index() {
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
          </View>
        )}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
        numColumns={2}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },

  item: {
    width: "50%",
    padding: 20,
    alignItems: "center",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#DDD" },
});
```

- Para poder alinear bien las columnas le establecemos a cada item que tome el `50%` del ancho disponible.
- En caso de necesitarlo podemos acceder al wrapper de cada columna con la propiedad `columnWrapperStyle`.

#### Agregando un Header

- Para agregar un header único para toda la lista podemos utilizar la propiedad `ListHeaderComponent` que acepta una función que retorna el componente que se va a renderizar.

```javascript
import { Text, View, FlatList, StyleSheet, SafeAreaView } from "react-native";

export default function Index() {
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
          </View>
        )}
        ListHeaderComponent={() => (
          <View style={styles.headerContainer}>
            <Text style={styles.headerText}>Alumnos</Text>
          </View>
        )}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  headerContainer: {
    paddingVertical: 20,
    alignItems: "center",
    backgroundColor: "white",
  },
  headerText: {
    fontSize: 20,
    fontWeight: "bold",
  },
  item: {
    padding: 20,
    alignItems: "center",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#DDD" },
});
```

- También usando un truco podemos establecer que el header se quede en el lugar usando la propiedad `stickyHeaderIndices={[0]}`.

```javascript
import { Text, View, FlatList, StyleSheet, SafeAreaView } from "react-native";

export default function Index() {
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
          </View>
        )}
        ListHeaderComponent={() => (
          <View style={styles.headerContainer}>
            <Text style={styles.headerText}>Alumnos</Text>
          </View>
        )}
        stickyHeaderIndices={[0]}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  headerContainer: {
    paddingVertical: 20,
    alignItems: "center",
    backgroundColor: "white",
  },
  headerText: {
    fontSize: 20,
    fontWeight: "bold",
  },
  item: {
    padding: 20,
    alignItems: "center",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#DDD" },
});
```

#### Agregando un Footer

- Para mostrar un pie o footer de la lista usamos la propiedad `ListFotterComponent`.
- Esta propiedad acepta una función como valor que retorna el component que queremos renderizar como footer.

```javascript
ListFooterComponent={() => (
  <View style={styles.footerContainer}>
    <Text style={styles.footerText}>Fin de la lista</Text>
  </View>
)}
```

- Usamos el footer en la lista de la siguiente manera:

```javascript
import { Text, View, FlatList, StyleSheet, SafeAreaView } from "react-native";

export default function Index() {
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
          </View>
        )}
        ListFooterComponent={() => (
          <View style={styles.footerContainer}>
            <Text style={styles.footerText}>Fin de la lista</Text>
          </View>
        )}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  item: {
    padding: 20,
    alignItems: "center",
  },
  footerContainer: {
    paddingVertical: 10,
    alignItems: "center",
  },
  footerText: {
    fontSize: 14,
    color: "darkgrey",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#DDD" },
});
```

#### Pull to Refresh

- Usando la propiedad `refreshControl` podemos utilizar el componente `RefreshControl` para mostar un indicador de que algo está cargando o pasando.
- Generalmente cuando el usuario hace pull de la lista es para cargar más datos como por ejemplo cargar más datos de la lista de Twitter (X).
- Para poder utilizar el componente RefreshControl hay que importarlo de react-native.

```javascript
// Importamos
import {  RefreshControl,} from "react-native";

// Código del componente / lista.
refreshControl={
  <RefreshControl
    refreshing={isRefreshing}
    onRefresh={onRefreshHandler}
  />
}
```

- Dado que no estamos cargando datos vamos a utilizar un timer para mostrar el indicador durante 5 segundos.

```javascript
import { useEffect, useState } from "react";
import {
  Text,
  View,
  FlatList,
  StyleSheet,
  SafeAreaView,
  RefreshControl,
} from "react-native";

export default function Index() {
  const [isRefreshing, setIsRefreshing] = useState(false);
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  useEffect(() => {
    let setTimeoutID = null;
    if (isRefreshing) {
      console.log("Cambió el valor de isRefreshing");
      console.log("Ejecutamos un times si isRefreshing es true");
      setTimeoutID = setTimeout(() => {
        setIsRefreshing(false);
      }, 5000);
    }

    return () => {
      if (setTimeoutID) {
        console.log(
          "Si hay un timer corriendo entonces limpiamos el timer antes de que el componente haga unmount"
        );

        clearTimeout(setTimeoutID);
      }
    };
  }, [isRefreshing]);

  const onRefreshHandler = () => {
    setIsRefreshing(true);
  };

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
          </View>
        )}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
        refreshControl={
          <RefreshControl
            refreshing={isRefreshing}
            onRefresh={onRefreshHandler}
          />
        }
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  item: {
    padding: 20,
    alignItems: "center",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#DDD" },
});
```

- La propiedad `refreshing` le dice a la lista que estamos refrescando el contenido.
- la propiedad `onRefresh` acepta un callback para permitirnos manejar lo que queremos hacer cuando el usuario hace pull de la lista para ejecutar un refresh.
- Se puede programar un indicador custom pero va a llevar más trabajo. Podemos leer más sobre como hacer esto en el [siguiente tutorial (en inglés)](https://blog.cloudboost.io/building-a-custom-refresh-animation-in-react-native-using-reanimated-9b64212a0366).

#### Carga infinita

- Cuando el usuario hace scroll hasta el final de la lista podemos utilizar `onEndReached` y `onEndReachedThreshold`,
- `onEndReached` es una función que se llama una vez cuando el índice del scroll está dentro del rango establcido por la propiedad `onEndReachedThreshold`.
- `onEndReachedThreshold` establece un valor de tolerancia para considerar que se llegó al final de la lista y así ejecutar el callback de `onEndReached`.
- En el próximo ejemplo estamos forzando a que muestre un ActivityIndicator cuando carga para simular un infinite scroll.

```javascript
import { useEffect, useState } from "react";
import {
  Text,
  View,
  FlatList,
  StyleSheet,
  SafeAreaView,
  ActivityIndicator,
} from "react-native";

export default function Index() {
  const [isLoadingMore, setisLoadingMore] = useState(false);
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  const onEndReachedHandler = () => {
    setisLoadingMore(true);
  };

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
          </View>
        )}
        ListFooterComponent={() => (
          <View style={styles.footerContainer}>
            {isLoadingMore ? (
              <ActivityIndicator />
            ) : (
              <Text style={styles.footerText}>Fin de la lista</Text>
            )}
          </View>
        )}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
        onEndReached={onEndReachedHandler}
        onEndReachedThreshold={0}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  item: {
    padding: 20,
    alignItems: "center",
  },
  footerContainer: {
    paddingVertical: 10,
    alignItems: "center",
  },
  footerText: {
    fontSize: 14,
    color: "darkgrey",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#DDD" },
});
```

- Por medio de la propiedad `onEndReached` usamos el callback para cambiar el valor de la variable de estado `isLoadingMore` a true.
- De esta manera al mostrar el componente footer en lugar de renderizar el texto de fin de lista va a mostrar un activity indicator para que el usuario sepa que estamos cargando más datos.

#### Scrollear a un elemento

- Las listas tienen una método que se llama `scrollToIndex`.
- Para poder utilizar este método necesitamos manejar una referencia de la lista que podamos llamar desde otras partes del código.
- React tiene un hook llamado `useRef` que nos permite crear una referencia a un componente.
- `useRef` retorna una referenciaq eu tiene una propiedad llamada `current` con la referencia al componente.
- Desde la referencia podemos llamar a `scrollToIndex` y pasarle un objeto como parámetro que tenga las siguientes propiedades:
  - `index`: es un valor numérico a donde queremos hacer scroll.
  - `animated`: es un valor booleano para decirle al scroll si queremos que se mueva de manera animada o no.

```javascript
import React, { useRef } from "react";
import {
  Text,
  View,
  FlatList,
  StyleSheet,
  SafeAreaView,
  Button,
} from "react-native";

export default function Index() {
  const flatListRef = useRef(null);

  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  const scrollToLastItem = () => {
    if (flatListRef.current) {
      flatListRef.current.scrollToIndex({
        index: alumnos.length - 1,
        animated: true,
      });
    }
  };

  const scrollToFirstItem = () => {
    if (flatListRef.current) {
      flatListRef.current.scrollToIndex({
        index: 0,
        animated: true,
      });
    }
  };

  return (
    <SafeAreaView style={styles.container}>
      <Button title="Ir al final de la lista" onPress={scrollToLastItem} />
      <FlatList
        ref={flatListRef}
        data={alumnos}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
          </View>
        )}
        ListFooterComponent={() => (
          <View style={styles.footerContainer}>
            <Text style={styles.footerText}>Fin de la lista</Text>
          </View>
        )}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
      />
      <Button title="Ir al principio de la lista" onPress={scrollToFirstItem} />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  item: {
    padding: 20,
    alignItems: "center",
  },
  footerContainer: {
    paddingVertical: 10,
    alignItems: "center",
  },
  footerText: {
    fontSize: 14,
    color: "darkgrey",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#DDD" },
});
```

#### Pasando datos extras

- La propiedad `extraData` se utiliza para indicar a la lista que vuelva a renderizarse cuando cambian algunos datos externos que no forman parte directamente de los datos pasados usando la propiedad `data`.
- La documentación de React Native nos muestra un ejemplo donde podemos seleccionar un elemento de la lista.
- Vamos a adaptar el ejemplo a nuestra lista.

```javascript
import { useState } from "react";
import {
  Text,
  View,
  FlatList,
  StyleSheet,
  SafeAreaView,
  TouchableOpacity,
} from "react-native";

const Item = ({ item, onPress, backgroundColor, fontWeight }) => {
  return (
    <TouchableOpacity
      onPress={onPress}
      style={[styles.item, { backgroundColor }]}
    >
      <Text style={[{ fontWeight: fontWeight }]}>{item.name}</Text>
    </TouchableOpacity>
  );
};

export default function Index() {
  const [selectedAlumno, setSelectedAlumno] = useState(null);
  const alumnos = [
    { name: "Catalina" },
    { name: "Maria" },
    { name: "Raydberg" },
    { name: "Yesenia" },
    { name: "Sofia" },
    { name: "Jefferson" },
    { name: "Sebastian" },
    { name: "Pipe" },
    { name: "Juan David" },
    { name: "Carlos" },
    { name: "Daniela" },
    { name: "Mara" },
    { name: "Heberson" },
    { name: "Jesus David" },
    { name: "Andrés" },
    { name: "Edison" },
    { name: "Santiago" },
  ];

  const renderItem = ({ item }) => {
    const backgroundColor = item.name === selectedAlumno ? "#CCC" : "#DDD";
    const fontWeight = item.name === selectedAlumno ? "bold" : "normal";

    return (
      <Item
        item={item}
        onPress={() => setSelectedAlumno(item.name)}
        backgroundColor={backgroundColor}
        fontWeight={fontWeight}
      />
    );
  };

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={alumnos}
        renderItem={renderItem}
        ListFooterComponent={() => (
          <View style={styles.footerContainer}>
            <Text style={styles.footerText}>Fin de la lista</Text>
          </View>
        )}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
        extraData={selectedAlumno}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  item: {
    padding: 20,
    alignItems: "center",
  },
  footerContainer: {
    paddingVertical: 10,
    alignItems: "center",
  },
  footerText: {
    fontSize: 14,
    color: "darkgrey",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#DDD" },
});
```

- En este ejemplo usamos `extraData` para pasar el valor del estado `selectedAlumno` que cambia al presionar cualquiera de los items de la lista.
- Cambiar el valor de `extraData` hace que la lista vuelva a renderizarse.

#### Mostrar un componente vacio

- Usando la propiedad `ListEmptyComponent` podemos mostrar un componente cuando la lista esté vacía.
- Por medio de la propiedad `contentContainerStyle` podemos acceder al contenedor de la lista para decirle que ocupe el 100% del alto pantalla.
- Luego establecemos el componente que queremos mostrar cuando la lista está vacia.

```javascript
import { Text, View, FlatList, StyleSheet, SafeAreaView } from "react-native";

const Item = ({ name }) => {
  return (
    <View style={styles.item}>
      <Text>{name}</Text>
    </View>
  );
};

export default function Index() {
  const alumnos = [
    {
      title: "Alumnas",
      data: [
        { name: "Catalina" },
        { name: "Maria" },
        { name: "Yesenia" },
        { name: "Sofia" },
        { name: "Daniela" },
        { name: "Mara" },
      ],
    },
    {
      title: "Alumnos",
      data: [
        { name: "Raydberg" },
        { name: "Jefferson" },
        { name: "Sebastian" },
        { name: "Pipe" },
        { name: "Juan David" },
        { name: "Carlos" },
        { name: "Heberson" },
        { name: "Jesus David" },
        { name: "Andrés" },
        { name: "Edison" },
        { name: "Santiago" },
      ],
    },
  ];

  const renderItem = ({ item }) => {
    return <Item name={item.name} />;
  };

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={[]}
        renderItem={renderItem}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
        contentContainerStyle={styles.container}
        ListEmptyComponent={() => (
          <View style={styles.emptyComponent}>
            <Text>No hay items para mostrar</Text>
          </View>
        )}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  item: {
    padding: 20,
    alignItems: "center",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#CCC" },
  emptyComponent: {
    height: "100%",
    justifyContent: "center",
    alignItems: "center",
  },
});
```

- Si bien FlatList es un componente que podemos utilizar para muchas cosas tiene sus limitaciones.
- Existen otras opciones para usar listas virtuales como son [FlashList de Shopify](https://shopify.github.io/flash-list/) y la super nueva lista de [Tanstack List](https://tanstack.com/virtual/latest) que pueden brindar mejor performance que FlatList.

### SectionList

- En alguna oportunidad vamos a necesitar mostrar una lista que tenga secciones y para esto usamos `SectionList`.
- Dado que es una lista virtual podemos usar muchas de las propiedades que vimos para `FlatList`.
- Uno de los cambios más importantes que tienen `SectionList` con `FlatList` es la forma en la que armamos los datos para decirle a la lista como son las secciones.
- En lugar de usar la propiedad `data` como hicimos en FlatList vamos a usar la propiedad `sections`.
- Section va a ser una colección de objetos que tenga una propiedad `title` para establecer el título de la sección y una propiedad llamada `data` donde van a estar los elementos.
- Modificamos nuesto código para mostrar secciones en la lista.

```javascript
import {
  Text,
  View,
  SectionList,
  StyleSheet,
  SafeAreaView,
} from "react-native";

const Item = ({ name }) => {
  return (
    <View style={styles.item}>
      <Text>{name}</Text>
    </View>
  );
};

export default function Index() {
  const alumnos = [
    {
      title: "Alumnas",
      data: [
        { name: "Catalina" },
        { name: "Maria" },
        { name: "Yesenia" },
        { name: "Sofia" },
        { name: "Daniela" },
        { name: "Mara" },
      ],
    },
    {
      title: "Alumnos",
      data: [
        { name: "Raydberg" },
        { name: "Jefferson" },
        { name: "Sebastian" },
        { name: "Pipe" },
        { name: "Juan David" },
        { name: "Carlos" },
        { name: "Heberson" },
        { name: "Jesus David" },
        { name: "Andrés" },
        { name: "Edison" },
        { name: "Santiago" },
      ],
    },
  ];

  const renderItem = ({ item }) => {
    return <Item name={item.name} />;
  };

  return (
    <SafeAreaView style={styles.container}>
      <SectionList
        sections={alumnos}
        renderSectionHeader={({ section: { title } }) => (
          <View style={styles.headerContainer}>
            <Text style={styles.headerText}>{title}</Text>
          </View>
        )}
        renderItem={renderItem}
        keyExtractor={(item, index) => `${item.name}-${index}`}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  headerContainer: {
    backgroundColor: "#CCC",
    padding: 10,
  },
  headerText: {
    fontSize: 20,
    fontWeight: "bold",
    textAlign: "center",
  },
  item: {
    padding: 20,
    alignItems: "center",
  },
  separator: { borderBottomWidth: 1, borderBottomColor: "#CCC" },
});
```

- Podemos cambiar si el header funcione como sticky o no usando la propiedad `stickySectionHeadersEnabled`.
- Esta propiedad funciona diferente para iOS y Android ya que inicialmente está seteada como true para iOS y false para Android.

```javascript
<SectionList
  sections={alumnos}
  renderSectionHeader={({ section: { title } }) => (
    <View style={styles.headerContainer}>
      <Text style={styles.headerText}>{title}</Text>
    </View>
  )}
  renderItem={renderItem}
  keyExtractor={(item, index) => `${item.name}-${index}`}
  ItemSeparatorComponent={() => <View style={styles.separator} />}
  stickySectionHeadersEnabled={false}
/>
```
