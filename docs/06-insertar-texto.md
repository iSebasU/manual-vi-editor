# 06 · Insertar texto

[⬅️ Volver al índice](../README.md) · [⬅️ Anterior](05-buscar-y-reemplazar.md)

Hay varias formas de entrar a modo inserción, y la que elijas decide **dónde aparece el cursor**. Esa es toda la diferencia: te ahorra moverte antes de escribir.

| Comando | Dónde te deja escribiendo |
|---------|---------------------------|
| `i` | **Antes** del carácter donde está el cursor (*insert*) |
| `a` | **Después** del carácter donde está el cursor (*append*) |
| `I` | Al **inicio de la línea** actual |
| `A` | Al **final de la línea** actual |
| `o` | En una **línea nueva debajo** de la actual (*open*) |
| `O` | En una **línea nueva encima** de la actual |

De todas ellas se sale igual: `Esc`.

## Cuándo uso cada una

- `i` cuando necesito meter algo en medio de una palabra o antes de ella.
- `a` cuando el cursor cayó justo en el carácter anterior al que quiero (muy común después de moverte con `w` o `e`). Escribir `a` es más rápido que `l` + `i`.
- `A` para agregar al final de una línea sin tener que ir con `$`.
- `o` y `O` para agregar líneas completas: no hay que ir al final y presionar Enter, la línea nueva aparece sola y ya quedas en modo inserción.

## Ejemplo real

**Agregar texto al inicio del archivo (`i`):**

```
1G     ← primera línea
i      ← modo inserción
Hello and     ← escribo esto (con espacio al final)
Esc
```

```
Hello and Welcome to the vi editor.
```

Luego, para pasar esa `W` a minúscula: `l` para avanzar un espacio y `~` para invertirla.

```
Hello and welcome to the vi editor.
```

**Agregar una palabra en medio (`a`):**
Con el cursor en el espacio entre `powerful` y `editor` (por ejemplo con `j` y luego `10l`):

```
a
text            ← escribo la palabra y un espacio
Esc
```

```
It is a very powerful text editor.
```

**Abrir líneas nuevas (`o` y `O`):**

```
o
This line was added by pressing lowercase o.
Esc
```

```
Hello and welcome to the vi editor.
It is a very powerful text editor.
This line was added by pressing lowercase o.
Especially for those who master it.
```

```
O
You just pressed O to open a line above.
Esc
```

```
Hello and welcome to the vi editor.
It is a very powerful text editor.
You just pressed O to open a line above.
This line was added by pressing lowercase o.
Especially for those who master it.
```

## Un arreglo real que hice con esto

Escribiendo mi archivo de práctica cometí dos errores de dedo en la primera línea: puse `welcome` con minúscula y dejé un espacio de más antes del punto, así:

```
welcome to the vi editor .
```

Lo arreglé sin borrar la línea ni reescribirla:

```
1G  0  ~       ← me paro en la primera letra y la cambio a mayúscula
$  h  x        ← me voy al final, retrocedo un carácter y borro el espacio
```

Quedó `Welcome to the vi editor.` Dos arreglos, seis teclas, sin tocar el mouse. Ahí fue donde por fin le encontré la gracia al editor.

## Lo que me pasó / lo que aprendí

Al principio usaba `i` para absolutamente todo y después me movía con las flechas dentro del modo inserción, que es la forma más lenta de hacerlo. Cuando empecé a elegir la letra correcta —`a` cuando el cursor quedó un carácter antes, `A` para irme al final de la línea, `o` para abrir una línea nueva— dejé de dar vueltas. El comando ya te pone donde tienes que escribir; ese es el punto.

Lo otro que aprendí a la mala es que en modo inserción **todo** lo que llegue al teclado se vuelve texto, incluido lo que uno pegue del portapapeles. Por eso la costumbre de presionar `Esc` apenas termino de escribir.

## Ejercicio de esta sección

En la última línea del archivo, usa `A` para agregar tu nombre al final. Después usa `O` para escribir una línea encima que diga por qué estás practicando vi.

---

**Siguiente:** [07 · Guardar y salir ➡️](07-guardar-y-salir.md)
