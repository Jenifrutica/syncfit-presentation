# Pitch en Beamer (estilo de marca)

Versión en LaTeX Beamer del pitch: **5 minutos de presentación** (diapositivas
1 a 5) y **10 minutos de demo en vivo** (diapositivas 6 a 9). Mismo guion que
`public/SyncFit-Pitch.html`, sin cronómetros en pantalla, más portada, tres diapositivas de contexto (las fases,
las dos IAs y por qué SyncFit) y cierre, con la marca de la app: cielo rosa, tinta índigo,
nubes, goteo, Pulsi, Fredoka (títulos) y Nunito (texto). Los colores salen de
`syncfit-frontend/app/tokens.css`.

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

Avanza con las flechas o la barra espaciadora: las diapositivas 1 a 6 se
revelan por pasos (11 diapositivas, 24 páginas).

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
