# 📝 Manual de supervivencia del editor vi.

> Mi propia guía del editor `vi`, escrita mientras lo aprendía a los golpes: qué me costó, en qué me equivoqué y los comandos que terminé usando de verdad.

![editor](https://img.shields.io/badge/editor-vi-brightgreen)
![OS](https://img.shields.io/badge/OS-Linux-blue)
![Estado](https://img.shields.io/badge/estado-en%20progreso-yellow)
![Curso](https://img.shields.io/badge/curso-Seminario%20Linux-orange)

---

## 📑 Tabla de contenido

| # | Sección | De qué trata |
|---|---------|--------------|
| 01 | [Modos y creación de archivos](docs/01-modos-y-creacion.md) | Modo comando vs. modo inserción y cómo crear un archivo |
| 02 | [Navegación](docs/02-navegacion.md) | Moverse por el texto sin usar el mouse |
| 03 | [Edición y deshacer](docs/03-edicion-y-deshacer.md) | Borrar palabras, caracteres, líneas y deshacer errores |
| 04 | [Copiar y pegar](docs/04-copiar-y-pegar.md) | Copiar (`yw`), pegar (`p`, `P`) y unir líneas |
| 05 | [Buscar y reemplazar](docs/05-buscar-y-reemplazar.md) | Búsqueda con `/` y sustitución con `:%s` |
| 06 | [Insertar texto](docs/06-insertar-texto.md) | `i`, `a`, `o`, `O` y cuándo usar cada uno |
| 07 | [Guardar y salir](docs/07-guardar-y-salir.md) | `:w`, `:wq`, `:x`, `ZZ`, `:q!` y cómo escapar de vi |
| 🏋️ | [Archivo de práctica](ejercicios/mi-archivo-practica.txt) | El archivo con el que hice todos los ejercicios |

---

## 🤔 ¿Qué es vi?

Soy estudiante de Ingeniería de Sistemas y llevo años usando editores con menús, botones y `Ctrl+Z`. La primera vez que abrí `vi` sentí que me habían quitado todo eso de golpe: una pantalla morada, una columna de virgulillas y nada que indicara qué hacer. Escribí algo y no pasó nada. Pensé que la máquina virtual se había trabado.

No estaba trabada. `vi` funciona con **modos**, y esa es toda la idea que hay que entender antes de aprenderse un solo comando. Cuando lo abres estás en *modo comando*: ahí las letras no escriben, dan órdenes. La `d` borra, la `u` deshace, la `x` elimina un carácter. Para escribir texto de verdad tienes que pasarte al *modo inserción* con `i`, y para volver presionas `Esc`. Suena simple escrito así, pero es justo donde todo el mundo se estrella al principio, yo incluido.

¿Y para qué aprenderlo, si existe `nano` o cualquier editor gráfico? Porque `vi` está en todos lados. Cuando te conectas por SSH a un servidor, cuando el sistema arranca en modo recuperación o cuando trabajas en una máquina sin entorno gráfico, puede que `nano` ni siquiera esté instalado — pero `vi` sí. Es una de esas herramientas que uno no usa todos los días, pero el día que la necesita no hay plan B. Después de pelearme con él un rato entendí que lo que al principio parece incomodidad es en realidad velocidad: borrar una palabra son dos teclas, no buscarla con el mouse y arrastrar.

---

## ⚡ Cheat sheet: los comandos que más usé

> Todos los ejemplos salieron de mi propia práctica sobre el archivo [`ejercicios/mi-archivo-practica.txt`](ejercicios/mi-archivo-practica.txt).

| Comando | Qué hace | Mi ejemplo |
|---------|----------|------------|
| `vi archivo` | Abre el archivo si existe, y lo crea si no | Con `vi myfile` creé mi archivo de práctica desde cero |
| `i` | Entra a modo inserción antes del cursor | Lo primero que tuve que presionar para poder escribir algo |
| `Esc` | Vuelve a modo comando | Mi tecla de pánico: la presiono siempre antes de cualquier comando |
| `h j k l` | Izquierda, abajo, arriba, derecha | Usé `8l` para avanzar 8 caracteres hasta la palabra `very` |
| `w` / `e` / `b` | Siguiente palabra / fin de palabra / palabra anterior | Con `4w` llegué a `powerful` sin contar un solo carácter |
| `0` / `$` | Inicio / fin de la línea actual | Con `$` me fui al final de la línea 1 para arreglar un espacio sobrante |
| `1G` / `G` | Primera / última línea del archivo | ⚠️ Es `G` mayúscula. Con `g` minúscula no funciona (me costó descubrirlo) |
| `x` / `X` | Borra el carácter bajo el cursor / a la izquierda | Con `x` borré el espacio que había dejado antes del punto final |
| `5X` | Borra 5 caracteres hacia la izquierda | Parado en `very`, me borró `is a ` y quedó `It very powerful text editor.` |
| `dw` | Borra una palabra desde el cursor | `dw` sobre `very` dejó la línea en `It is a powerful text editor.` |
| `2dw` | Borra dos palabras | Me borró `very powerful` con un solo comando |
| `14x` | Borra 14 caracteres seguidos | Mismo resultado que `2dw`, pero contando caracteres en vez de palabras |
| `dd` / `2dd` | Borra la línea completa / dos líneas | Con `2dd` el archivo me quedó en una sola línea |
| `D` | Borra desde el cursor hasta el fin de la línea | Después de `4w`, la línea 2 quedó en `It is a very` |
| `u` | Deshace la última operación | Mi comando más usado, sin exagerar |
| `4u` | Deshace las últimas 4 operaciones | Necesario después de `xxxx`, porque fueron 4 operaciones distintas |
| `yw` | Copia («jala») una palabra | Copié `powerful` y la pantalla no cambió, creí que había fallado |
| `p` / `P` | Pega después / antes del cursor | Con `P` me quedó `powerful powerful` en la misma línea |
| `J` / `3J` | Une la línea actual con la siguiente / une 3 líneas | `3J` convirtió las tres líneas del archivo en un solo párrafo |
| `~` | Cambia mayúscula ↔ minúscula | Había escrito `welcome` en minúscula; con `~` lo dejé en `Welcome` |
| `/palabra` | Busca hacia adelante | `/very` me dejó exacto en la palabra, sin contar caracteres |
| `:%s/viejo/nuevo/g` | Reemplaza en todo el archivo | `:%s/text //g` borró la palabra `text` junto con su espacio |
| `:w` | Guarda sin salir | Lo uso cada tanto por miedo a perder lo que llevo |
| `:wq` / `:x` / `ZZ` | Guarda y sale | `:wq` es el que se me quedó grabado |
| `:q!` | Sale sin guardar | Mi salida de emergencia cuando dejé el archivo hecho un desastre |
| `yy` | Copia la línea completa | Copié la primera línea y la pegué al final con `p` |

---

## 🏋️ Cómo practicar tú mismo

Si quieres repetir exactamente lo que hice yo, necesitas una máquina con Linux (yo usé Ubuntu en VirtualBox):

1. Clona este repositorio:
   ```bash
   git clone https://github.com/iSebasU/manual-vi-editor.git
   cd manual-vi-editor
   ```
2. Crea el archivo de práctica sin tener que escribirlo a mano:
   ```bash
   cp ejercicios/mi-archivo-practica.txt myfile
   vi myfile
   ```
3. Sigue las secciones de [`docs/`](docs/) en orden, de la 01 a la 07. Cada una termina con un ejercicio corto.

> 🆘 **Si te pierdes o el editor deja de responderte:** presiona `Esc`, escribe `:q!` y Enter. Sales sin guardar y puedes volver a empezar con `vi myfile`. Esta fue la primera cosa que aprendí y la que más veces usé.

Dos consejos que me habría gustado que alguien me diera antes de empezar:

- **No copies y pegues comandos dentro de vi.** Tecléalos. Si pegas, el editor los toma como texto y te llena el archivo de basura (me pasó, y quedó documentado en los Issues).
- **Las mayúsculas importan.** `g` y `G` no son el mismo comando, ni `x` y `X`, ni `p` y `P`.

---

## 🙌 Créditos

 **Seminario Linux**.
- **Docente:** Bayron Jesit Ospina Cifuentes — bayron.ospinaci@amigo.edu.co
- **Institución:** Universidad Católica Luis Amigó (FUNLAM), Medellín.
- **Autor:** Sebastian Jaramillo Benitez — [@iSebasU](https://github.com/iSebasU)

Todo el contenido de `docs/` está redactado con mis propias palabras y los ejemplos salieron de mi propia sesión de práctica en la máquina virtual, errores incluidos.
