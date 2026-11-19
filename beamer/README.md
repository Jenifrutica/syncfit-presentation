# Pitch en Beamer (estilo de marca)

Versión en LaTeX Beamer del pitch de 15 minutos. Mismo guion y tiempos que
`public/SyncFit-Pitch.html`, con la marca de la app: cielo rosa, tinta índigo,
nubes, goteo, Pulsi, Fredoka (títulos) y Nunito (texto). Los colores salen de
`syncfit-frontend/app/tokens.css`.

- PDF listo: [`syncfit-pitch.pdf`](./syncfit-pitch.pdf)
- Fuente: `syncfit-pitch.tex` + tema `beamerthemesyncfit.sty`
- Fuentes tipográficas en `fonts/` (licencia OFL, ver `fonts/OFL.txt`)

## Compilar

```bash
cd beamer
xelatex syncfit-pitch.tex
xelatex syncfit-pitch.tex
```

Se compila dos veces para que el contador "n de 6" quede bien. Las diapositivas
2 y 5 se revelan por pasos (una tarjeta por clic).

Notas del orador: descomenta `\setbeameroption{show notes on second screen=right}`
en `syncfit-pitch.tex`.
