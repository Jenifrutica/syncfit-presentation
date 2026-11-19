# Pitch en Beamer (estilo de marca)

Versión en LaTeX Beamer del pitch de 15 minutos. Mismo guion y tiempos que
`public/SyncFit-Pitch.html` (más portada y cierre), con la marca de la app: cielo rosa, tinta índigo,
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
- **Animaciones en bucle** (paquete `animate`): Pulsi flotando en la portada
  y el cierre, nubes que cruzan, el goteo que sube al entrar a la diapositiva
  lavanda y al cierre, Pulsi recorriendo los pasos y la onda de pulso de la
  telemetría.

Si Acrobat pregunta, permite el JavaScript del documento: las animaciones lo
necesitan. En Vista Previa de macOS o en el navegador se ve un cuadro fijo
de cada animación (el diseño sigue completo, pero sin movimiento).

Avanza con las flechas o la barra espaciadora: las diapositivas 1 a 6 se
revelan por pasos (8 diapositivas, 19 páginas).

## Compilar

```bash
cd beamer
xelatex syncfit-pitch.tex
xelatex syncfit-pitch.tex
```

Se compila dos veces para que el contador "n de 8" quede bien. Necesita el
paquete `animate` de LaTeX.

Notas del orador: descomenta `\setbeameroption{show notes on second screen=right}`
en `syncfit-pitch.tex`.
