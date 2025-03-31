# React Native

## Firebase Login

- Firebase es una plataforma creada por Google que te ayuda a crear aplicaciones más rápido, sin necesidad de escribir un backend completo.
- Podemos pensar a Firebase como un backend como servicio (BaaS) - te da herramientas para manejar cosas como:

  - 🔐 Autenticación: Permite a los usuarios iniciar sesión (correo electrónico, Google, Apple, Facebook, etc.).
  - 🗄️ Base de datos Firestore: Una base de datos NoSQL en tiempo real que sincroniza los datos al instante entre usuarios /dispositivos.
  - 💾 Almacenamiento: Almacena archivos como imágenes, vídeos y documentos.
  - 💬 Mensajería cloud: Envía notificaciones push (como cuando alguien te envía un mensaje).
  - ☁️ Cloud Functions: Escribe lógica de backend personalizada en Node.js y ejecútala en la nube.
  - 📈 Analytics: Rastrea el comportamiento de los usuarios dentro de tu app.
  - 🛡️ Reglas de seguridad: Controla quién puede leer / escribir datos o usar funciones específicas.
  - 💡 Configuración remota: Cambia el comportamiento de la app sin actualizarla en las tiendas de aplicaciones.

- En esta sección vamos a aprender sobre Autenticación usando Firebase.

### ¿Por qué usar Firebase?

- Puedes construir y escalar aplicaciones rápidamente.
- No necesitas configurar tu propio backend.
- Ideal para aplicaciones móviles y web (React Native, Expo, Flutter, etc.).
- Utilizado por muchas startups e incluso grandes empresas.

## Configurar el proyecto Firebase

- Lo primero que tenemos que hacer es [ir a la consola Firebase](https://firebase.google.com) y crear un projecto.
- En Project Overview vemos un banner `Get started by adding Firebase to your App`.
- Seleccionamos la opción `</>` para crear un proyecto web.
- Registra la app unsando cualquier nombre que quieras para tu proyecto.
- En la sección de Add Firebase SDK te va a dar unas credenciales tipo:

```javascript
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";

// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: ""
  authDomain: "",
  projectId: "",
  storageBucket: "",
  messagingSenderId: "",
  appId: "",
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
```

- Guardamos estos datos en algún lado ya que los vamos a necesitar para utilizar firebase dentro de nuestro proyecto.

## Instalar Firebase

- Para poder usar Firebase debemos installar el módulo de firebase en nuestro proyecto.

```bash
$ npm install firebase
```

- Una vez instalado debemos configurar nuestro projecto.
- Creamos un archivo de configuración con el nombre `firebaseConfig.js` con los datos que nos dió Firebase:

```javascript
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";

const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "TU_PROJECT_ID.firebaseapp.com",
  projectId: "TU_PROJECT_ID",
  storageBucket: "TU_PROJECT_ID.appspot.com",
  messagingSenderId: "TU_SENDER_ID",
  appId: "TU_APP_ID",
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);

export { auth };
```

## Crear pantalla de Login

- Ahora que está configurado el proyecto podemos crear la pantalla inicial de login en `app/index.tsx`.

```javascript
// app/index.tsx
import React, { useState } from "react";
import { View, TextInput, Button, Text, StyleSheet } from "react-native";
import { signInWithEmailAndPassword } from "firebase/auth";
import { auth } from "@/firebaseConfig";
import { router } from "expo-router";

export default function Index() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [error, setError] = useState("");

  const handleLogin = async () => {
    try {
      const user = await signInWithEmailAndPassword(auth, email, password);
      console.log(user);

      setError("");

      router.navigate("/(protected)/home");
    } catch (err) {
      setError(err.message);
    }
  };

  return (
    <View style={styles.container}>
      <TextInput
        placeholder="Email"
        value={email}
        onChangeText={setEmail}
        style={styles.input}
        autoCapitalize="none"
      />
      <TextInput
        placeholder="Password"
        value={password}
        onChangeText={setPassword}
        secureTextEntry
        style={styles.input}
      />
      {error ? <Text style={styles.error}>{error}</Text> : null}
      <Button title="Login" onPress={handleLogin} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", padding: 16 },
  input: { borderWidth: 1, marginBottom: 10, padding: 8 },
  error: { color: "red", marginBottom: 10 },
});
```

- Firebase nos da una función con el nombre `signInWithEmailAndPassword` que nos permite validar un usuario creado en Firebase.
- De esta forma podemos crear usuarios en un servidor remoto y validar los datos contra esa cuenta.
- Una vez que tenemos esto funcionando podemos optar por buscar como usar Google o Facebook login que son otros servicios que nos brinda Firebase.
- En este ejemplo una vez que autenticamos al usuario, navegamos a la pantalla `(protected)/home.tsx`.
- Creamos la carpeta `(protected)`.
- Creamos el archivo `(protected)/_layout.tsx` con el siguiente código:

```javascript
// (protected)/_layout.tsx
import { Stack } from "expo-router";

export default function ProtectedLayout() {
  return <Stack />;
}
```

- Ahora creamos `(protected)/home.tsx` con el siguiente código:

```javascript
import { Link } from "expo-router";
import React from "react";
import { View, Text } from "react-native";

export default function Home() {
  return (
    <View>
      <Text>home</Text>
      <Link href="./todos">Ir a Todos</Link>
    </View>
  );
}
```

- Con este setup ahora podemos navegar a la Home screen luego de autenticar al usuario.
- Podes aprender más sobre Firebase leyendo la [documentación oficial](https://firebase.google.com/?hl=es-419)

## Usando Firebase Firestore

- Firestore es una base de datos NoSQL en la nube de Firebase, ideal para la sincronización en tiempo real y escalable.
- Firebase tiene una sección llamada `Project Overview` que está en la barra de la izquierda.
- Dentro de esa página hay una sección con el nombre CloudFirestore.
- En esta sección podemos crear una nueva base de datos (`Create database`).
- Nos pide unos datos como el ID de la base de datos y la location pero sólo presionamos `Next` para crear la base con la configuración básica.
- En la sección de `Secure Rules` podemos dejar la base de datos en modo producción.
- Firestore va a crear una base de dato `default` para que puedas utilizar.
- Al principio es una base de datos vacía por lo cual tenemos que crear una colección.
- Presionamos `Start Collection` para crear una nueva colección con el nombre `todos`.
- Como regla nos pide que creemos un primer item y creamos un documento con Auto-ID y 2 campos de textos (Podes usar `Add field`):

  - Document ID: usamos `Auto-ID`.
  - Fields:
    - Field: title Type: string Value: 'Primer todo'.
    - Field: completed Type: boolean Value: false.

- Dentro de la página de Cloud Firestore hay una sección que dice `Rules` que está en el tab siguiente a `Data` donde podemos ver nuestros datos.
- Vas a ver unas reglas similares a estas:

```javascript
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

- Tenemos que cambiar la linea `allow read, write: if false;` para que no sea falsa y podamos escribir.
- Modificamos ese código por: `request.auth != null;`
- La regla debería quedar así:

```javascript
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

- Este paso lo hacemos ya que te puede dar el siguiente error al querer usar esta base de datos:

```bash
 (NOBRIDGE) ERROR  [2025-03-31T21:58:49.963Z]  @firebase/firestore: Firestore (11.5.0): Uncaught Error in snapshot listener: FirebaseError: [code=permission-denied]: Missing or insufficient permissions.
```

- Ahora que ya tenemos la base de datos de Firestore configurada podemos utilizarla.
- Creamos un nuevo documento en la carpeta `(protected)` con el nombre de `todos.tsx` y pegamos el siguiente código:

```javascript
import React, { useState, useEffect } from "react";
import {
  View,
  Text,
  TextInput,
  Button,
  FlatList,
  TouchableOpacity,
  StyleSheet,
} from "react-native";
import { db } from "@/firebaseConfig";
import {
  collection,
  addDoc,
  deleteDoc,
  doc,
  onSnapshot,
  updateDoc,
} from "firebase/firestore";

export default function Todos() {
import React, { useState, useEffect } from "react";
import {
  View,
  Text,
  TextInput,
  Button,
  FlatList,
  TouchableOpacity,
  StyleSheet,
} from "react-native";
import { db } from "@/firebaseConfig";
import {
  collection,
  addDoc,
  deleteDoc,
  doc,
  onSnapshot,
  updateDoc,
} from "firebase/firestore";

export default function Todos() {
  const [task, setTask] = useState("");
  const [todos, setTodos] = useState([]);

  useEffect(() => {
    const unsubscribe = onSnapshot(collection(db, "todos"), (snapshot) => {
      const list = snapshot.docs.map((doc) => ({
        id: doc.id,
        ...doc.data(),
      }));
      setTodos(list);
    });

    return unsubscribe;
  }, []);

  const addTodo = async () => {
    if (task.trim()) {
      await addDoc(collection(db, "todos"), {
        title: task,
        completed: false,
      });
      setTask("");
    }
  };

  const toggleComplete = async (id, current) => {
    const todoRef = doc(db, "todos", id);
    await updateDoc(todoRef, {
      completed: !current,
    });
  };

  const deleteTodo = async (id) => {
    await deleteDoc(doc(db, "todos", id));
  };

  const renderItem = ({ item }) => (
    <View style={styles.todoItem}>
      <TouchableOpacity onPress={() => toggleComplete(item.id, item.completed)}>
        <Text
          style={{
            textDecorationLine: item.completed ? "line-through" : "none",
          }}
        >
          {item.title}
        </Text>
      </TouchableOpacity>
      <Button title="Borrar" onPress={() => deleteTodo(item.id)} />
    </View>
  );

  return (
    <View style={styles.container}>
      <TextInput
        placeholder="Ingrese un nuevo Todo"
        value={task}
        onChangeText={setTask}
        style={styles.textInput}
      />
      <Button title="Agregar Todo" onPress={addTodo} />

      <FlatList
        data={todos}
        keyExtractor={(item) => item.id}
        renderItem={renderItem}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 20, marginTop: 50 },
  textInput: {
    borderWidth: 1,
    padding: 10,
    marginBottom: 10,
    borderRadius: 5,
  },
  todoItem: {
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    padding: 10,
    backgroundColor: "#f9f9f9",
    marginBottom: 5,
    borderRadius: 5,
  },
});

```

- Ahora al navegar a Home tenemos un Link que nos lleva a la pantalla de Todo's.
- En esta pantalla tenemos un campo de texto para agregar un nuevo Todo.
- Al ingresar un texto y presionar el botón que dice `Agregar Todo` se va a crear un nuevo Todo en la base de datos `todos` de Firestore.
- Automáticamente vemos que el Todo es agregado a la lista de nuestra aplicación en tiempo real.
- Podemos borrar un Todo presionando el botón Borrar y lo borra tanto de nuestra App como de Firestore.
- También podemos marcar un todo como terminado por medio de presionar el texto del todo.
- Ahora que entendemos como funciona la pantalla vamos a ver el código por secciones:

```javascript
import { db } from "@/firebaseConfig";
```

- Para poder interactuar con Firebase / Firestore necesitamos tener accesso al servicio y eso lo hacemos importando `db` del archivo de configuración de Firebase.

```javascript
import {
  onSnapshot,
  collection,
  doc,
  addDoc,
  deleteDoc,
  updateDoc,
} from "firebase/firestore";
```

- Al instalar el módulo de `firebase` también installamos firestore.
- Este módulo nos da todo lo que necesitamos para interactuar con la base de datos.
- Firestore tiene 2 formas de obtener datos de la base de datos.
- Podemos usar `get` para llamar a la base de datos o podemos utilizar `onSnapshot` para tener un `listener` que se comunique entre nuestra App y la base de datos para mantener en sync.
- `collection` permite establecer cuál es la colección que vamos a utilizar. Acepta una conección `db` y el nombre de la colección que queremos utilizar. En nuestro ejemplo va a ser `collection(db, 'todos')` ya que usamos `todos` como nombre de la colección y `db` es la conección que creamos en la configuración.
- `doc` nos permite fererenciar un documento en la base de datos. `doc(db, 'todos', id)`. Le pasamos 3 parámetros, la base de datos, el nombre de la colección y finalmente el id del documento que queremos.
- `addDoc, deleteDoc y updateDoc` permiten agregar, borrar y actualizar un documento de la base de datos.

```javascript
const [task, setTask] = useState("");
const [todos, setTodos] = useState([]);
```

- Esta pantalla va a utilizar 2 variables de estado.
- `task` es la variable temporal para crear un nuevo todo. Se va a utilizar como texto temporal dentro del campo de texto para crear el Todo.
- `todos` son todos los todos que tenemos en la base de datos.

```javascript
return (
  <View style={styles.container}>
    <TextInput
      placeholder="Ingrese un nuevo Todo"
      value={task}
      onChangeText={setTask}
      style={styles.textInput}
    />
    <Button title="Agregar Todo" onPress={addTodo} />

    <FlatList
      data={todos}
      keyExtractor={(item) => item.id}
      renderItem={renderItem}
    />
  </View>
);
```

- En la pantalla vemos 3 componentes que están envueltos por un View que funciona como container.
- El TextInput nos permite ingresar un valor como titulo de nuestro todo.
- Acepta la variable de estado `task` para mantener el nombre del título del todo.
- Al ingresar un valor nuevo se va a ejecutar la funci´øn `setTask`.
- El Button tiene el título `Agregar Todo` y cuando se lo presione va a llamar a `addTodo`.
- Finalmente tenemos un FlatList que toma la colección de `todos` como data.
- Inicialmente es una colección vacía.
- También usa la función `renderItem` para renderirzar un componente por cada item de la colección todos.
- Analizemos ahora como se ejecuta el primer render de este componente:

```javascript
useEffect(() => {
  const unsubscribe = onSnapshot(collection(db, "todos"), (snapshot) => {
    const list = snapshot.docs.map((doc) => ({
      id: doc.id,
      ...doc.data(),
    }));
    setTodos(list);
  });

  return unsubscribe;
}, []);
```

- Por medio de `useEffect(() => {}, [])` sabemos que este efecto se ejecuta una vez al renderizar el componente.
- Dentro de este efecto llamamos a `onSnapshot` para crear una conección con el servidor que va a estar manejando los cambios con la base de datos. Esta función devuelve una subscripción.
- Esta función acepta 2 parámetros.
  - `collection(db, "todos")`: el primer parámetro establece cual va a ser la colección que va a estar manejando.
  - `(snapshot) => {}`: el segundo parámetro es un callback que se va a ejecutar cuando algo cambie.

```javascript
const list = snapshot.docs.map((doc) => ({
  id: doc.id,
  ...doc.data(),
}));

setTodos(list);
```

- En el cuerpo del callback de useSnapshot obtenemos los todos y los recorremos para crear un documento con `id` y las propiedades que tiene el item en la base de datos `(title, completed)`.
- Una vez obtenidos los datos podemos setear la colección en la variable de estado de `todos` usando `setTodos(list)`.
- Con esto estamos trayendo todos los todos de la base de datos y seteandolos localmente en nuestro componente.
- Finalmente el useEffect limpia la subscripción a la base de datos cuando el componente se desmonte.

```javascript
return unsubscribe;
```

- Ahora que entendemos la carga podemos ver como se crea un nuevo todo:

```javascript

const [task, setTask] = useState("");

const addTodo = async () => {
  if (task.trim()) {
    await addDoc(collection(db, "todos"), {
      title: task,
      completed: false,
    });
    setTask("");
  }
};

<TextInput
  placeholder="Ingrese un nuevo Todo"
  value={task}
  onChangeText={setTask}
  style={styles.textInput}
/>
<Button title="Agregar Todo" onPress={addTodo} />
```

- El TextInput usa `task` para manejar el título de un todo.
- Al presionar una letra se ejecuta `setTask` para cambiar el valor de la variable `task`.
- Cuando presionamos el botón se ejecuta `addTodo`.
- `addTodo` es una función `asyn` ya que vamos a utilizar `await`.
- usamos `task.trim()` para borrar los espacios del valor que estaba en el campo de texto y si al borrar los espacios del costado del texto sigue habiendo texto, entonces significa que hay un texto que guardar.
- usamos `addDocument` para agregar un nuevo documento en la base de datos.
- Dado que necesitamos saber cual es la colección usamos `collection(db, "todos")` y le pasamos como segundo parámetro el objto que queremos crear. En este caso es un objeto con la propiedades title y completed.
- Usamos como título de nuestro todo el valor que tenemos guardado en la variable de estado `task`.
- Inicialmente a crear un Todo podemos setear el valor `completed` en false ya que recién lo estamos creando.
- Finalmente llamamos a `setTask` para borrar el contenido del campo de texto luego de crear un Todo.
- Ahora nos toca borrar o editar un Todo y para eso tenemos que ver que se renderiza por cada Todo:

```javascript
const renderItem = ({ item }) => (
  <View style={styles.todoItem}>
    <TouchableOpacity onPress={() => toggleComplete(item.id, item.completed)}>
      <Text
        style={{
          textDecorationLine: item.completed ? "line-through" : "none",
        }}
      >
        {item.title}
      </Text>
    </TouchableOpacity>
    <Button title="Borrar" onPress={() => deleteTodo(item.id)} />
  </View>
);
```

- En este componente estamos haciendo un par de cosas.
- Al presionar el título del Todo se llama a `toggleComplete` pasandole como parámetro el `id y completed` del todo seleccionado.
- Al presionar borrar se llama a la función `deleteTodo` pasando como parámetro el `id` del todo a borrar.

```javascript
const toggleComplete = async (id, current) => {
  const todoRef = doc(db, "todos", id);
  await updateDoc(todoRef, {
    completed: !current,
  });
};
```

- `toggleComplete` es una función `async` ya que vamos a utilizar `await`.
- Esta función recibe 2 parámetros, el id del todo que queremos actualizar y el valor actual del todo si está completado o no.
- usando `doc` podemos buscar al todo que está en la base de datos en la colección `todos` con el `id` que pasamos como parámetro que sabemos es el que el usuario hizo press en el título.
- El valor current es boolean y nos da el estado actual de este Todo. Usando el concepto de toggle podemos decir que un valor va a pasar de `true` a `false` y de `false` a `true`.
- Una vez que encontramos el documento que queremos modificar, `doc` nos devuelve una referencia a ese documento.
- Con esa referencia podemos utilizar `updateDoc` para actualizar el documento pasando la referencia como primer parámetro y un objeto con lo que queremos modificar. En este caso `{completed: !current}` le dice a Firestore que tiene que actualizar la propiedad completed del todo de la referencia usando el valor inverso de lo que le pasamos como `currnent` (parámetro).
- De esta forma seleccionamos el todo y actualizamos el valor de completed al valor opuesto de lo que tenía en el momento de presionar el todo.
- Para borrar hacemos algo similar:

```javascript
const deleteTodo = async (id) => {
  await deleteDoc(doc(db, "todos", id));
};
```

- `deleteTodo` es una función `async` porque también vamos a utilizar `await`.
- Usando `deleteDoc` podemos borrar un documento de la base de datos.
- De nuevo por medio de `doc` podemos buscar un documento en la base de datos y luego lo va a borrar.
- Cualquier operación que hacemos se va a reflejar en nuestro componente ya que se llama el callback que usa `onSnapshot`.
- Esto es una simple introducción / ejemplo de como usar una base en tiempo real que nos permite seguir aprendiendo y usando este servicio para plasmar muchas ideas.
- Podes aprender más sobre Firestore leyendo la [documentación oficial](https://firebase.google.com/docs/firestore?hl=es).

## Agregando validación

- `Zod` es una librería de validación y declaración de esquemas que usa TypeScript.
- Es súper útil en proyectos React Native para validar formularios, respuestas API, o cualquier tipo de datos.
- En este ejemplo podemos utilizarlo para validar el email del formualrio de login.
- Lo primero que tenemos que hacer es instalar la librería:

```bash
$ npx expo install zod
```

- En `index.tsx` tenemos que importar el módulo de la siguiente manera:

```javascript
import { z } from "zod";
```

- Una vez importado debemos crear un schema que refleje los datos que queremos utilizar.
- En este formulario nosotros usamos un email y un string para el password.
- Podemos defnir el esquema de la siguiente manera:

```javascript
const schema = z.object({
  email: z.string().email("Ingrese un email con formato válido"),
});
```

- En este esquema estamos definiendo que hay un valor email que es un `string` con formato de `email`.
- `z.object` nos permite definir cual es el esquema que queremos utilizar.
- Una vez agregado el schema podemos utilizarlo para validar que el email sea una dirección de email con formato válido:

```javascript
const handleLogin = async () => {
  const result = schema.safeParse({
    email: email,
  });

  if (result.success) {
    try {
      const user = await signInWithEmailAndPassword(auth, email, password);

      setError("");

      router.navigate("/(protected)/home");
    } catch (err) {
      setError(err.message);
    }
  } else {
    setError(result.error.issues[0].message);
  }
};
```

- Usamos `safeParse` para parsear que la variable de estado email sea un string con formato de email.
- Esta validación puede ser `success` o puede tener un `error`.
- Si la validación es exitosa entonces seguimos el flow del código para autenticar al usuario.
- En caso de que hay error Zod nos va a dar un array de errores en la propiedad `result.errors`.
- Como sabemos este form tiene un solo valor que estámos manejando y podemos acceder al error con `issues[0]` ya que es el primer error y `message` para obtener el mensaje de error.
- Es decir que con result.error.issues[0].message accedemos al primer mensaje de error.
- Esta librería permite validar esquemas complejos y tiene muchas opciones.
- En este ejemplo solo la usamos para validar un email pero puede ser muy útil.
- Para aprender más podes leer la [documentación oficial](https://zod.dev/?id=introduction).
- [Zod Tutorial 1 - Español](https://www.youtube.com/watch?v=sQZPIMufppE)
- [Zod Tutorial 2 - Español](https://www.youtube.com/watch?v=bUzGfrjg66M)
- [Zod Tutorial 3 - Ingles](https://www.youtube.com/watch?v=L6BE-U3oy80)
- [Zod Tutorial 4 - Ingles](https://www.totaltypescript.com/tutorials/zod)

![ZOD](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExdGY0aTdnem9kamg0bGFtaHZvY2Vjbzd5cHRxMGFicDllOG5oYm9xbyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/cJQGB93fsnaPm/giphy.gif)

[App de ejemplo](https://github.com/nisnardi/firebase-auth)
