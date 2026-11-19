# Pitch en Beamer (estilo de marca)

Presentación **corta** de SyncFit Edge: 8 diapositivas con la idea (el problema,
qué cambia hoy y las dos IAs), cómo se construyó el backend y las estructuras de
datos que usa, y un cierre de agradecimiento. La app se muestra en vivo, sin diapositivas.
Usa la marca de la app: cielo rosa, tinta índigo, nubes, goteo, Pulsi, Fredoka
(títulos) y Nunito (texto). Los colores salen de `syncfit-frontend/app/tokens.css`.

- **Guion por persona:** [`GUION.md`](./GUION.md) (Juan López abre; Jenifer Urbano y
  Juan Cuarán siguen). Cada nota del `.tex` empieza con quién presenta.
- PDF listo: [`syncfit-pitch.pdf`](./syncfit-pitch.pdf)
- Fuente: `syncfit-pitch.tex` + tema `beamerthemesyncfit.sty`
- Fuentes tipográficas en `fonts/` (licencia OFL, ver `fonts/OFL.txt`)

## Presentarla (Adobe Acrobat)

Ábrela en **Adobe Acrobat o Acrobat Reader** y entra en pantalla completa
(Ver → Modo Pantalla completa, o Ctrl/Cmd + L). Acrobat reproduce:

- **Transiciones** al cambiar de diapositiva (disolver, barrido, persianas,
  cortina, empuje, destello) y un fundido corto en cada revelado.
- **Pulsi flota en la portada** sin parar desde que se abre el PDF.
- **Animaciones de una sola vez** (paquete `animate`), que esperan medio
  segundo a que termine la transición antes de arrancar: Pulsi aparece en el cierre, las nubes llegan a su sitio, el goteo sube al entrar a
  la diapositiva lavanda y al cierre, Pulsi recorre las cuatro paradas de las
  dos IAs, avanza un tramo por clic en el catálogo, y la onda de pulso se
  dibuja al revelar el último paso. Ninguna se repite: al revelar el
  siguiente elemento, la animación ya terminada se queda quieta.

Si Acrobat pregunta, permite el JavaScript del documento: las animaciones lo
necesitan. En Vista Previa de macOS o en el navegador se ve un cuadro fijo
de cada animación (el diseño sigue completo, pero sin movimiento).

Avanza con las flechas o la barra espaciadora: cada diapositiva muestra todo su
contenido de una vez (8 diapositivas, 8 páginas).

## Antes de exponer

- Acrobat con el JavaScript del documento permitido (sin él no hay animaciones).
- Pantalla completa (Ctrl/Cmd + L) desde la portada, para que Pulsi ya esté flotando.
- Para la demo en vivo (después de la diapositiva 7), tres sesiones abiertas en el navegador:
  administrador del gimnasio de prueba, atleta con el código del gimnasio y
  superadministrador en Catálogos.
- Si la demo es en local: backend y frontend corriendo, y el acceso de prueba
  visible en `/entrar`.

## Compilar

```bash
cd beamer
xelatex syncfit-pitch.tex
xelatex syncfit-pitch.tex
```

Se compila dos veces para que el contador "n de 11" quede bien. Necesita el
paquete `animate` de LaTeX.

Notas del orador: descomenta `\setbeameroption{show notes on second screen=right}`
en `syncfit-pitch.tex`.
