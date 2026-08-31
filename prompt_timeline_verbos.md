# Rol y objetivo
Eres desarrollador front-end + diseñador pedagógico. Construye una **única "slide"** (una sola
página que entra en pantalla, **sin scroll**) en **Vue 3** (Composition API, `<script setup>`) con
**D3.js** para toda la visualización, **sin backend**, que enseñe los **tiempos verbales del pasado
en español** a estudiantes de nivel B1. El motor de aprendizaje es una **LÍNEA DE TIEMPO de nodos y
conexiones** basada en el **ASPECTO**: si la acción empezó, terminó, seguía en curso, es anterior a
otra, o es irreal/deseada. Es una herramienta **para el alumno**: aprende **manipulando**. Prioridad:
**fácil de usar, poco saturada y bien diseñada** (márgenes generosos, jerarquía clara).

# Alcance (tiempos a incluir)
Sistema del pasado sobre **dos planos**:
- **Indicativo (plano REAL):** presente (ancla del "ahora"), pretérito indefinido, imperfecto,
  pretérito perfecto compuesto, pluscuamperfecto.
- **Subjuntivo (plano MENTAL):** presente, pretérito perfecto, imperfecto, pluscuamperfecto.
Arquitectura **dirigida por datos** para añadir después futuro/condicional sin tocar la lógica.

# Idea pedagógica central (respétala en todo el diseño)
El español elige el tiempo por el **ASPECTO**, no por "cuánto hace". Reutiliza dos modelos mentales:
- **Dos mundos:** indicativo = **mundo real** (lo que es/fue) en el eje; subjuntivo = **mundo mental**
  (deseo, duda, hipótesis, lo irreal) flotando encima, colgado de una **matriz** que lo dispara.
- **Formas por aspecto en la línea:**
  - Pretérito indefinido = **PUNTO cerrado ●** = terminado. *Ayer terminé el proyecto.*
  - Imperfecto = **LÍNEA ondulada ~~~** = en curso / costumbre / fondo. *Terminaba cuando llamaste.*
  - Pretérito perfecto = punto **pegado a AHORA**, conectado al presente = pasado que toca el presente.
  - Pluscuamperfecto = punto **anterior a otro punto** del pasado = "el pasado del pasado".
  - Subjuntivos = **nubes** en el plano mental (presente/pasado/irreal).
- **Joyas visibles:** (1) la línea (imperfecto) que el punto (pretérito) **interrumpe**;
  (2) el pluscuamperfecto **antes** de un punto pasado; (3) la misma escena saltando al plano mental.
Primero el uso (la forma en la línea), después la forma (la conjugación).

# La frase ancla (dispositivo central, impleméntalo)
Usa **una sola oración modelo** cuyo significado es constante y cuyo **verbo objetivo** se conjuga
por todo el sistema. Tiene dos ranuras variables:
- **contexto temporal** que fija el aspecto (ayer / antes / hoy·ya / cuando llamaste / antes de que…),
- **matriz/gancho** que licencia el modo y enciende el plano mental (espero que / me pidió que /
  ojalá / si…).
Núcleo por defecto (todo reemplazable por datos): sujeto **yo**, verbo **terminar**, complemento
**el proyecto**. La app **transforma la misma frase** en cada tiempo y la muestra al expandir el nodo:
- Pretérito: *Ayer terminé el proyecto.* · Imperfecto: *Terminaba el proyecto cuando sonó el teléfono.*
- Perfecto: *Ya he terminado el proyecto.* · Pluscuam.: *Cuando llamaste, ya había terminado el proyecto.*
- Subj. pres.: *Espero que termine…* · perf.: *Espero que haya terminado…*
- Subj. imperf.: *Me pidió que terminara…* / *Ojalá terminara…*
- Subj. pluscuam.: *Ojalá hubiera terminado…* / *Si hubiera terminado…, habría descansado.*
El **verbo objetivo es seleccionable** por el alumno (regulares e irregulares frecuentes).

# La metáfora visual (dibujada con D3.js — NODOS y CONEXIONES)
- **Eje horizontal** (D3 scale/axis) con marca central **AHORA**; izquierda = PASADO; derecha =
  futuro (reservado). **Márgenes amplios**; nada pegado a los bordes.
- **Dos planos** separados por un divisor sutil rotulado **"MUNDO REAL"** (abajo, sobre el eje) y
  **"EN MI MENTE"** (arriba). Los subjuntivos van arriba; los indicativos, en el eje.
- **Nodos** por forma-aspecto: punto lleno (pretérito), línea ondulada/discontinua (imperfecto),
  punto pegado a AHORA (perfecto), punto anterior (pluscuam.), nube redondeada (subjuntivos).
- **Conexiones/enlaces:** "interrupción" (imperfecto→pretérito), "anterioridad" (pluscuam.→pretérito),
  "matriz" (verbo que dispara → nube de subjuntivo). Trázalas con curvas D3.
- **Anti-saturación (clave):** cada nodo muestra solo lo esencial (etiqueta del tiempo + forma).
  **Conjugación completa + frase transformada + "por qué" se revelan al pulsar/hover**, con el nodo
  **expandiéndose** (transición D3). **Un solo nodo abierto a la vez.** Los no activos, atenuados.
- **Leyenda** compacta y siempre visible: forma → aspecto → tiempo.

# Interacción del alumno
1. **Explorar (por defecto):** elige **verbo objetivo** y **sujeto**; pulsa un **tiempo** (o su nodo):
   la app coloca/resalta el nodo, **transforma la frase ancla** a ese tiempo, y al **expandir** muestra
   la **conjugación completa** (6 personas), la **frase de ejemplo** y el **"por qué"** en una línea.
2. **Decidir (quiz):** frase con hueco + fichas de forma (punto/línea/nube…); el alumno arrastra la
   correcta al nodo; feedback inmediato con la regla; marcador de aciertos.
3. **Contraste:** una escena con dos verbos (fondo + interrupción) donde asigna aspecto a cada uno y
   ve la animación línea + punto (y su salto al plano mental si activa una matriz).

# Contenido lingüístico (todo como DATOS estructurados, no incrustado en la vista)
Modela cada verbo con lo mínimo para DERIVAR el resto por reglas (ver motor abajo). Incluye:

**Regulares (raíz + terminaciones):**
- Pretérito -AR/-ER/-IR: hablé/-aste/-ó/-amos/-asteis/-aron · comí/-iste/-ió/-imos/-isteis/-ieron ·
  viví/-iste/-ió/-imos/-isteis/-ieron
- Imperfecto -AR: -aba/-abas/-aba/-ábamos/-abais/-aban · -ER/-IR: -ía/-ías/-ía/-íamos/-íais/-ían
- Participio: -ar→-ado, -er/-ir→-ido

**Irregulares de pretérito más frecuentes (por familia, como override):**
- ser/ir: fui, fuiste, fue, fuimos, fuisteis, fueron
- familia "u": estar (estuv-), tener (tuv-), poder (pud-), poner (pus-), saber (sup-), haber (hub-)
  → -e/-iste/-o/-imos/-isteis/-ieron
- familia "i": hacer (hic-/hizo), querer (quis-), venir (vin-)
- familia "j": decir (dij-), traer (traj-), conducir (conduj-) → ellos **-eron** (dijeron, trajeron)
- dar (di, diste, dio, dimos, disteis, dieron), ver (vi, viste, vio, vimos, visteis, vieron)

**Imperfecto: solo 3 irregulares** (dato pedagógico): ir (iba…), ser (era…), ver (veía…).

**Participios irregulares frecuentes:** hecho, dicho, visto, escrito, puesto, vuelto, roto, abierto,
muerto, cubierto, resuelto.

**Marcadores de contexto** (cada uno con su aspecto y explicación de una línea): pretérito → *ayer,
anoche, el lunes, de repente, una vez, en 1990*; imperfecto → *antes, siempre, todos los días,
mientras, de niño, cada verano*; perfecto → *hoy, ya, esta semana, últimamente, nunca (aún)*;
pluscuam. → *cuando llegué ya…, antes de eso, hasta entonces*; subjuntivo → matrices *espero que,
me pidió que, ojalá, si…*.

# ESPECIFICACIÓN TÉCNICA DE CONSTRUCCIÓN (para que la edifiques así)
## Modelo de datos
- `VERBOS: []` — `{ infinitivo, grupo:'ar'|'er'|'ir', sujetoDefault, complementoDefault,
  irregulares:{ preterito?:[6], imperfecto?:[6], participio?:string } }`. Si no hay override,
  se conjuga por regla.
- `TIEMPOS: []` — cada uno: `{ id, nombre, modo:'indicativo'|'subjuntivo', plano:'real'|'mental',
  compuesto:bool, auxTiempo?:idDelTiempoDeHaber, forma:'punto'|'linea'|'punto-ahora'|'punto-anterior'|'nube',
  posicion:número|'ahora', disparadores:[{texto,aspectoNota}], nota }`. Añadir un tiempo = añadir
  una entrada aquí (más, si hace falta, un override en algún verbo). **Nada de lógica hardcodeada por tiempo.**
## Motor de conjugación — `conjugar(verbo, tiempoId, persona) -> string`
- **Simples** por regla: aplica terminaciones del grupo; si hay `irregulares[tiempo]`, úsalo.
- **Compuestos**: `conjugar('haber', auxTiempo, persona) + ' ' + participio(verbo)`.
  Tablas de `haber`: perfecto (he/has/ha/hemos/habéis/han), pluscuam. (había…), perf. subj. (haya…),
  pluscuam. subj. (hubiera/hubiese…).
- **Derivaciones que DEBES implementar (menos datos, más pedagogía):**
  - **Imperfecto de subjuntivo** = raíz de **pretérito ellos** (quita `-ron`) + `-ra/-ras/-ra/
    -´ramos/-rais/-ran` (variante `-se`). Ej.: hablar→hablaron→**hablara**; tener→tuvieron→**tuviera**;
    ser/ir→fueron→**fuera**; decir→dijeron→**dijera**. (Muestra este vínculo en la UI.)
  - **Presente de subjuntivo** = raíz de la **1ª pers. presente** + **vocal contraria** (hable, coma,
    viva). Reutiliza el modelo "vocal contraria / usted = subjuntivo" de la guía.
- Devuelve además metadatos para resaltar la parte irregular/derivada en la UI.
## Motor de la frase ancla — `transformarFrase(nucleo, tiempoId, contexto) -> string`
- `nucleo = { sujeto, verbo, complemento }`. Compón: `[matriz?] + sujeto/gancho + conjugar(...) +
  complemento + [contexto temporal]`, eligiendo la matriz/contexto por defecto de ese `TIEMPOS[id]`.
## Componentes (Vue) y render (D3)
- `App`: estado (`verboActivo`, `sujeto`, `tiempoActivo`, `nodoExpandido`, `modo`).
- `Controles`: selectores de verbo/sujeto y conmutador de modo (explorar/quiz/contraste).
- `Linea` (contenedor del `<svg>`): **Vue pasa datos reactivos → D3 posee el SVG** (selección,
  escalas, ejes, transiciones). Evita que Vue y D3 peleen por el mismo DOM del SVG.
- `viz/timeline.d3.js`: `render(svgEl, {nodos, enlaces, planos}, callbacks)`; `xScale` sobre las
  `posicion`; dos bandas `y` (real/mental); dibuja nodos por `forma`, enlaces por curva; expandir =
  transición de radio + panel de detalle (Vue o `foreignObject`); redibuja en `resize`.
- `NodoDetalle`: tabla de conjugación (6 personas, resaltando irregular/derivado) + frase transformada
  + "por qué".
- `Leyenda`.
## Estado/flujo
Máquina simple por `modo`. En 'explorar', elegir un `tiempo` → `transformarFrase` + resaltar nodo;
expandir → detalle. Un nodo abierto a la vez; el resto atenuado (anti-saturación).

# Diseño visual (coherente con la guía existente)
- Acento `#2c3e8a`; tipografía `'Segoe UI', Arial, sans-serif`; lienzo central con `border-radius` y
  sombra sutil; *callouts* aviso (`#fff8dd`/`#e0b400`) y modelo mental (`#eef3ff`/acento). Acierto
  `#1a7a3a`, error `#b3261e`.
- **Formato slide:** todo en **una pantalla sin scroll**; **márgenes generosos** y aire entre
  elementos; jerarquía clara (título breve → línea protagonista → controles compactos → leyenda).
- **Responsivo:** el SVG de D3 se reescala al contenedor (`viewBox` + `preserveAspectRatio`, redibujo
  en `resize`); nodos se expanden/colapsan según el espacio. `@media max-width:680px`: controles
  apilados, nodos táctiles.
- **UI en español**, limpia, sin saturación.

# Requisitos técnicos
- **Un único archivo `.html` autónomo** con **Vue 3** y **D3.js v7** vía CDN (`<script type="module">`
  con `createApp`). Sin build ni más dependencias. Abre con doble clic en cualquier navegador. (Si
  prefieres Vite, conserva la misma separación datos/lógica/vista y el formato de una sola slide.)
- Sin red en tiempo de ejecución, sin backend, sin almacenamiento externo.
- Código comentado en español donde la lógica pedagógica lo requiera.

# Entregable
Devuelve el archivo completo y funcional, más un párrafo de "cómo usarlo en clase" y una nota de
"cómo añadir el siguiente tiempo" (agregar una entrada a `TIEMPOS`, y si acaso un override de verbo).
