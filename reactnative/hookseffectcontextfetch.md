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
- Podes aprender más sobre `useState` leyendo la [documentación de React](https://react.dev/reference/react/useState).

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
- Podes aprender más sobre `useEffect` leyendo la [documentación de React](https://react.dev/reference/react/useEffect).

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

### useContext

- `Context` nos permite pasar propiedades a lo largo del árbol de componentes de una manera simple sin tener que pasar las propiedades a cada componente hijo.
- El siguiente no es código válido sino más bien para simular / Imaginar una situación.
- Supongamos que tenemos el siguiente árbol de componentes:

```javascript
const value = 1;
<Contenedor value={value}>
  <ComponenteHijo value={value}>
    <ComponenteNieto value={value}>
      <ComponenteBisnieto value={value} />
    </ComponenteNieto>
  </ComponenteHijo>
</Contenedor>;
```

- En el caso de que el `ComponenteBisnieto` necesita usar el valor `value` debemos pasar el valor como propiedad desde el componente `Contenedor` hasta el `ComponenteBisnieto`.
- Esto se conoce como `props drill` que se produce cuando un componente padre transmite datos a sus hijos y éstos a su vez los transmiten a sus propios hijos. Este proceso puede continuar indefinidamente. Al final, es una larga cadena de dependencias de componentes que puede ser difícil de gestionar y mantener.
- Para evitar este tipo de problema React creó `Context` que es un contexto.
-

```javascript
const value = 1;

<Context value={value}>
  <Contenedor>
    <ComponenteHijo>
      <ComponenteNieto>
        <ComponenteBisnieto />
      </ComponenteNieto>
    </ComponenteHijo>
  </Contenedor>
</Context>;
```

- Como vemos en este ejemplo los componentes no tienen que pasar la propiedad value hasta el componente que lo necesita utilizar ya que internamente usando `useContext` vamos a poder acceder al componente `Context` que tiene el valor.

```javascript
const value = 1;

<Context value={value}>
  <Contenedor>
    <ComponenteHijo>
      <ComponenteNieto>
        <Context value={2}>
          <ComponenteBisnieto />
        </Context>
      </ComponenteNieto>
    </ComponenteHijo>
  </Contenedor>
</Context>;
```

- Los componentes que usan `useContext` se "conectan" al contexto más cercano.
- En este caso `ComponenteBisnieto` usaría 2 como valor de `value` y todo el resto de los componentes usarían 1 ya que el `Context` más cercano tiene value seteado en 1.
- `Context` está diseñado para compartir datos que pueden considerarse **globales** para el árbol de componentes React.
- Por ejemplo podríamos usar Context para compartir el usuario que está logeado, el Theme seleccionado o el idioma preferido.
- Context se utiliza principalmente cuando algunos datos deben ser accesibles por muchos componentes en diferentes niveles de anidamiento.
- Es importante recordar usarlo con moderación porque dificulta la reutilización de componentes ya que genera un dependencia externa entre el Componente y el Contexto.
- Ahora imaginames el caso donde `ThemeComponent` necesita acceder al Theme que está definido en el Contexto que es la pantalla principal.
- Tenemos la siguiente jerarquia de componentes:

```javascript
<Contexto>
  <ThemeParentComponent>
    <ThemedComponent />
  </ThemeParentComponent>
</Contexto>
```

```javascript
// app/contexto.tsx
import React, { createContext, useState } from "react";
import { View, StyleSheet } from "react-native";
import { ThemeParentComponent } from "@/components/ThemeParentComponent";

export type Theme = "light" | "dark";

interface ThemeContextType {
  theme: Theme;
  setTheme: (theme: Theme) => void;
}

export const ThemeContext =
  createContext <
  ThemeContextType >
  {
    theme: "light",
    setTheme: () => {},
  };

export default function Contexto() {
  const [theme, setTheme] = useState < Theme > "light";

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <View style={styles.container}>
        <ThemeParentComponent />
      </View>
    </ThemeContext.Provider>
  );

  return;
}

const styles = StyleSheet.create({
  container: { flex: 1 },
});
```

- Contexto crea un contexto con el nombre `ThemeContext` y le asigna como valor un objeto con una propiedad `theme` y una función que se llama `setTheme`.
- Luega crea una variable de estado con el nombre `theme` para poder guardar el theme seleccionado.
- Usando `ThemeContext.Provider` podemos crear un componente que funciona como contexto para compartir el valor con todos los otros componentes.
- Usamos la propiedad `value` que es algo propio de `Provider` para compartir el valor entre componentes.

```javascript
// components/ThemeParentComponent.tsx
import { View, Text } from "react-native";
import { ThemedComponent } from "./ThemedComponent";

export const ThemeParentComponent = () => {
  return (
    <View style={{ flex: 1, backgroundColor: "#CCC", padding: 20 }}>
      <Text>Componente Padre</Text>
      <ThemedComponent />
    </View>
  );
};
```

- Este componente sólo lo agregamos para que sea una capa en el medio entre Contexto y el componente `ThemedComponent` que es el que finalmente usa el contexto.

```javascript
//components/ThemedComponent.tsx
import React, { useContext } from "react";
import { View, StyleSheet, Text, TouchableOpacity } from "react-native";
import { ThemeContext } from "@/app/contexto";

export function ThemedComponent() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <View
      style={[
        styles.container,
        {
          backgroundColor: theme === "light" ? "white" : "black",
        },
      ]}
    >
      <Text style={{ color: theme === "light" ? "black" : "white" }}>
        Componente Hijo
      </Text>
      <Text
        style={[styles.text, { color: theme === "light" ? "black" : "white" }]}
      >
        Current Theme: {theme}
      </Text>
      <TouchableOpacity
        onPress={() => setTheme(theme === "light" ? "dark" : "light")}
        style={{
          marginTop: 10,
          padding: 10,
          backgroundColor: theme === "light" ? "blue" : "red",
          borderRadius: 5,
        }}
      >
        <Text style={{ color: "white", fontSize: 18 }}>Toggle Theme</Text>
      </TouchableOpacity>
    </View>
  );
}
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: { fontSize: 20 },
});
```

- Este componente usa `const { theme, setTheme } = useContext(ThemeContext)` para decirle a React que vamos a usar un contexto.
- En este ejemplo estamos usando el contexto `ThemeContext` que creamos en el componente `Contexto`.
- Este contexto tiene en value el objeto con la propiedad `theme` que es el valor del estado y `setTheme` que nos permite cambiarlo.
- Desde el componente podemos hacer uso de theme para saber si es `ligth` o `dark` y actuar en consecuencia.
- Al precionar el botón llamamos para cambiar el estado del Componente Contexto y automáticamente se re-renderiza los componentes hijos.
- Este ejemplo está funcionando sin tener que pasar la propiedad theme de `Componente -> ThemeParentComponent -> ThemedComponent` evitando el props drill.
- Podes aprender más sobre `useContext` leyendo la [documentación de React](https://react.dev/reference/react/useContext).

### useRef

- `useRef` es un hook de React que permite hacer referencia a un valor que no es necesario para el renderizado.

```javascript
import React, { useRef, LegacyRef } from "react";
import { TextInput, View, Button, StyleSheet } from "react-native";

export default function Referencia() {
  const inputRef = useRef<TextInput>(undefined);

  const onPressHandler = () => {
    if (inputRef?.current) {
      inputRef.current.focus();
    }
  };

  return (
    <View style={styles.container}>
      <TextInput
        ref={inputRef as LegacyRef<TextInput>}
        placeholder="Presionar el botón para hacer foco en el Input..."
        style={styles.input}
      />
      <Button title="Enfocar Intput" onPress={onPressHandler} />
    </View>
  );
}

const styles = StyleSheet.create({
  input: {
    borderBottomWidth: 1,
    borderBottomColor: "gray",
    fontSize: 18,
    paddingVertical: 5,
  },
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});

```

- Por ejemplo en este caso creamos una referencia usando `useRef` con el nombre `inputRef` y asignamos esta referencia al componente `TextInput` usando la propiedad `ref`.
- Una vez que creamos + asignamos la referencia la podemos utilizar.
- Necesitamos encontrar una forma de poder establecer el foco en el `TextInput` pero la realidad es que no tenemos forma con las propiedades que nos da.
- Usando una referencia al `TextInput` podemos llamar al método `focus` al presionar un botón.
- Podes aprender más sobre `useRef` leyendo la [documentación de React](https://react.dev/reference/react/useRef).

### useMemo

- `useMemo` es un hook de React que permite almacenar en caché el resultado de un cálculo entre repeticiones.
- Usando `useMemo` podemos evitar tener que hacer cálculos 'caros' para evitar consumir más memoria en cada render o tener renders lentos.
- Dado que una función al ser llamada con unos parámetros retorna siempre el mismo valor, esto significa que mientras los parámetros no cambien, el valor de retorno tampoco.
- Usando este concepto `useMemo` llama a la función una vez, guarda el resultado y hasta que los parámetros no cambien no vuelve a llamar a la función y de esta manera hacer nuestros renders más performantes evitando cálculos que no son necesarios sobre todo para operaciones dificiles de calcular.

```javascript
import React, { useState, useMemo } from "react";
import { View, Text, TouchableOpacity, StyleSheet } from "react-native";

export default function Memoria() {
  const [numero, setNumero] = useState(0);

  const cuadrado = useMemo(() => {
    console.log("Calculando el cuadrado del número...");
    return numero * numero;
  }, [numero]);

  const onPressHandler = () => setNumero(numero + 1);

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Valor del Cuadrado: {cuadrado}</Text>
      <Text style={styles.text}>Valor del Cuadrado: {cuadrado}</Text>
      <TouchableOpacity onPress={onPressHandler} style={styles.button}>
        <Text>Incrementar el valor del número</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: { fontSize: 20 },
  button: {
    padding: 10,
    backgroundColor: "#CCC",
    borderRadius: 5,
    marginTop: 10,
  },
});
```

- En este ejemplo creamos una variable de estado con el nombre de número y le asignamos un valor inicial de 0.
- Al presionar el botón incrementamos el valor de la variable número.
- Usando `useMemo` se calcula un nuevo valor que es el cuadrado del número que está en la variable de estado.
- Cuando la variable de estado `numero` cambia entonces `useEffect` sabe que tiene que calcular el valor de nuevo.
- Cuando llamamos el valor `cuadrado` una segunda vez, como `useEffect` ya calculo el valor no vuelve a calcularlo y utiliza el valor que tiene en caché.
- De esta manera cuando tenemos operaciones que puden ser costosas para el dispositivo procesar, podemos usar `useMemo` para sólo calcular los valores una vez hasta que algo cambie.
- Podes aprender más sobre `useMemo` leyendo la [documentación de React](https://react.dev/reference/react/useMemo).

### useCallback

- `useCallback` es un hook de React que permite guardar en caché la definición de una función entre repeticiones.
- Es similar a `useMemo` pero en lugar de usar valores usa funciones.
- `useCallback` es útil cuando pasamos como propiedad a un componente envuelto en `React.memo`. De esta forma `React.memo` detecta que es la misma referencia y omite re-renderizar el componete hijo si el valor no ha cambiado. Memoization permite que el componente sólo vuelva a renderizar si las dependencias han cambiado.
- También es útil si la función que se pasa como parámetro se utiliza más tarde como dependencia de algún hook. Se usa en otro useCallback o en useEffect.

```javascript
import React, { useState, useCallback, useRef, memo } from "react";
import { View, Text, TouchableOpacity, StyleSheet } from "react-native";

const ComponenteBotonHijo = memo(({ onPress }: { onPress: () => void }) => {
  console.log("Componente Hijo se re-renderizó!");
  return (
    <TouchableOpacity onPress={onPress} style={styles.button}>
      <Text style={styles.textButton}>Botón del componente hijo</Text>
    </TouchableOpacity>
  );
});

export default function Callback() {
  const [count, setCount] = useState(0);

  const handlePress = useCallback(() => {
    console.log("Se apretó el botón");
  }, []);

  const functionRef = useRef(handlePress);

  console.log(
    "Es la función y la referencia el mismo valor?",
    functionRef.current === handlePress
  );

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Contador: {count}</Text>
      <ComponenteBotonHijo onPress={handlePress} />
      <TouchableOpacity
        onPress={() => setCount(count + 1)}
        style={styles.button}
      >
        <Text style={styles.textButton}>Actualizar en +1 el contador</Text>
      </TouchableOpacity>
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
    fontSize: 24,
    marginBottom: 20,
  },
  button: {
    marginTop: 10,
    padding: 10,
    backgroundColor: "#CCC",
    borderRadius: 5,
  },
  textButton: {
    color: "black",
  },
});
```

- En este ejemplo usamos `React.memo` para memorizar el componente.
- Este componente se va a volver a renderizar `solo` si la propiedad `onPress` cambia.
- Dado que en el componente que usa al componente memorizado definimos el handler usando `useCallback` la función crea una referencia una vez y no vuelve a cambiar. Esto hace que al ser pasada al componente mememorizado no se tenga que re-renderizar de nuevo.
- Podemos decir que esto es una optimización para evitar re-renders necesarios.
- El componente Callback tiene una referencia a la función handlePress `const functionRef = useRef(handlePress)` para guardar la referencia y saber si este valor cambia en cada renderizado.
- Podemos ver que al utilzar `useCallback` la referencia se mantiene siempre la misma en lugar de ser re-creado en cada render:

```javascript
const handlePress = () => {
  console.log("Se apretó el botón");
};

// VS

const handlePress = useCallback(() => {
  console.log("Se apretó el botón");
}, []);
```

- En el primer caso cada vez que el componente se renderiza estamos creando y asignando una nueva función.
- En el segundo caso la primera ver se va a ejecutar useCallback, llamar a la función que pasamos por parámetro y devolver una referencia. Esta referencia se mantiene contaste entre renders y eso hace que React no re-renderize el componente que usa `memo`.
- Para este ejemplo esto es un overkill porque es mucho control para un ejemplo simple pero en aplicaciones más complejas podemos necesitar usar este tipo de técnicas para mejorar la performance de nuestros componentes.
- Podes aprender más sobre `useCallback` leyendo la [documentación de React](https://react.dev/reference/react/useCallback).
- También podes aprender más sobre `React.memo` leyendo la [documentación de React](https://react.dev/reference/react/memo).

### useReducer

- `useReducer` es un hook de React que permite añadir un reductor a tu componente para actualizar estados complejos.
- En programación, particularmente con frameworks como `Redux y useReducer de React`, un **reductor** o reducer es una función pura que toma el estado actual y una acción como parámetros, y devuelve un nuevo estado basado en esas valores de entradas.
- Este hook toma dos parámetros. El primero es una función que va a trabajar como reducer y el segundo parámetro es el valor inicial del estado.
- `useReducer` retorna el estado como hace `useState` y una función que vamos a llamar `dispatch`.
- `dispatch` es diferente que la función que nos da `useState` aún si las dos se usan para actualizar el estado.
- `dispatch` toma como parámetro un objeto que tiene una propiedad con el nombre `type`.
- El reducer va a recibir el estado inicial como primer parámetro y una acción como segundo valor.
- Veamos un ejemplo:

```javascript
import React, { useReducer } from "react";
import { View, Text, TouchableOpacity, StyleSheet } from "react-native";

type Action = "increment" | "decrement";

function reducer(state: { count: number }, action: { type: Action }) {
  console.log(action);
  console.log(state);

  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
}

export default function Achicar() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Count: {state.count}</Text>
      <View style={styles.buttonsContainer}>
        <TouchableOpacity
          onPress={() => dispatch({ type: "increment" })}
          style={styles.button}
        >
          <Text style={[styles.textButton, { color: "#ffff00" }]}>+</Text>
        </TouchableOpacity>
        <TouchableOpacity
          onPress={() => dispatch({ type: "decrement" })}
          style={[styles.button, { backgroundColor: "#ffff00" }]}
        >
          <Text style={[styles.textButton, { color: "darkblue" }]}>-</Text>
        </TouchableOpacity>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    alignItems: "center",
    marginTop: 50,
  },
  text: {
    fontSize: 24,
  },
  button: {
    padding: 10,
    backgroundColor: "darkblue",
    borderRadius: 5,
  },
  textButton: {
    color: "white",
    fontSize: 24,
  },
  buttonsContainer: {
    flexDirection: "row",
    gap: 10,
    marginTop: 10,
  },
});
```

- En este ejemplo vemos que tenemos una función reducer con el nombre de `reducer`.
- Esta función toma dos parámetros, el estado inicial y la acción que tiene que manejar.
- Utiliza un switch statement para manejar diferentes opciones de tipos de acciones que maneja este reducer.
- En este caso maneja `increment` para sumar 1 al estado y `decrement` para reducir el valor en 1.
- De esta forma le estamos dando un contexto a lo que estamos cambiando.
- El reducer tiene que siempre devolver un nuevo estado.
- Si ningún `action.type` matchea con alguno de los actions que maneja el reducer va a retornar el estado por `default`.
- Los botones utilizar `dispatch()` para usar `incremenet` or `decrement` para cambiar el estado.
- Dado que useReducer devuelve el nuevo valor del estado, React va a re-renderizar el componente.
- Esta forma de trabajar se parece mucho a utilizar `Redux` donde tenemos conceptos similares pero en este caso estamos usando lo que React nos da.
- Podes aprender más sobre `useReducer` leyendo la [documentación de React](https://react.dev/reference/react/useReducer).
- Con todo esto aprendimos un montón sobre hooks! Felicitaciones!!

![Aprendiste Hook's](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExNHZwNGE1MjdzbXhicGdzcm02Zmx1M2R4bmlhZWhrZWJiaThkOHEzbiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/9p8hgZoQjj9y8/giphy.gif)

[App de ejemplo](https://github.com/nisnardi/effect-context-fetch)

#### Extra

[Tutorial React hooks | Todos los React hooks explicados 🪝](https://www.youtube.com/watch?v=jaLl4ErmU44)
