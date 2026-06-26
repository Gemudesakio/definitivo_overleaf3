# Documento definitivo (unificado)

Tesis: *Capacidad del canal de acceso aleatorio no ortogonal de redes 5G NB-IoT
soportadas en redes satelitales de órbita baja.*

Este proyecto unifica en un solo documento, con **nomenclatura única Legacy / CRACS-R /
CRACS-T**, el contenido que estaba repartido entre dos versiones (el documento general
"capacidad" y el proyecto de Overleaf con los capítulos nuevos).

## Estructura

| Cap. | Archivo | Origen |
|------|---------|--------|
| 1 | `ch01_introduccion.tex` | documento general |
| 2 | `ch02_marco_teorico.tex` | documento general |
| 3 | `ch04_requerimientos.tex` | overleaf (versión actualizada, CRACS) |
| 4 | `ch06_diseno.tex` | overleaf (versión actualizada, CRACS) |
| 5 | `ch07_metodologia.tex` | overleaf |
| 6 | `ch08_implementacion.tex` | overleaf (capítulo nuevo) |
| 7 | `ch09_resultados.tex` | overleaf (capítulo nuevo) |

`main.tex` los ensambla en ese orden. `preamble.tex` es el preámbulo común.
Los nombres de archivo conservan su numeración original (ch04, ch06…) por trazabilidad;
el número de capítulo final lo asigna LaTeX automáticamente.

## Compilación

Usa biblatex/biber. Secuencia:

```
pdflatex main
biber main
pdflatex main
pdflatex main
```

(En Overleaf: subir esta carpeta y poner el compilador en **pdfLaTeX**; biber es automático.)

## Bibliografía

Dos archivos `.bib` fusionados vía `\addbibresource`:
- `referencias.bib` — claves `ref1`…`ref20` (Introducción y Marco Teórico).
- `tesis.bib` — claves con nombre (capítulos de diseño en adelante).
No hay colisión de claves.

## Decisiones de unificación aplicadas

1. **Nomenclatura.** Todo en CRACS-R / CRACS-T (antes SARA / SCMA-NORA-CD en el doc
   general). SARA se conserva solo como técnica de la literatura (Moon et al.), de la que
   CRACS-R es la adaptación.
2. **Sin redundancia.** Se descartó el capítulo viejo "Diseño del Sistema + Plan de
   Evaluación" del documento general (lo reemplaza la versión actualizada del overleaf).
   En Metodología (cap. 5) se eliminaron las tablas/figura/listas que duplicaban al
   capítulo de Diseño (KPIs, regiones operativas, criterios de aceptación): ahora son
   referencias cruzadas. Eso resolvió además una etiqueta `fig:regiones` duplicada.
3. **KPIs.** La tabla de KPIs del capítulo de Diseño se amplió al conjunto completo
   (SAR, SAR₁, T_access, T_inst, SDP, TST, ECDF, PCR_pre, PCR_msg3, throughput, RTX, CID)
   para que cubra todas las métricas usadas en Resultados.
4. **Coherencia de referencias.** Se corrigieron referencias cruzadas rotas
   (`sec:sara_colisiones` → `sec:cracs_r`), un número de capítulo escrito a mano
   ("Cap. 9" → `\cref{ch:resultados}`) y la frase de Metodología que decía que la
   Implementación estaba "fuera del alcance" (ahora es el cap. 6 de este documento).
5. **Uniformidad menor.** `Msg1…Msg5` → `MSG1…MSG5` en Marco Teórico, para igualar al
   resto del documento.

## Respaldo de datos (zip `resultados`)

No es texto: son los datos crudos de la campaña (4.260 corridas NS-3), los scripts de
post-proceso y las 12 figuras del cap. 7 (ya copiadas en `figures/ch09/`). Incluye
`audit_ch09_data.md`, que verifica los 171 datos numéricos del capítulo de Resultados
contra los CSV crudos: 0 discrepancias.

## Pendiente / sugerencias

- **Conclusiones:** ninguno de los dos zips traía capítulo de conclusiones. Habría que
  añadirlo.
- **Marco Teórico (cap. 5 reservado):** en la numeración original del overleaf el Marco
  Teórico iba como cap. 5. Aquí va como cap. 2 (orden lógico: teoría antes de
  requerimientos). Si tu plantilla institucional exige otro orden, es solo reordenar los
  `\input` de `main.tex`.
- **Redacción:** los capítulos de Implementación y Resultados son densos (estadística:
  bootstrap, Wilcoxon, Tukey). Es contenido legítimo de tesis, pero se puede hacer una
  pasada para suavizar el lenguaje más técnico si se desea.
