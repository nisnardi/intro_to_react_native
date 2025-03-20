# React Native

## Hooks? Effect? Context? y Fetch?

- Es posible que en algún momento escuchamos o leímos sobre algo llamado hooks, effect o context y no sabemos bien qué son o para que se usan y React lo utiliza bastante.
- Venimos aprendiendo un montón de cosas pero todavía no vimos como hacer para traer datos de un servidor. Podemos usar `fetch` en React Native?
- Durante esta sección del curso vamos a aprender sobre todos estos temas `hooks, effect, context y fetch` para entender qué son, cómo se usan y sobre todo si podemos traer datos del servidor.
- Como veamos varios temas técnicos ahora es un buen momento de `agarrar tu snack favorito y algo de tomar`, como dice [Russ de Retro Game Corps](https://www.youtube.com/@RetroGameCorps) en todos sus videos (por si le gustan los juegos retro!!).

### Hooks

- `Hooks` en React son unas funciones especiales que nos permiten usar manejar el estado de un componente funcional y su ciclo de vida.
- Antes de que salieran los hooks, solo los componentes creados usando una clase de JavaScript podían gestionar eventos de estado y el ciclo de vida del componente.
- Ahora los también los componentes funcionales pueden hacer lo mismo que los componentes de clases pero de una forma más sencilla.
- Hace un tiempo React migró de componentes que usaban Class a componentes funcionales usando tan solo funciones.

#### ¿Para qué se usan los hooks?

- Pueden manejar el estado dentro de componentes funcionales.
- También manejan efectos secundarios como hacer fetch de datos de una fuente externa al componente y subscribirse a eventos.
- Reutilizar la lógica entre componentes sin utilizar patrones complejos como render props o componentes de orden superior.

### Hooks más importantes

#### useState

- **useState**: Agrega estado a un componente funcional.

```javascript
import React, { useState } from "react";
import { View, Text, TouchableOpacity, StyleSheet } from "react-native";

export default function Estado() {
  const [count, setCount] = useState(0);

  const onPressHandler = () => setCount(count + 1);

  return (
    <View style={styles.container}>
      <Text style={styles.count}>Contador: {count}</Text>
      <TouchableOpacity onPress={onPressHandler} style={styles.button}>
        <Text style={styles.buttonText}>+</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { alignItems: "center", marginTop: 50 },
  count: { fontSize: 24 },
  button: {
    marginTop: 10,
    padding: 10,
    backgroundColor: "blue",
    borderRadius: 5,
  },
  buttonText: { color: "white", fontSize: 20 },
});
```

- Como sabemos `useState` acepta como parámetro el valor por default que va a tener la variable.
- Retorna un array de 2 posiciones donde la primera es la variable que mantiene el estado entre render. En este caso se llama `count` y se inicializa con el valor 0.
- El segundo valor del array es una función que podemos utilizar para actualizar el valor de la variable de estado. En este caso nombramos a la función `setCount` siguiendo la convención de usar `set` para establecer lo que hace esta función y el nombre de la variable que actualiza `count`.
- También sabemos que la función `setCount` acepta una función `setCount((estadoPrevio) => estadoPrevio + 1 )` en casos que necesitamos actualizar el valor usando el estado anterior.

### useEffect

- `useEffect` es un hook que permite sincronizar un componente con un sistemas externos.

```javascript
import React, { useEffect, useState } from "react";
import { View, Text, Button, StyleSheet } from "react-native";

export default function FetchData() {
  const [contador, setContador] = useState(0);

  // Sin dependencias
  useEffect(() => {
    console.log("useEffect sin dependencias se ejecuta en cada render.");
  });

  // Con dependencia vacia
  useEffect(() => {
    console.log(
      "useEffect con dependencias vacía se ejecuta solamente cuando el componente se monta o renderiza por primera vez."
    );
  }, []);

  useEffect(() => {
    console.log(
      "useEffect con dependencias se ejecuta cada vez que algún valor de las dependencias cambia de valor."
    );
  }, [contador]);

  return (
    <View style={styles.container}>
      <Text style={styles.contador}>Contador: {contador}</Text>
      <Button
        title="Incrementar estado y ver la consola"
        onPress={() => {
          setContador(contador + 1);
        }}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
  contador: { fontSize: 24, marginBottom: 20 },
});
```

- `useEffect` acepta dos parámetros:
  - El primer parámetro es una función que se va a ejecutar como efecto.
  - El segundo parámetro es opcional y acepta un array de dependencias.
- `useEffect` se va a ejecutar de diferentes formas según lo utilicemos:
  - Si no le pasasmo ninguna colección de dependencias se va a ejecutar en cada render del componente.
  - Si le pasamos una colección vacía se va a ejecutar sólo cuando el componente se monta o renderiza por primera vez.
  - Finalmente al pasarle un valor o varios valores como dependencia en el array, `useEffect` se va a ejecutar cada vez que alguno de esos valores cambie.
- Tenemos que tener cuidado al usar `useEffect` porque puede causar loops infinitos de renders dependiendo como lo usemos.

### Context

### Carga de Datos - Fetch

- Cargar datos de una fuente externa es considerado un efecto ya que la función o componente van a mostrar diferentes datos según un resultado externo y no podemos garantizar el valor retornado.
- Dado que es un efecto podemos utilizar `useEffect` para cargar datos de una API por ejemplo.
- Para llamar al servidor podemos usar `fetch`.
- Podemos manejar el estado de carga con `useState`.
- También tenemos que manejar si hay error para mantener informado al usuario de lo que está pasando.
- En este ejemplo vamos a cargar una list de TODO's de una API que está en `https://jsonplaceholder.typicode.com/todos`.
- Podes abrir esa dirección en el navegador para ver que tipo de respuesta nos da.

```javascript
import React, { useEffect, useState } from "react";
import {
  View,
  Text,
  ActivityIndicator,
  StyleSheet,
  FlatList,
} from "react-native";

interface TODO {
  userId: number;
  id: number;
  title: string;
  completed: boolean;
}

interface ItemProps {
  item: TODO;
}

const API_URL = "https://jsonplaceholder.typicode.com/todos";

const Item = ({ item }: ItemProps) => {
  return (
    <View style={styles.item}>
      <Text>
        ID: {item.id} UserID: {item.userId} Title: {item.title} Completado:{" "}
        {item.completed}
      </Text>
    </View>
  );
};

export default function Efecto() {
  const [data, setData] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [loadingError, setLoadingError] = useState<string | null>(null);

  useEffect(() => {
    const loadData = async () => {
      setLoadingError(null);
      setIsLoading(true);
      try {
        const response = await fetch(API_URL);
        const todos = await response.json();

        setData(todos);
      } catch (error: unknown) {
        console.log(error);
        if (error instanceof Error) {
          setLoadingError(error.message);
        }
      } finally {
        setIsLoading(false);
      }
    };

    loadData();
  }, []);

  return (
    <View style={styles.container}>
      {isLoading ? (
        <ActivityIndicator size="large" color="#CCC" />
      ) : loadingError === null ? (
        <FlatList
          data={data}
          renderItem={({ item }) => <Item item={item} />}
          ItemSeparatorComponent={() => <View style={styles.separator} />}
        />
      ) : (
        <Text>Error</Text>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: { padding: 20 },
  item: { paddingVertical: 10 },
  separator: { height: 1, backgroundColor: "#CCC" },
});

```

- En este ejemplo estamos haciendo varias cosas:

```javascript
const [data, setData] = useState([]);
const [isLoading, setIsLoading] = useState(false);
const [loadingError, setLoadingError] = (useState < string) | (null > null);
```

- Declaramos 3 variables de estado para manejar diferentes cosas.
  - `data` va a ser los datos que vamos a mostrar en pantalla. En este caso hasta podríamos nombrar esta variable `todos`. Inicialmente le seteamos el valor de un array vacio.
  - `isLoading` nos va a ayudar a saber si la aplicación está cargando datos. Inicialmente lo establcemos en false ya que vamos a cambiar este valor cuando carguemos los datos.
  - `loadingError` es una variable de estado que vamos a usar para saber si tenemos algún error o no.
- Gran parte del trabajo pasa en `useEffect`:

```javascript
useEffect(() => {
  const loadData = async () => {
    setLoadingError(null);
    setIsLoading(true);
    try {
      const response = await fetch(API_URL);
      const todos = await response.json();

      setData(todos);
    } catch (error: unknown) {
      console.log(error);
      if (error instanceof Error) {
        setLoadingError(error.message);
      }
    } finally {
      setIsLoading(false);
    }
  };

  loadData();
}, []);
```

- `useEffect` tiene una dependencia vacía lo que significa que solo queremos que se ejecute la primera vez que el componente se monta o renderiza.
- Al ejecutarse el `useEffect` llama a una función `loadData` que es una función `async` ya que queremos utilizar `await` para esperar que se resuelvan las promesas de `fetch` y `json`.
- La función `loadData` setea inicialmente el estado de loading error a null por si hay algún error previo y isLoading a true para que la aplicación sepa que está cargando.
- Luego llama a fecth y utiliza `await` para esperar la respuesta del servidor.
- Una vez obtenida la respuesta debemos parsear el contenido de `JSON` a objeto para poder usarlo en nuestro código.
- Si todo salió bien se llama a `setData` para cambiar el estado y guardar los `Todo's` que trajimos del servidor que se van a mostrar en pantalla.
- Dado que usamos `try and catch` podemos guardar el error para mostrarle al usuario, en caso de que ocurra alguno, usando la variable de estado `loadingError`.
- Finalmente usamos `finally` para asegurarnos que ya sea con o sin error cambiemos el estado de isLoading a false ya que no hay ninguna carga ejecutandose.
- Ahora que entendimos como funciona la carga sólo nos queda ver como mostrar los datos:

```javascript
return (
  <View style={styles.container}>
    {isLoading ? (
      <ActivityIndicator size="large" color="#CCC" />
    ) : loadingError === null ? (
      <FlatList
        data={data}
        renderItem={({ item }) => <Item item={item} />}
        ItemSeparatorComponent={() => <View style={styles.separator} />}
      />
    ) : (
      <Text>Error</Text>
    )}
  </View>
);
```

- Dado que la pantalla carga datos vamos a usar la variable de estado `isLoading` para mostrar un `ActivityIndicator` mientras cargamos los datos.
- Cuando `isLoading` sea false necesitamos manejar el error y para eso podemos usar `loadingError` y ver si es `null` o no. En caso de que sea null significa que no hay error y podemos mostrar la lista. Si hay error entonces mostramos el error en un componente de Texto.
- FlatList usa la propiedad `data` para mostrar la colección que tenemos en la variable `data` que es la colección de Todo's.
- `renderItem` es una función que se ejecuta por cada item de la colección data para mostrar el item de la lista. En este caso creamos un componente `Item` que muestra los datos del Todo.
- ItemSeparatorComponent lo usamos para mostrar algo entre items de la lista y que no queden tan pegados.
- Con esto ya podemos cargar datos de fuentes externas a nuestra aplicación.
- Existen muchas otras formas de hacer esto como usar [Axios](https://axios-http.com/docs/intro) en lugar de fetch, usar [GraphQL con Apollo](https://www.apollographql.com/docs/react) o usar algo como [React Query](https://tanstack.com/query/latest).
