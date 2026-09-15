# 04 · Copiar y pegar

[⬅️ Volver al índice](../README.md) · [⬅️ Anterior](03-edicion-y-deshacer.md)

En `vi` copiar se llama *yank* («jalar»), y de ahí viene la letra `y`.

## Copiar

| Comando | Qué hace |
|---------|----------|
| `yw` | Copia una palabra desde el cursor (*yank word*) |
| `yy` | Copia la línea completa |
| `3yy` | Copia tres líneas |
| `y$` | Copia desde el cursor hasta el fin de la línea |

⚠️ **Al copiar no pasa nada visible en la pantalla.** No hay mensaje, no se resalta nada. La primera vez uno cree que el comando no funcionó; en realidad el texto ya está guardado en el buffer y solo lo confirmas cuando lo pegas.

## Pegar

| Comando | Qué hace |
|---------|----------|
| `p` | Pega **después** del cursor (o **debajo** de la línea, si copiaste líneas) |
| `P` (`Shift+p`) | Pega **antes** del cursor (o **encima** de la línea) |

La diferencia entre minúscula y mayúscula es la misma idea que en otros comandos de `vi`: la mayúscula hace lo mismo pero "hacia el otro lado".

## Lo importante: borrar también copia

`x`, `dw`, `dd` y `D` no solo eliminan: dejan lo borrado en el mismo buffer que usa `y`. Por eso funciona esto:

```
dd    ← corta la línea
(me muevo a donde la quiero)
p     ← la pego ahí
```

Eso es "cortar y pegar" en `vi`. No existe un comando separado para cortar porque no se necesita.

## Ejemplo real

Con el cursor en la palabra `powerful` de la segunda línea:

```
yw    ← copio "powerful" (la pantalla no cambia)
P     ← pego antes del cursor
```

Resultado:

```
Welcome to the vi editor.
It is a very powerful powerful text editor.
Especially for those who master it.
```

Y con `u` queda como estaba.

Otro ejemplo, uniendo el tema con la sección anterior:

```
1G    ← primera línea
3J    ← une las tres líneas en una sola
```

```
Welcome to the vi editor.  It is a very powerful text editor. Especially for those who master it.
```

## Lo que me pasó / lo que aprendí

Perdí un rato repitiendo `yw` porque la pantalla no cambiaba y yo pensaba que el comando no estaba funcionando. Venía acostumbrado a que al copiar algo se resalte en azul o salga un aviso, y aquí no pasa absolutamente nada. Solo cuando presioné `P` me di cuenta de que sí había copiado, y de que probablemente lo había copiado varias veces.

La lección es que en `vi` el silencio no significa error: muchas operaciones no muestran nada porque no tienen por qué. Si quieres confirmar que copiaste, la forma de verificarlo es pegando.

Lo otro que me pareció útil de esta sección es que `dd` no solo borra, también guarda. Eso significa que "cortar y pegar" ya existe en `vi` sin ser un comando aparte: borras con `dd`, te mueves, y pegas con `p`.

## Ejercicio de esta sección

Copia la primera línea con `yy`, muévete a la última con `G` y pégala debajo con `p`. Después usa `u` para dejar el archivo como estaba.

---

**Siguiente:** [05 · Buscar y reemplazar ➡️](05-buscar-y-reemplazar.md)
