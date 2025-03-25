# React Native

## Principios de Redux - Manejo de estado

- `Redux` es una librería para manejo de estado global de una aplicación de forma predecible.
- Sigue tres principios básicos:
  - **Una única fuente de verdad**: El estado global se almacena en un único objeto JavaScript llamado store.
  - **El estado es de sólo lectura**: El estado sólo puede cambiarse enviando acciones.
  - **Los cambios se realizan con funciones puras**: Los reductores son funciones puras que toman el estado actual y una acción, y devuelven un nuevo estado.
- Dentro de estos conceptos Redux va a utilizar un objeto para representar el estado de nuestra aplicación y va a ser la fuente única para acceder o modificar el estado.
- Para poder cambiar el estado, un componente va a hacer un `dispatch` de una acción y alguna función `reducer` va a manejar esa accción utilizando el `tipo de acción`.
- Una `acción` no es más que un objeto de JavaScript que tiene una propiedad con el nombre `type` que nos permite en las funciones reductoras (reducers) saber si el reducer tiene que hacer alguna operación para devolver un nuevo estado.
- El estado va a tener un estado inicial con el que se inicia hasta que alguna acción haga que un reducer lo cambie.
- Una sección del estado se conoce como `slice` o una porción del estado.
- Vamos a crear un ejemplo de contador utilizando Redux.

### Instalar dependencias

- El equipo de Redux recomienda utilizar `@reduxjs/toolkit` para estructurar nuestro project.
- También necesitamos instalar `react-redux` ya que vamos a integrarlo con React (React Native).
- Ejecutamos el siguiente comando para instalar las dependencias necesarias:

```bash
npx expo install @reduxjs/toolkit react-redux
```

### Crear un Slice

- `@reduxjs/toolkit` tiene una función `createSlice` que nos permite crear una porción del estado que queremos manejar.
- `createSlice` es una función que acepta un `estado inicial`, un objeto de `funciones reductoras (reducers)` y un `nombre de estado` y genera automáticamente unas funciones que se encargan de crear `acciones` y `tipos de acciones` que se corresponden con los `reducers` y el `estado`.
- Para organizar nuestro código mejor vamos a crear una carpeta con el nombre `redux` y adentro vamos a crear otro archivo con el nombre `counterSlice.ts`.

```typescript
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;
export default counterSlice.reducer;
```

- En este ejemplo estamos creando un `slice` con el nombre de `counter` que tiene un estado inicial `{value: 0}` representado por un objeto con la propiedad value y el valor en 0.
- Esto hace que el slice counter tenga su estado inicial en 0.
- Otra de las propiedades de este slice es `reducers` que hacepta un objeto donde cada propiedad es una función que se encarga de hacer una operación y devolver un nuevo estado.
- Esta librería utiliza algo llamado [Immer](https://redux-toolkit.js.org/usage/immer-reducers) que se encarga de modifciar el valor del estado por nosotros y devolver una nueva instancia sin que lo tengamos que hacer a mano.
- Redux mantiene el concepto de React donde el estado tiene que ser inmutable y siempre tenemos que utilizar un nuevo estado (objetos y arrays como vimos).
- Dado que estamos usando Redux Toolkit nos permite hacer todo esto de una manera más simple.
- En los reducers hay una función `increment` que incrementa el valor del estado en 1.
- Otra de las funciones se llama `decrement` y reduce el valor del estado (value) en 1.
- Finalmente tenemos una acción que incrementa por un monto especial variable que se llama `incrementByAmount`.
- Todas las funciones reciben `state` como primer parámetro que representan el estado actual.
- `incrementByAmount` también recibe un segundo parámetro que es la acción que se despachó. Esta acción tiene una propiedad con el nombre de `payload` de donde podemos acceder al valor que cambió.
- Es decir que si una función reducer no necesita un valor externo para modificar el estado lo puede hacer como hacen `increment y decrement` sin necesidad de acceder a la acción.
- En el caso de necesitar hacer llegar un valor al reducer para hacer alguna operación y luego devolver el nuevo estado podemos pasarle valores usando la propiedad `payload` del action.
- Al `action` lo podemos pensar como un objeto con la siguiente forma: `{ type: 'incrementByAmount', payload: 2}`.
- `counterSlice.actions` retorna un objeto con todos los `actions` que tiene definido el slice y los exportamos para poder utilizarlos desde otro lado.
- `counterSlice.reducer` retorna los reducers que luego vamos a utilizar para crear el store de Redux.
- Ahora que sabemos como funciona `createSlice`, `actions` y `reducers` podemos crear el `store` de Redux.

### Crear el Store de Redux

- `@reduxjs/toolkit` nos da otra función con el nombre de `configureStore` que crea un `store` de Redux que contiene el árbol de estado completo de tu aplicación.
- Una de las reglas de Redux es que sólo debe haber un único almacén en tu aplicación.
- Dentro de la carpeta `redux` creamos otro archivo con el nombre `store.ts` y agregamos el siguiente código:

```typescript
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

- Creamos un nuevo `store` que va a almacenar el estado de nuestra app.
- En este caso sólo tiene un reducer con el nombre `counter` y le asignamos el `slice` que creamos en `redux/counterSlice.ts`.

### Relacionar la App con el Store

- Hasta acá tenemos configurado Redux por medio de crear un slice que luego asignamos al store.
- Para que los componentes puedan acceder al estado tenemos primero que envolver la App utilizando un Provider que va a tener el `store`. Es de alguna forma como cuando usamos Context.
- Modificamos `app/_layout.tsx` para que utilize el Provider y así darle acceso a los componentes.

```typescript
import { Stack } from "expo-router";
import { Provider } from "react-redux";

import { store } from "@/redux/store";

export default function RootLayout() {
  return (
    <Provider store={store}>
      <Stack>
        <Stack.Screen name="index" />
      </Stack>
    </Provider>
  );
}
```

- Como el Provider envuelve al Stack de navegación significa que en todas las pantallas podríamos acceder al estado.
- Le pasamos al Provider una propiedad con el nombre `store` y le asignamos la variable `store` que creamos en la sección anterior.
- De esta forma exponemos el store a todos los componentes que lo quieran consumir ya sea para leer o hacer dispatch de actions.

### Usar Redux desde los componentes

- Vamos a modificar el archivo `app/index.tsx` para crear un contador usando el estado.

```typescript
import { Text, View, StyleSheet, Button } from "react-native";
import { useSelector, useDispatch } from "react-redux";
import { RootState } from "@/redux/store";
import { increment, decrement, incrementByAmount } from "@/redux/counterSlice";

export default function Index() {
  const count = useSelector((state: RootState) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Contador: {count}</Text>
      <View style={styles.row}>
        <Button title="-" onPress={() => dispatch(decrement())} />
        <Button title="+" onPress={() => dispatch(increment())} />
      </View>
      <Button
        title="Incrementar en 5"
        onPress={() => dispatch(incrementByAmount(5))}
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
  row: {
    flexDirection: "row",
  },
  text: {
    fontSize: 24,
    marginBottom: 10,
  },
});
```

- Primero vamos a importar `useSelector y useDispatch` de `react-redux`.
- `useSelector` nos permite pasar una función que recibe como primer parámetro el estado de nuestra aplicación.
- Un selector es una función que nos permite acceder al estado y retornar una sección o valor.
- En este caso vamos a utilizar el selctor para obter el valor del slice `counter.value`.
- `useDispatch` nos va a retornar una función `dispatch` que nos va a permitir emitir o dispatchear acciones.
- Importamos los actions creators `increment, decrement, incrementByAmount` para poder interactuar con el slice.
- Al presionar alguno de los botones hacemos `dispatch(actionCreator())` para emitir una acción.

```javascript
console.log(decrement()); // {"payload": undefined, "type": "counter/decrement"}
console.log(increment()); // {"payload": undefined, "type": "counter/increment"}
console.log(incrementByAmount(5)); // {"payload": 5, "type": "counter/incrementByAmount"}
```

- Al hacer console.log de los action creators vemos que no hacen más que crear un objeto que tienen una propiedad `type` con el valor `counter/action` donde `counter` viene del nombre que le pusimos al slice.
- Los actions tienen un payload que en algunos casos tienen el valor undefined ya que no lo estamos usando y para incrementByAmount tiene el valor de 5 ya que es el valor que le pasamos al crear el action.
- Podemos instalar un plugin para poder ver el estado utilizando una dev tool.

### Instalar Redux Dev Tools

- [Expo tiene un componente para utilizar Dev Tools](https://docs.expo.dev/debugging/devtools-plugins/) que son herramientas que nos ayudan para trabajar.
- Redux tiene un plugin que se llama `redux-devtools-expo-dev-plugin`.
- Instalamos la herramienta:

```bash
$ npx expo install redux-devtools-expo-dev-plugin
```

- Una vez instalado el módulo necesitamos configurarlo de la siguiente manera:

```typescript
// redux/store.ts;
import { configureStore } from "@reduxjs/toolkit";
import devToolsEnhancer from "redux-devtools-expo-dev-plugin";

import counterReducer from "./counterSlice";

export type RootState = ReturnType<typeof store.getState>;

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
  devTools: false,
  enhancers: (getDefaultEnhancers) =>
    getDefaultEnhancers().concat(devToolsEnhancer()),
});
```

- Por último necesitamos re iniciar el servidor de metro `npx expo start` y cuando la app esté corriendo presionar en la consola `shift+m` para que Expo nos muestre más herramientas de desarrollo.

![More Tools](../assets/react-native/more_tools.png)

- Seleccionamos la opción `Open redux-devtools-expo-dev-plugin` y se debería abrir una ventana con una aplicación que nos permite ver el estado de nuestra App.
- Del lado izquierdo vamos a ver las acciones que se emiten.
- Del lado derecho tenemos `Action` para ver la acción, `State` para ver el estado, `Diff` para ver como la acción cambia al estado.
- Si ejecutamos algunas acciones luego podemos presionar el botón de play que está abajo a la izquierda y Redux reproduce los cambios en tiempo real y podemos viajar en el tiempo.
- Otro logro más, felicitaciones! ahora aprendiste las bases de Redux.

![Redux!](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExdmRqMXgxemM0NGpkNXBnZzE2eGNvYjd0bjQ2MTN1MDRnODZocWV1dSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/AP5AEWUWAERqVEP4Yv/giphy.gif)
