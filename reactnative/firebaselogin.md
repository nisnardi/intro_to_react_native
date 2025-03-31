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
import React from "react";
import { View, Text } from "react-native";

export default function Home() {
  return (
    <View>
      <Text>home</Text>
    </View>
  );
}
```

- Con este setup ahora podemos navegar a la Home screen luego de autenticar al usuario.
