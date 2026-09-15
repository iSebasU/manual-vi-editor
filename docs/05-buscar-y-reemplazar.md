# 05 · Buscar y reemplazar

[⬅️ Volver al índice](../README.md) · [⬅️ Anterior](04-copiar-y-pegar.md)

## Buscar

| Comando | Qué hace |
|---------|----------|
| `/palabra` + Enter | Busca hacia **adelante** desde el cursor |
| `?palabra` + Enter | Busca hacia **atrás** |
| `n` | Siguiente coincidencia (en la misma dirección) |
| `N` | Coincidencia anterior |

Buscar es la forma más honesta de navegar: en vez de contar caracteres con `8l`, escribes `/very` y el cursor aterriza ahí.

## Reemplazar: la estructura del comando `:s`

Este es el comando que se ve más raro y en realidad tiene solo cuatro piezas:

```
:%s/patron/reemplazo/g
 │ │    │        │     │
 │ │    │        │     └── g = global: todas las veces en cada línea (sin g, solo la primera de cada línea)
 │ │    │        └──────── con qué lo reemplazo (vacío = borrar)
 │ │    └───────────────── qué busco
 │ └────────────────────── s = substitute (sustituir)
 └──────────────────────── % = en TODO el archivo (sin %, solo en la línea actual)
```

| Variante | Alcance |
|----------|---------|
| `:s/viejo/nuevo/` | Primera coincidencia de la línea actual |
| `:s/viejo/nuevo/g` | Todas las coincidencias de la línea actual |
| `:%s/viejo/nuevo/g` | Todas las coincidencias del archivo completo |
| `:%s/viejo/nuevo/gc` | Igual, pero pidiendo **confirmación** en cada una (`c` = confirm) |
| `:%s/viejo//g` | Borra `viejo` en todo el archivo (reemplazo vacío) |

> 💡 `:%s/viejo/nuevo/gc` es el que recomiendo usar cuando el archivo es importante: te pregunta una por una y respondes `y` o `n`.

## El detalle del espacio

Este ejemplo del laboratorio:

```
:%s/text //g
```

Fíjate que hay un **espacio después de `text`**, antes de la barra. Eso es intencional: si escribes `:%s/text//g` borras la palabra pero queda un espacio doble (`It is a very powerful  editor.`). Incluyendo el espacio en el patrón, el resultado queda limpio:

```
It is a very powerful editor.
```

No hay espacios "decorativos" en este comando: cada carácter entre las barras se busca literalmente, incluidos los espacios.

## Ejemplo real

```
/powerful     ← busco la palabra sin contar caracteres
:%s/text //g  ← elimino la palabra "text" y su espacio en todo el archivo
u             ← deshago el reemplazo
```

## Lo que me pasó / lo que aprendí

Este comando es el que más feo se ve de todos los que aprendí. `:%s/text //g` parece una clave de wifi. Me confundían el `%` y la `g` porque los veía como adorno, hasta que entendí que cada símbolo responde una pregunta distinta: el `%` dice **dónde** buscar (todo el archivo o solo esta línea) y la `g` dice **cuántas veces** reemplazar en cada línea. Con eso dejó de parecerme un jeroglífico.

Lo del espacio me tomó por sorpresa. Uno asume que los espacios en un comando son para que se lea bonito, y aquí no: el espacio después de `text` es parte de lo que se está buscando. Si lo quitas, la palabra desaparece pero queda un hueco doble en la frase.

También me sirvió mucho descubrir que buscar con `/` es la forma más cómoda de moverse. Antes de esto yo contaba caracteres con `8l` y me equivocaba de línea; con `/very` llego exacto y sin pensar.

## Ejercicio de esta sección

Busca una palabra con `/`, reemplázala en todo el archivo usando `:%s/.../.../gc` respondiendo `y` a la primera y `n` al resto, y observa la diferencia.

---

**Siguiente:** [06 · Insertar texto ➡️](06-insertar-texto.md)
