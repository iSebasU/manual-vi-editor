# 02 · Navegación

[⬅️ Volver al índice](../README.md) · [⬅️ Anterior](01-modos-y-creacion.md)

Todo lo de esta sección se hace en **modo comando**. Si algo empieza a escribirse en pantalla, estás en modo inserción: `Esc` y vuelve a intentar.

## Movimiento carácter por carácter

| Tecla | Qué hace | Equivalente |
|-------|----------|-------------|
| `h` | Un carácter a la izquierda | ← |
| `j` | Una línea abajo | ↓ |
| `k` | Una línea arriba | ↑ |
| `l` | Un carácter a la derecha | → |

Sí, las flechas funcionan. Pero `hjkl` está justo debajo de la mano derecha, y ahí está la ventaja: no sueltas la posición de escritura.

> 🧠 Truco para no confundirlas: `j` tiene la colita hacia abajo (baja), `k` apunta hacia arriba, y `h` y `l` son literalmente la tecla más a la izquierda y la más a la derecha del grupo.

## Movimiento por palabras

| Tecla | Qué hace |
|-------|----------|
| `w` | Al **inicio de la siguiente** palabra (*word*) |
| `e` | Al **final** de la palabra actual (*end*) |
| `b` | Al **inicio de la palabra anterior** (*back*) |

## Movimiento por líneas y por archivo

| Tecla | Qué hace |
|-------|----------|
| `0` (cero) | Inicio de la línea actual (como la tecla Inicio) |
| `$` | Fin de la línea actual (como la tecla Fin) |
| `1G` | Primera línea del archivo |
| `3G` | Línea 3 — en general `nG` salta a la línea *n* |
| `G` (`Shift+G`) | Última línea del archivo |

## El multiplicador: el número antes del comando

Esto es lo que hace que `vi` se sienta rápido. Casi cualquier movimiento acepta un número adelante, y significa "hazlo n veces":

- `8l` → ocho caracteres a la derecha
- `3j` → tres líneas abajo
- `4w` → cuatro palabras adelante
- `2k` → dos líneas arriba

## Ejemplo real: llegar a una palabra específica

En el archivo de práctica, para dejar el cursor exactamente en la `v` de `very` (segunda línea):

```
G      ← me manda a la última línea
k      ← subo una línea: quedo en la línea 2
8l     ← avanzo 8 caracteres (el número ocho, luego la letra L minúscula)
```

Resultado:

```
Welcome to the vi editor.
It is a very powerful text editor.
        ^ el cursor queda aquí
Especially for those who master it.
```

## ⚠️ El error que más me costó: `g` no es `G`

Hice exactamente esa secuencia y terminé parado en la palabra `vi` de la **primera** línea, no en `very` de la segunda. Me demoré un rato entendiendo por qué.

El problema era que estaba presionando **`g` minúscula**. En `vi` las mayúsculas y minúsculas son comandos completamente distintos: `G` (o sea `Shift+G`) salta a la última línea, pero `g` sola no hace eso — se queda esperando una segunda tecla. Al presionar `k` después, lo que ejecuté fue `gk`, que sube una línea. Por eso nunca bajé al final del archivo.

Esto aplica a casi todo el editor: `x` y `X` borran en direcciones opuestas, `p` y `P` pegan en lados distintos, `o` y `O` abren la línea abajo o arriba. La tecla `Shift` cambia el comando, no lo "refuerza".

## La forma menos frágil de llegar a una palabra

Contar caracteres funciona, pero depende de que el cursor haya arrancado donde uno cree. Si te equivocas por una línea, aterrizas en otra palabra — que es justo lo que me pasó. Por eso terminé usando esto:

```
/very
```

Escribes eso, Enter, y el cursor cae **exacto** en la `v` de `very`, sin importar dónde estabas. Es más rápido y no se equivoca.

## Lo que me pasó / lo que aprendí

Al principio contaba caracteres uno por uno con `l`, y encima me equivocaba de línea por usar `g` en vez de `G`. Cuando empecé a usar `w` para saltar palabras y `/palabra` para buscar directo, dejé de contar y dejé de perderme. La lección es que en `vi` casi siempre hay una forma más corta que la que uno está usando.

## Ejercicio de esta sección

Sin usar las flechas: ve a la última línea, súbete a la primera con `1G`, baja dos líneas, ponte al final de esa línea con `$` y vuelve al inicio con `0`.

---

**Siguiente:** [03 · Edición y deshacer ➡️](03-edicion-y-deshacer.md)
