# Gauss-Jordan — cuaderno de procedimiento

Calculadora web que resuelve sistemas de ecuaciones lineales con el método de
**Gauss-Jordan** y muestra el procedimiento completo, paso a paso, con
aritmética exacta (fracciones).

**Autoras:** Mariana Quiñones Muñoz y Manuela Tamayo Aristizábal
**Universidad Autónoma de Occidente (UAO)**

---

## Cómo ejecutarla

Toda la página está en un solo archivo: `gauss-jordan.html`. No necesita
instalar nada ni conexión a internet.

1. Descargue el archivo `gauss-jordan.html`.
2. Ábralo con doble clic. Se abre en el navegador (Chrome, Edge o Firefox).

> El visor de adjuntos de Gmail muestra solo el texto del código y no ejecuta
> la página. Por eso hay que descargar el archivo primero.

Para ver el código, abra el mismo archivo con un editor como Visual Studio Code
(clic derecho → Abrir con), o presione `Ctrl + U` con la página abierta en el
navegador.

## Qué hace

- Resuelve sistemas de hasta 8 ecuaciones con hasta 8 incógnitas.
- El sistema se escribe como en el cuaderno (`4 x + 3 y + 2 z = 1`). Solo se
  indica el número de **ecuaciones** y de **incógnitas**; la casilla del término
  independiente se agrega sola.
- Acepta enteros, decimales (`0.75` o `0,75`) y fracciones (`3/4`).
- Muestra cada paso con la matriz aumentada, el pivote resaltado y la operación
  de filas realizada. Se puede avanzar paso a paso o ver todos los pasos juntos.
- Clasifica el sistema:
  - **Solución única**
  - **Infinitas soluciones** (indica las variables libres y la solución general)
  - **Sin solución** (sistema inconsistente)
- Para sistemas 2×2 dibuja la gráfica de las dos rectas (se cortan, coinciden o
  son paralelas), con una ventana de zoom.
- Tiene tema claro y oscuro y funciona en celular.

## Método: cada pivote se procesa completo

Antes de pasar a la siguiente columna, cada pivote se procesa por completo:

1. **Se ubica el pivote.** Si alguna fila tiene 1 o −1 en esa columna, se
   prefiere esa fila, porque así no hay que dividir. Si la posición del pivote
   tiene un 0, se intercambian filas.
2. **Se normaliza** el pivote a 1.
3. **Se hacen ceros debajo** del pivote.
4. **Se hacen ceros arriba** del pivote.

Al terminar, la matriz queda en su forma escalonada reducida (RREF) y la
solución se lee directamente.

### Notación de las operaciones de fila

| Operación                         | Ejemplo            |
|-----------------------------------|--------------------|
| Intercambio de filas              | `F1 ⇔ F2`          |
| Multiplicar una fila (normalizar) | `(1/4)F1 → F1`     |
| Sumar un múltiplo de otra fila    | `−3F1 + F2 → F2`   |

## Estructura del código

Todo está dentro de `gauss-jordan.html`, en este orden:

- **`<style>`**: colores (tema claro y oscuro), diseño de la página, entrada del
  sistema, gráfica y ajustes para celular.
- **HTML**: encabezado, panel de entrada (ecuaciones, incógnitas, cuadrícula,
  botones y ejemplos), panel de pasos y solución, y la ventana de zoom de la
  gráfica.
- **`<script>`**, dividido en secciones numeradas:
  1. **Fracciones**: la clase `F` hace aritmética exacta (suma, resta,
     multiplicación y división de fracciones) y `parseF` convierte lo que se
     escribe en las casillas en fracciones.
  2. **Algoritmo de Gauss-Jordan**: `gaussJordan` aplica el método pivote por
     pivote y guarda cada paso. `coef`, `opSwap`, `opScale` y `opCombo` escriben
     las operaciones de fila.
  3. **Clasificación de la solución**: `classify` decide si hay solución única,
     infinitas soluciones o ninguna. `exprFor` escribe cada variable en términos
     de las variables libres.
  4. **Interfaz**: `buildGrid` crea las casillas del sistema (se puede mover
     entre ellas con las flechas del teclado), y `matrixHTML`, `stepHTML` y
     `render` muestran los pasos.
  5. **Gráfica 2×2**: `drawGraph` dibuja las rectas en SVG y explica si el
     sistema es consistente o no.

  Al final están los ejemplos (`EXAMPLES`), los eventos de los botones, el zoom
  de la gráfica y el arranque, que carga y resuelve el primer ejemplo.

## Licencia

Código abierto bajo la licencia MIT. Vea el archivo `LICENSE`.
