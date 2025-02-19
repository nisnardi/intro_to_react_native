# React Native

## Aprendiendo React

- Meta creó una librería llamada React que es muy performante para renderizar o dibujar elementos en pantalla cuando el estado de la app cambia.
- Meta creó React Native para poder utilizar React en sus proyectos mobiles.
- React se usa para proyectos Web.
- React Native cambia la forma de renderizar components en la aplicación ya que necesita crear componentes nativos para iOS y Android en lugar de HTML como se hace para Web.
- Aprender las bases de React nos ayudan a aprender las bases de React Native.
- Mucho del código que vamos a escribir / utilizar puede ser adaptado o utilizado tanto en una App React como React Native.
- React Native permite a programadores Web que saben React pasar al mundo de Mobile.
- Vamos a utilizar un proyecto de React Native para ir viendo algunos conceptos de React que luego podemos utilizar en nuestras app React Native.

### Creando componentes de React y React Native

- Un componente es una parte de la Interfaz de Usuario (UI).
- Puede tener lógica o no.
- Puede tener su propio estilo y funcionalidad.
- Al crear un componente podemos pensar en algo tan pequeño como un texto o tan grande como toda una pantalla de nuestra aplicación.
- Los componentes en React son `funciones de JavaScript` que devuelven algo que va a ser renderizado en pantalla.

```javascript
function Mensaje() {
  return <Text>Bienvenidos a React Native</Text>;
}

<Mensaje>
```

- En este ejemplo vemos un componente simple de React que utiliza una `function` para definir que esto es un componente.
- Utilizamos el nombre de la función `Mensaje` como nombre del componente y en mayúscual porque es un componente de React.
- La función devuelve un `<Text>` con el mensaje `Bienvenidos a React Native` y finalmente hay una etiqueta de cerrado del texto `</Text>`.
- Los componentes pueden tener otros componentes anidados y se conocen como `child` o hijos.
- Un concepto que da mucho poder a importancia a las componentes es que se puede reutilizar.

```javascript
function Mensaje() {
  return <Text>Bienvenidos a React Native</Text>;
}
<>
  <Mensaje />
  <Mensaje />
  <Mensaje />
</>;
```

- Si ejecutaramos un código similar veríamos en pantalla el mensaje `Bienvenidos a React Native` 3 veces.
- Si queremos cambiar el texto, sólo lo tenemos que hacer en un lugar... el componente!
- React Native nos da un componente genérico que es una vista o contenedor `<View>`.
- Tanto `<Text>` como `<View>` hay que importarlos del módulo `react-native` para poder utilizarlos.

```javascript
import { Text, View } from "react-native";

function Mensaje() {
  return (
    <View>
      <Text>Bienvenidos a React Native</Text>
    </View>
  );
}

export default function Index() {
  return (
    <View>
      <Mensaje />
      <Mensaje />
      <Mensaje />
    </View>
  );
}
```

- En este código tenemos un componente llamado `Index` que funciona como pantalla o screen de nuestra app.
- Este componente `Index` es exportado por default y el router de `expo-router` lo renderiza como primer pantalla.
- Cuando React Native llama a renderizar este componente `Index` devuelve unos componentes anidados que tienen una vista o `<View>` y dentro de la vista hay 3 llamados al componente `<Mensaje />`.
- El resultado final va a ser ver 3 veces `Bienvenidos a React Native`.
- Si bien podemos definir más de un componente en un archivo, se recomienda tener un componente por archivo.
- Creamos una nueva carpeta en la raíz del proyecto con el nombre `components`.
- Dentro de la carpeta `components` creamos un nuevo archivo con el nombre `Mensaje.tsx`.
- Copiamos el código de la función `Mensaje` y lo pegamos dentro del archivo `Mensaje.tsx`.
- También vamos a tener que mover el import sino el componente no sabe de donde vienen `<Text> y <View>`.
- Dado que movimos este componente a su propio archivo también debemos exportarlo para luego poder importarlo desde el componente `Index`.

```javascript
//components/Mensaje.tsx
import { Text, View } from "react-native";

export function Mensaje() {
  return (
    <View>
      <Text>Bienvenidos a React Native</Text>
    </View>
  );
}

// app/index.tsx
import { View } from "react-native";
import { Mensaje } from "@/components/Mensaje";

export default function Index() {
  return (
    <View>
      <Mensaje />
      <Mensaje />
      <Mensaje />
    </View>
  );
}
```

- En este caso podemos ver que `<View>` contiene 3 componentes `<Mensaje />`.
- En este caso decimos que `<View>` es el padre de los componentes `<Mensaje />`.
- Cuando retornamos algunos componentes podemos utilizar `()` para mejorar la legibilidad sobre todo cuando utilizamos arrow functions.
- Llamamos a `<Mensaje />` componentes hijos o `children`.
- React entonces va a terminar teniendo lo que se conoce como un árbol de componentes donde hay un componente padre de la App y dentro del mismo hay muchos componentes hijos organizados con algún criterio en forma de componentes.
- React es muy rápido renderizando componentes y eso es lo que lo hace tan popular.
- Se dice que cuando un valor cambia o mejor dicho una propiedad cambia, React re-renderiza lo que necesita para reflejar ese cambio y lo hace de manera muy performante.
- Si se re-renderiza el componente padre se termina re-renderizando los hijos.

### Renderizando componentes

- React utiliza React DOM para renderizar elementos `HTML` en un documento web.
- Los componentes de React se diferencian de los de HTML por ejemplo utilizando Mayúscula para los nombres de componentes y minúscula para los elementos HTML.
- En React Native no utilizamos HTML.
- React Native utiliza otra forma de renderizar componentes utilizando la versión nativa para cada sistema operativo.
- React Native utiliza a React como librería para saber que tiene que renderizar pero luego llama a otro módulo para que lo renderize.
- Al programar de forma nativa (iOS y Android) el componente `view` es un componente básico para crear vistas.
- podemos pensar a las `vistas` como un cuadrado donde podemos utilizar textos o imágenes como contenido.
- Una vista puede tener otras vistas y de esta forma estar anidadas.
- Cuando se ejecuta el código de JavaScript en el sistema operativo (iOS o Android) hay una conversión del componente escrito en react como `<View>` por algo llamado `<ViewGroup>` en Android y `<UIView>` en iOS.
- En Web una `<View>` es un `div` que sería un contenedor genérico.
- En React Native podemos crear un `<Text>` y al correr la app se va a renderizar un `<TextView>` en Android, `<UITextView>` en iOS y `<p>` un párrafo en Web.
- Podemos ver de esta forma que React Native puede crear un componente `<View> o <Text>` que luego se convertira en un componente nativo de Android, iOS o Web.

![React Native to native components](../assets/react-native/react_native_to_native.png)

- React Native permite crear aplicaciones nativas y por eso se siente como una aplicación 100% nativa porque en el fondo lo que los dispositivos ejecutan es código nativo.
- React Native trae algunos componentes que se conocen como `core components` que nos dan los bloques iniciales como para poder crear nuestros propios componentes y así lograr armar una App.
- Algunos de esos componentes son `View, Text, Image, ScrollView, TextInput`.
- Combinando estos componentes ya podemos ir armando otros componentes.
- React y React Native tienen la mejor comunidad y por ende el mejor soporte para crear aplicaciones Web o Mobile.
- Existen un montón de componentes que podemos utilizar con tan solo instalar un módulo de JavaScript con node y hacerlo parte de nuestra app.

![Superheroe](../assets/react-native/componentes_comunidad.png)

- React Native tiene acceso al código nativo para poder comunicar el mundo de JS con el mundo nativo por medio de intercambiar mensajes a modo de promesas o `promises`. Esto se conoce como módulos nativos.
  Por medio de los módulos nativos es que React Native termina siendo super poderoso!

![Superheroe](../assets/react-native/superhero.jpg)

### JSX

- JSX? Qué es eso?
- JSX es una forma de escribir JavaScript como si fuera etiquetas como las que tenemos en HTML.
- Podemos utilizar JSX para escribir componente de React y React Native de manera más fácil.
- Para entender como funciona JSX primero vamos a ver como funciona React sin JSX.

```javascript
const element = createElement(type, props, ...children);
```

- React tiene una función llamada `createElement` que acepta 3 parámetros.
  - El primer parámetro es el tipo de componente que queremos construir.
  - El segundo son propiedades que le queremos pasar al componente. Podemos pensar como propiedades que le pasamos a una clase y la función `constructor`. Este valor suele ser un obejeto donde cada propiedad es una propiedad del componente.
  - El tercer parámetro es una colección de componentes hijos.

```javascript
import { createElement } from "react";

// Como crea React sus componentes:
function Mensaje({ name }) {
  return createElement("text", {}, "Bienvenidos a React Native");
}

// Como crear un componente de React con JSX
function Mensaje() {
  return (
    <View>
      <Text>Bienvenidos a React Native</Text>
    </View>
  );
}
```

- Posiblemente este código no funcione al 100% pero es para demostrar como sería llamar un componente usando React con funciones vs utilizar JSC con etiquetas.
- Queda claro que JSX es una forma más limpia y fácil de leer que utilizando `createElement`.
- Esto se ve todavía mejor cuando utilizamos propiedades y tenemos componentes hijos donde serían un montón de componentes que tenemos que pasar como parámetros.
- JSX tiene 2 formas de ser utilizado:
  - Con una etiqueta de apertura y cierre en el mismo tag: `<Mensaje />`.
  - Con una etiqueta de apertura y una etiqueta de cierre: `<Mensaje><Text>Más texto</Text></Mensaje>`.
- Vemos en la estructura `<Mensaje></Mensaje>` que `<Mensaje>` es la etiqueta de apertura y `</Mensaje>` es la etiqueta de cierre. Todo lo que va entre estas dos etiquetas es considerado un componente hijo.
- En el caso de `<Mensaje />` vemos que no tiene componentes hijos entonces podemos abrir y cerrar `/` la etiqueta en una sola.
- Cuándo utilizar cada una? va a depender si el componente acepta o no componentes hijos.
- JSX también nos permite utilizar propiedades.
- Para utilizar propiedades o properties utilizamos la siguiente forma:

  - `propiedad="valor"`: utilizamos el nombre de la propiedad, el igual y luego un valor entre comillas dobles cuando queremos utilizar un valor string.
  - `propiedad={valorNoString}`: utilizamos el nombre de la propiedad, el igual y luego llaves cuando queremos utilizar un valor que no sea un string.
  - `propiedad={{}}`: también podemos querer utilizar un objeto y en ese caso tenemos que poner doble `{{}}`. El primer set es por la propiedad y las segundas son porque esto es un objeto.
  - En los ejemplos anteriores estuvimos utilizando una propiedad sin saberlo: `<View style={{flex: 1}}>`.

```javascript
<View style={{flex: 1}}>
```

- En este ejmplo vemos que View tiene una propiedad que se llama `style` que nos permite establecer el estilo que queremos utilizar con este componente.
- Dado que el estilo se configura con un objeto de JavaScript `{flex: 1}` al utilizarlo para una propiedad queda como `style={{flex: 1}}`.
- Ahora que sabemos de propiedades podemos agreagar una propiedad a nuestro componente `Mensaje`

```javascript
function Mensaje(props) {
  return (
    <View>
      <Text>{props.mensaje}</Text>
    </View>
  );
}

export default function Index() {
  return (
    <View>
      <Mensaje mensaje="Bienvenidos" />
      <Mensaje mensaje="a" />
      <Mensaje mensaje="React Native" />
    </View>
  );
}
```

- En este ejemplo vemos que la función Mensaje (nuestro componente) recibe un parámetro que le pusimos el nombre de `prop`.
- JSX le pasa a cada componente un objeto de JavaScript que tiene dentro las propiedades: valores pasados al componente.
- En este caso `props` tiene una propiedad llamada `mensaje` con el valor que se le pasó a cada `<Mensaje mensaje="">`.
- El primer componente renderiza "Bienvenidos"
- El segundo "a"
- El tercero "React Native"
- Esto nos enseña que utilizando propiedades podemos hacer que los componentes de React Native sean reutilizables y customizables.
- Al ser `props` un objeto también podemos utilizar destructuring:

```javascript
function Mensaje({ mensaje }) {
  return (
    <View>
      <Text>{mensaje}</Text>
    </View>
  );
}

export default function Index() {
  return (
    <View>
      <Mensaje mensaje="Bienvenidos" />
      <Mensaje mensaje="a" />
      <Mensaje mensaje="React Native" />
    </View>
  );
}
```

- En este caso `{mensaje}` es como hacer destructuring sobre el objeto que nos pasan como parámetro.
- `<Text>{mensaje}</Text>` En el caso de las etiquetas podemos utiizar `{}` para decirle a React que en ese lugar vamos a utilizar código JavaScript.
- En el ejemplo `{mensaje}` significa que vamos a utilizar el valor de la variable mensaje.
- Podemos utilizar también propiedades como un número:

```javascript
function Mensaje({ mensaje, numero = 0 }) {
  return (
    <View>
      <Text>{mensaje + numero}</Text>
    </View>
  );
}

export default function Index() {
  return (
    <View>
      <Mensaje mensaje="Bienvenidos" numero={10} />
      <Mensaje mensaje="a" />
      <Mensaje mensaje="React Native" />
    </View>
  );
}
```

- En este ejemplo establecemos que `Mensaje` ahora acepta una propiedad con el nombre número.
- Al igual que con las funciones podemos establecer un valor por defecto para un parámetro que en este caso es una propiedad.
- `<Mensaje mensaje="Bienvenidos" numero={10} />` pasa el número 10 como propiedad.
- Los otros dos componentes no están pasando la propiedad numero por lo cual el componente utiliza el valor por defecto.
- También podemos pasar un valor Boolean como `true or false`.

```javascript
function Mensaje({ mensaje, numero = 0, mostrarNumero = false }) {
  return (
    <View>
      <Text>{mensaje}</Text>
      <Text>{numero}</Text>
      <Text>{mostrarNumero}</Text>
    </View>
  );
}

export default function Index() {
  return (
    <View>
      <Mensaje mensaje="Bienvenidos" numero={10} />
      <Mensaje mensaje="a" mostrarNumero />
      <Mensaje mensaje="React Native" mostrarNumero={false} />
    </View>
  );
}
```

- En este ejemplo vemos como al no pasar la propiedad `mostrarNumero` se utiliza el valor por defecto.
- Para los propiedades boolean podemos utilizar el nombre de la propiedad sólo y eso le pasa `true` al componente.
- También podemos pasar un valor `false o true` entre `{true}` or `{false}`.
