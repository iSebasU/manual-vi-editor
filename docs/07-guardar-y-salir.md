# 07 · Guardar y salir

[⬅️ Volver al índice](../README.md) · [⬅️ Anterior](06-insertar-texto.md)

Casi todo lo de esta sección empieza con dos puntos `:`. Ese `:` abre la línea de comandos de `vi` en la parte inferior de la pantalla, y funciona **solo en modo comando**. Si escribes `:` y aparece un `:` dentro del texto, estabas en modo inserción: `Esc` y otra vez.

## Guardar

| Comando | Qué hace |
|---------|----------|
| `:w` | Guarda (*write*) y **se queda** en el editor |
| `:w nombre.txt` | Guarda con otro nombre (como "Guardar como") |
| `:w!` | Fuerza el guardado en un archivo de solo lectura, si el sistema lo permite |

Al guardar, abajo a la izquierda aparece la confirmación:

```
"myfile" 3 lines, 102 characters written
```

Esa palabra `written` es la señal de que el archivo sí quedó en el disco.

## Guardar y salir

| Comando | Qué hace |
|---------|----------|
| `:wq` | Guarda y sale |
| `:x` | Guarda y sale (solo escribe si hubo cambios) |
| `ZZ` | Guarda y sale — **sin** dos puntos, es `Shift+z` dos veces |
| `:wq!` | Guarda y sale forzando, en un archivo de solo lectura |

Los tres primeros hacen prácticamente lo mismo. La diferencia fina: `:wq` siempre escribe el archivo (incluso si no cambió nada, lo que actualiza la fecha de modificación), mientras `:x` solo escribe si hubo cambios reales.

## Salir sin guardar

| Comando | Qué hace |
|---------|----------|
| `:q` | Sale — **falla** si hay cambios sin guardar |
| `:q!` | Sale descartando todos los cambios (el `!` significa "sé lo que hago") |
| `:e!` | Descarta los cambios y **recarga** el archivo sin salir del editor |

Si intentas `:q` con cambios pendientes, `vi` te frena con un mensaje tipo `E37: No write since last change`. No está dañado: te está protegiendo. Decide si quieres `:wq` (guardar) o `:q!` (descartar).

## 🆘 La receta para salir de vi cuando estás perdido

Esta es probablemente la información más útil de todo el manual:

```
Esc      ← me aseguro de estar en modo comando
:q!      ← salgo sin guardar nada
Enter
```

Funciona siempre, sin importar en qué modo estabas ni qué tanto dañaste el archivo. Y si lo que quieres es conservar los cambios, el mismo camino pero con `:wq`.

De los tres que guardan y salen, yo me quedé con `:wq`. No porque sea mejor que `:x` o `ZZ`, sino porque es el que se me pegó primero y el que leo más claro: *write* y *quit*, guardar y salir. `ZZ` es más corto pero me da desconfianza no ver lo que estoy escribiendo.

## Lo que me pasó / lo que aprendí

La primera vez que abrí `vi` no supe salir. Probé `Ctrl+C`, probé cerrar con la X, y terminé cerrando la terminal completa. Suena bobo, pero es el chiste más repetido sobre este editor y ahora entiendo por qué: no hay ningún botón ni ningún menú que te diga cómo salir.

También me pasó lo contrario. Después de dejar el archivo lleno de texto pegado por accidente, `:q!` me salvó: salí sin guardar y el archivo quedó intacto, como si nada hubiera pasado. Ese comando es, para mí, el más importante del editor — no porque haga algo útil, sino porque quita el miedo a experimentar. Si sé que puedo salir sin dañar nada, pruebo comandos con tranquilidad.

Tener `Esc` + `:q!` grabado en la cabeza es lo que convierte a `vi` de trampa a herramienta.

## Tabla resumen de salidas

| Quiero… | Comando |
|---------|---------|
| Guardar y seguir trabajando | `:w` |
| Guardar y salir | `:wq` · `:x` · `ZZ` |
| Salir sin guardar | `:q!` |
| Deshacer todo y recargar el archivo | `:e!` |
| Salir y no hay cambios | `:q` |

## Ejercicio de esta sección

Haz un cambio cualquiera, intenta salir con `:q` (va a fallar), lee el mensaje, y luego sal con `:q!`. Vuelve a abrir el archivo y confirma que el cambio no se guardó.

---

[⬅️ Volver al índice](../README.md)
