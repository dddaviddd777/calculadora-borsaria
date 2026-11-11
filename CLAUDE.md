# Màquina del Temps Borsària

Calculadora d'inversió (`index.html`), amb una pàgina educativa complementària (`apren.html`): mostra què hauria passat si haguessis invertit en un índex o una acció en el passat, i projecta què podria passar cap al futur. Tota la interfície i els textos són en **català**.

## Estructura

- `index.html` — la calculadora: HTML, CSS i JS en un sol fitxer. Sense build ni dependències locals; s'obre directament al navegador.
- `apren.html` — «Aprèn · Suplement per a l'inversor»: guia educativa en 7 capítols plegables (fonaments, fons i ETFs, tipus d'ordres, apalancament i venda en curt, risc i estratègia, impostos a Espanya, glossari). Cada concepte té un `id` per enllaçar-hi des del glossari. Copia les variables de color de `index.html`; si en canvies una, canvia-la a tots dos fitxers.
- Els botons «Prova-ho a la calculadora» obren `index.html` amb paràmetres a l'adreça, que llegeix `readParams()`: `sel` (ids d'`ASSETS` separats per comes), `dca`, `initial`, `monthly`, `start` (any o `now`), `end`, i `div`/`fx`/`inf`/`net`/`log` (`1` o `0`).
- Publicat a GitHub Pages des de la branca `main`: https://dddaviddd777.github.io/calculadora-borsaria/
- Únic recurs extern: Chart.js 4.4.1 des de jsDelivr, i les fonts de Google Fonts (Old Standard TT, Libre Caslon Text, IBM Plex Mono).

## Dades

Les dades són **anuals i incrustades** al JS (no hi ha cap API):

- `ASSETS` — per a cada actiu: rendibilitats anuals en % (`d`, començant a l'any `from`), moneda (`cur`), si són de rendibilitat total amb dividends (`kind:'tr'`) o només preu (`'price'`), i un dividend mitjà aproximat (`div`).
- `FX` — EUR/USD a final d'any. `CPI` — IPC d'Espanya per any des del 2000.
- "Avui" és inici de novembre de 2026 (`TM`); el 2026 compta 10 mesos. En afegir dades d'un any nou cal actualitzar `TM`, l'excepció de mesos a `yearRet`, `FX`, `CPI`, el text del segell de capçalera i les opcions "Avui (nov. 2026)".

## Càlcul

Les rendibilitats anuals es reparteixen mes a mes. Opcions: aportació única o + mensual, dividends reinvertits, efecte del canvi EUR/USD, euros d'avui (inflació), net d'IRPF de l'estalvi (trams 2026) i escala logarítmica. La projecció usa la rendibilitat mitjana dels últims N anys (o una de manual), amb escenaris pessimista/optimista a ± un marge.

## Estil

Estètica de **diari antic**: paleta sèpia/paper, tipografies serif clàssiques, filets dobles a la capçalera, majúscules espaiades als rètols. Tots els colors són variables CSS a `:root`, amb mode fosc via `prefers-color-scheme` i `data-theme`. Mantingues aquest estil en qualsevol canvi, i la maquetació ha de funcionar en mòbil.
