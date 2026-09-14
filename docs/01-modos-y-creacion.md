# 01 · Modos y creación de archivos

[⬅️ Volver al índice](../README.md)

## La idea que hay que entender antes que cualquier comando

`vi` no funciona como el Bloc de notas. En un editor normal abres el archivo y escribes. En `vi` lo primero que tienes que saber es **en qué modo estás**, porque la misma tecla hace cosas distintas según el modo.

| Modo | Qué pasa si presionas `d` | Cómo entrar | Cómo salir |
|------|---------------------------|-------------|------------|
| **Comando** (el modo por defecto) | Interpreta la `d` como una orden de borrado | `Esc` | Presionando `i`, `a`, `o`, `O`… |
| **Inserción** | Escribe la letra `d` en el archivo | `i`, `a`, `o`, `O`, `I`, `A` | `Esc` |

Cuando abres un archivo, `vi` te deja en **modo comando**. Es decir: al principio no puedes escribir. Eso es normal, no está dañado.

> 🧭 Regla de oro: **si no sabes dónde estás, presiona `Esc`.** Te deja en modo comando siempre, incluso si ya estabas ahí.

## Crear un archivo nuevo

```bash
vi myfile
```

Si `myfile` no existe, `vi` abre un archivo vacío con ese nombre (y solo se crea en el disco cuando lo guardas). Si ya existe, lo abre para editarlo.

Lo que ves al abrir un archivo vacío es una columna de virgulillas `~`. Esas líneas **no** son parte del archivo: son la forma que tiene `vi` de decirte "aquí ya no hay contenido".

```
~
~
~
"myfile" [New File]
```

## Primer archivo, de principio a fin

1. `vi myfile` → se abre el editor en modo comando.
2. Presiona `i` → entras a modo inserción (en las versiones modernas verás `-- INSERT --` abajo).
3. Escribe el texto:
   ```
   Welcome to the vi editor.
   It is a very powerful text editor.
   Especially for those who master it.
   ```
4. Presiona `Esc` → vuelves a modo comando.
5. Escribe `:wq` y Enter → guarda (*write*) y sale (*quit*).

Si ahora vuelves a abrirlo con `vi myfile`, en la esquina inferior izquierda aparece un resumen del archivo:

```
"myfile" 3 lines, 97 characters
```

Ese renglón es útil para confirmar que el archivo se guardó y cuánto pesa realmente.

## Lo que me pasó / lo que aprendí

Me pasaron dos cosas en esta parte y las dos fueron por no entender los modos.

La primera: abrí `vi` con un nombre de archivo y apareció texto que yo no había escrito. Pensé que el editor traía algo por defecto. No: el archivo **ya existía** de una prueba anterior, y `vi archivo` lo abre si existe en vez de crear uno nuevo. Ahora antes de abrir algo hago `ls` para ver qué hay en la carpeta.

La segunda fue más grave. Estaba en modo inserción y **pegué** un texto que tenía copiado. Todo ese texto entró al archivo como contenido, y me borró lo que llevaba. Aprendí dos cosas de ahí: que en modo inserción todo lo que llega al teclado se vuelve texto, y que dentro de `vi` uno **no pega, uno teclea**.

## Ejercicio de esta sección

Crea un archivo llamado `practica.txt`, escribe tres líneas cualquiera, guarda y sal con `:wq`. Vuelve a abrirlo y verifica que el contador de abajo diga 3 líneas.

---

**Siguiente:** [02 · Navegación ➡️](02-navegacion.md)
