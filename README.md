# Simulador del Teorema del Límite Central (TLC)

> Aplicación web educativa interactiva desarrollada con **Claude (Anthropic)** para un curso de Estadística de posgrado de una Escuela de Negocios. Todo el código, los textos y los gráficos se construyeron en una sesión de trabajo con Claude.

**App en vivo:** https://sjchiona.github.io/tlc-simulador/

---

Aplicación web educativa sobre el **Teorema del Límite Central** para uso autónomo de los estudiantes. Funciona en computadora y en celular, y puede alojarse en la web o en un aula virtual (LMS).

## 1. Entregable

Un único archivo **HTML autocontenido** (HTML + CSS + JavaScript), en español, que:

- Abre en Google Chrome y funciona como archivo estático (sin servidor).
- Se ve bien tanto en **pantalla de computadora** como en **celular**.
- Existe en dos versiones equivalentes:
  - `index.html`: con las librerías incrustadas (sin dependencias externas), usada en GitHub Pages.
  - `TLC_Simulador.html`: con las librerías por CDN.

Librerías: **Chart.js** (gráficos) y **KaTeX** (fórmulas).

## 2. Navegación: tres secciones

Orden de pestañas: **¿Qué es el TLC?** · **Simulador interactivo** · **Fórmulas principales**.
La pestaña de aterrizaje es "¿Qué es el TLC?"; el simulador se ejecuta al abrir su pestaña.

### 2.1. ¿Qué es el TLC?
Intuición y enunciado en lenguaje claro: qué afirma el teorema, por qué es notable, qué significa "n suficientemente grande", y qué **no** dice (habla de la distribución de la media muestral, no de la forma de los datos individuales).

### 2.2. Simulador interactivo
El alumno configura todo por controles, sin tocar código:

- **Población de origen** (selector, con su descripción justo debajo).
- **Tamaño de muestra `n`**: 1 a 200 (slider + input; default 2).
- **N.º de simulaciones `B`**: 10 a 50 000 (slider + input; default 1000).
- **Semilla aleatoria**: editable (default 123) para reproducir resultados.

En cada simulación se extrae una muestra **con reemplazo**, se calcula su media, y al final se grafica la distribución de todas las medias.

**Poblaciones disponibles:**

- **Bases de datos reales (corte transversal, observaciones independientes):**
  - *Old Faithful — tiempo de espera* (272): bimodal.
  - *Sismos de Fiji — magnitud* (1000): asimétrica a la derecha.
  - *Boston — criminalidad* (506): asimetría extrema a la derecha.
  - *Boston — valor de viviendas* (506): asimetría moderada.
  - *Diamantes — precio* (muestra de 2000): muy sesgada a la derecha.
- **Distribuciones sintéticas (parámetros editables):** Uniforme, Exponencial, Log-normal, Chi-cuadrado y Bernoulli.
- **CSV propio:** una columna numérica; se autodetectan separador y símbolo decimal, y se ignoran las celdas vacías o no numéricas.

**Salidas:**

- Histograma de la **población original** vs. histograma de las **medias muestrales**, lado a lado, con la **normal teórica N(μ, σ/√n)** y la densidad empírica superpuestas.
- El **eje horizontal de ambos gráficos muestra las unidades** de la base elegida (p. ej. "Minutos de espera" y "Media de minutos de espera").
- Para las distribuciones **teóricas**, una nota indica que el histograma proviene de una **muestra simulada** de N valores (no aparece en las bases reales).
- Para **Bernoulli y variables discretas**, la población se dibuja como **dos barras** con la probabilidad de cada valor (0 y 1), sin curva suavizada.
- **Panel de estadísticos:** μ y σ poblacionales; media y desviación de las medias simuladas; tabla **"Desviación de las medias muestrales" vs. σ/√n** con su cociente y un veredicto de coincidencia de la fórmula.
- **Normalidad de las medias** evaluada con asimetría y curtosis (lo que de verdad mejora al aumentar `n`), con su veredicto.
- **Gráfico cuantil–cuantil (Q–Q)** de las medias.
- Cómputo por lotes con barra de progreso para `B` grande.

### 2.3. Fórmulas principales
Notación formal en KaTeX: enunciado, μ_X̄ = μ, σ_X̄ = σ/√n, convergencia en distribución y condiciones de aplicación.

## 3. Restricciones

- Compatible con Chrome; autocontenido (un solo archivo); todo en español, tratamiento formal.
- Responsivo: usable en celular y en escritorio.

## 4. Alojamiento

- **GitHub Pages:** https://sjchiona.github.io/tlc-simulador/ (se ejecuta como web normal).
- **Aula virtual / LMS:** subir `index.html` como archivo y abrirlo en pestaña nueva, o enlazarlo como **URL externa** apuntando a GitHub Pages.
  - Nota: la *vista previa* de archivos de algunos LMS no ejecuta JavaScript; por eso conviene abrirlo en pestaña nueva o usar la URL externa.

## 5. Decisiones de diseño relevantes

- Se descartó una base **longitudinal** (datos de las mismas unidades a lo largo del tiempo) porque el TLC exige **independencia** de las observaciones; se usaron bases de **corte transversal**.
- El cociente "desviación de las medias / (σ/√n)" verifica la **fórmula del error estándar** (válida para cualquier `n`) y **no** la normalidad; la normalidad se juzga con el Q–Q y con la asimetría/curtosis de las medias.
- Muestreo **con reemplazo** y semilla reproducible, replicando un script de R original sobre la base `faithful`.

---

*Desarrollado con Claude (Anthropic).*
