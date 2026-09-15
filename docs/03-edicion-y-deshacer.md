# 03 · Edición y deshacer

[⬅️ Volver al índice](../README.md) · [⬅️ Anterior](02-navegacion.md)

Esta es la sección donde `vi` empieza a compensar el esfuerzo: borrar en modo comando es muchísimo más corto que seleccionar con el mouse.

## Borrar caracteres

| Comando | Qué hace |
|---------|----------|
| `x` | Borra el carácter **bajo** el cursor |
| `5x` | Borra 5 caracteres hacia la derecha |
| `X` (`Shift+x`) | Borra el carácter **a la izquierda** del cursor (como Backspace) |
| `5X` | Borra los 5 caracteres a la izquierda |

`xxxx` (cuatro veces la x) hace lo mismo que `4x`, pero cuenta como **cuatro operaciones distintas** para el deshacer. Eso importa más adelante.

## Borrar palabras

| Comando | Qué hace |
|---------|----------|
| `dw` | Borra desde el cursor hasta el inicio de la siguiente palabra (*delete word*) |
| `2dw` | Borra dos palabras |

Detalle que confunde: `dw` no borra "la palabra donde estoy" completa, sino **desde donde está el cursor hacia adelante**. Si el cursor está en la `e` de `very`, `dw` deja la `v` y borra `ery `.

## Borrar líneas

| Comando | Qué hace |
|---------|----------|
| `dd` | Borra la línea completa |
| `2dd` | Borra dos líneas: la actual y la siguiente |
| `D` (`Shift+d`) | Borra desde el cursor hasta el **final de la línea** |
| `d$` | Exactamente lo mismo que `D` (porque `$` significa "fin de línea") |

Lo que borras con `dd` no se pierde: queda en el portapapeles interno de `vi` y se puede pegar con `p`. Eso convierte `dd` + `p` en la forma más fácil de **mover** una línea de sitio.

## Deshacer

| Comando | Qué hace |
|---------|----------|
| `u` | Deshace la última operación |
| `4u` | Deshace las últimas 4 operaciones |

Aquí se entiende por qué importaba lo de `xxxx` vs `4x`:

- Borraste con `4x` → **un** `u` lo devuelve todo.
- Borraste con `xxxx` → necesitas `4u`, porque fueron cuatro operaciones.

## Cambiar mayúsculas y unir líneas

| Comando | Qué hace |
|---------|----------|
| `~` | Invierte la mayúscula/minúscula del carácter bajo el cursor y avanza |
| `J` (`Shift+j`) | Une la línea actual con la siguiente en una sola |
| `3J` | Une tres líneas en una |

## Secuencia de práctica (la que más me sirvió)

Sobre la línea `It is a very powerful text editor.`:

```
dw     → It is a powerful text editor.
u      → vuelve todo
2dw    → It is a text editor.
u      → vuelve todo
14x    → It is a text editor.        (borra " very powerful" de un golpe)
u      → vuelve todo
4w D   → It is a very                (D borra desde el cursor hasta el final)
u      → vuelve todo
```

## 🧪 El experimento que me aclaró todo: `xxxx` vs `4x`

Borré cuatro caracteres presionando `x` cuatro veces seguidas y luego presioné `u` esperando recuperarlos. Solo me devolvió **una letra**. Tuve que presionar `u` tres veces más.

La explicación es que `vi` no cuenta letras borradas, cuenta **operaciones**. `xxxx` son cuatro operaciones distintas, así que hacen falta cuatro `u` (o un `4u`). En cambio `4x` es una sola operación, y con un solo `u` vuelve todo.

Es un detalle chiquito pero cambia la forma de trabajar: si vas a borrar varias cosas, es mejor hacerlo con un comando grande que con muchos pequeños, porque después deshacer es mucho más fácil.

## Otra cosa que no esperaba: `X` borra al revés

`x` borra el carácter donde está el cursor, hacia adelante. `X` borra **hacia atrás**, como el Backspace. Estando parado en `very`, yo esperaba que `5X` me borrara la palabra, y lo que hizo fue borrar los cinco caracteres anteriores (`is a `), dejando `It very powerful text editor.`

Otra vez lo mismo: la mayúscula no es "el mismo comando pero más fuerte", es el comando en la dirección contraria.

## Lo que me pasó / lo que aprendí

Me costó entender la diferencia entre `x`, `dw`, `dd` y `D`, porque los cuatro borran. Lo que me ordenó la cabeza fue pensar en **el tamaño de lo que se lleva cada uno**: `x` un carácter, `dw` una palabra, `dd` la línea entera y `D` lo que queda de la línea desde donde estoy parado. Y por encima de todo eso está `u`, que es el que más usé de lejos: sabiendo que puedo deshacer, dejé de tenerle miedo a probar comandos.

## Ejercicio de esta sección

Borra la segunda línea con `dd`, pégala al final con `p`, y luego devuelve todo a como estaba con `2u`.

---

**Siguiente:** [04 · Copiar y pegar ➡️](04-copiar-y-pegar.md)
