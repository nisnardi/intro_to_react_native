# React Native

## Tic Tact Toe

### Cómo funciona calculateWinner

- `calculateWinner` es una función utilizada en un juego de Tic Tac Toe para determinar si hay un ganador.

```javascript
function calculateWinner(squares)
```

- Primero declaramos el nombre de la función `calculateWinner`.
- Esta función acepta un sólo parámetro con el nombre de `squares` que es un array que representa al tablero del juego.
- Cada elemento del array va a tener un valor 'X', 'O' o null.

```javascript
const lines = [
  [0, 1, 2], // Fila superior.
  [3, 4, 5], // Fila del medio.
  [6, 7, 8], // Fila de abajo.
  [0, 3, 6], // Columna izquierda.
  [1, 4, 7], // Columna del medio.
  [2, 5, 8], // Columna derecha.
  [0, 4, 8], // Diagonal superior izquierda a inferior derecha.
  [2, 4, 6], // Diagonal superior derecha a inferior izquierda.
];
```

- En esta sección definimos las posibles lineas y combinaciones ganadoreas.
- Cada array interno contiene tres índices que forman una línea ganadora.
- Los índices corresponden a posiciones en el array de cuadrados.

```javascript
for (let i = 0; i < lines.length; i++) {
  const [a, b, c] = lines[i];
  if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
    return squares[a];
  }
}
```

- Por medio de esta secciónd el código podemos chequear si hay un ganador.
- Con un bucle `for` recorre cada una de las posibles combinaciones ganadoras.
- Para cada combinación:
  - Usa destructuring de los tres índices en variables con nombres a, b, y c.
  - Luego comprueba si:
    - El primer cuadrado (squares[a]) no es nulo o está vacío.
    - El primer cuadrado es igual al segundo cuadrado (squares[a] === squares[b]).
    - El primer cuadrado es igual al tercer cuadrado (squares[a] === squares[c])
  - Si se cumplen todas las condiciones, devuelve el jugador ganador ('X' u 'O').
- Si no se encuentra ninguna combinación ganadora devuelve null.
- Esto indica que el juego sigue en curso o es un empate.

#### Ejemplos

- Si squares = ['X', 'X', 'X', null, null, null, null, null], la función retorna 'X' porque la fila superior está llena de X's.
- Si squares = ['O', null, null, 'O', null, null, 'O', null, null], la función retorna 'O' porque la columna de la izquierda está llena de O's
- Si squares = ['X', 'O', 'X', 'O', 'X', 'O', 'O', 'X', 'O'], la función retorna null porque no hay ninguna combinación ganadora.

#### Test?

- Esta función es una buena oportunidad para escribir un test.
- Tenemos los valores de entrada y salida esperados.
- Te animas?

```javascript
import { calculateWinner } from "../index";

describe("calculateWinner", () => {
  test("gana X", () => {
    const squares = ["X", "X", "X", null, null, null, null, null];
    const resultado = calculateWinner(squares);

    expect(resultado).toBe("X");
  });

  test("gana O", () => {
    const squares = ["O", null, null, "O", null, null, "O", null, null];
    const resultado = calculateWinner(squares);

    expect(resultado).toBe("O");
  });

  test("Empate o no hay ganador", () => {
    const squares = ["X", "O", "X", "O", "X", "O", "O", "X", "O"];
    const resultado = calculateWinner(squares);

    expect(resultado).toBe(null);
  });
});
```
