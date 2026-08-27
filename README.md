# Calificador de Riesgo Fiduciario

Instrumento provisional de **grado de riesgo de cliente** para fideicomisos (proyecto B por Más · Lex Quo), en lo que se libera el sistema definitivo. Califica cada fideicomiso y a cada uno de sus integrantes, consolida el riesgo en escala 100–500 (bandas de la Tabla 5 de la Matriz BX+), aplica invalidaciones (PEP, listas, BC) y emite recomendaciones de tratamiento con fundamento normativo.

> ⚠️ **Repositorio privado.** Contiene la lógica del modelo de riesgo del cliente; no publicar.

## La app es un solo archivo

`index.html` es la aplicación completa: HTML + CSS + JS, sin build, sin dependencias, sin backend. Es deliberado: se despliega arrastrando el archivo y no hay nada que compilar ni actualizar de terceros. Todo el motor (catálogos, pesos, consolidación, reglas, generador de PDF) vive ahí.

## Funciones

- Captura de fideicomiso + integrantes sin límite (alta individual, masiva "n iguales" o importación CSV).
- Cálculo en vivo: riesgo por integrante, estructural del vehículo, ponderado por grupo de rol, peor parte, consolidado y banda.
- Invalidaciones tipo A (PEP, BC no identificado → mínimo ALTO) y tipo B (listas → PROHIBITIVO).
- Tablero por rol, distribución por banda y armado de la calificación.
- **Cédula PDF** con branding Lex Quo (composición por rol, armado, recomendaciones, detalle de integrantes).
- Base de reglas de tratamiento y monitoreo (`docs/REGLAS_TRATAMIENTO.md`).
- Registro local con reabrir/actualizar y exportación CSV.
- Etiquetas de trazabilidad por factor (V1 / V1* / V2 / AUTO) según el recorrido en sistema.

## Privacidad de datos

Los datos capturados viven **solo en el navegador de quien captura** (`localStorage`); la página no los envía a ningún lado. La vía de salida es la exportación CSV / cédula PDF. Quien abre el enlace encuentra la app en blanco.

## Despliegue

**Netlify:** arrastrar `index.html` (o conectar este repo) → Site configuration → activar *Password protection*. `netlify.toml` ya trae encabezados de no-indexación.

**Artifact de Claude:** la app también corre publicada como artifact (mismo archivo).

## Uso masivo

1. Descargar la plantilla desde la app (o `plantillas/plantilla_captura_fideicomisos.csv`).
2. Llenar en Excel: **una fila por integrante**, agrupadas por `ID` de fideicomiso. La plantilla lista los valores válidos de cada columna.
3. Importar el CSV en la app: agrupa por ID, califica todo y alimenta el registro.

## Branding

La interfaz y la cédula PDF usan la paleta BX+ real (carbón #2e383e + verde lima #a4c425 + teal #2fa3a0, tomados del sitio —
ver `assets/README.md` para colocar el logo oficial y afinar colores con el manual de identidad).
Crédito «Desarrollado por Lex Quo» en pie de cabecera.

## ¿Dónde vive la base de variables?

- **Fuente de verdad:** `data/base_variables_bx.csv` (2,673 variables: modelo de clientes BX+ completo + factores fiduciarios serie 9000, con pesos y marca de aplicabilidad).
- **Catálogo operable de la app:** objeto `CAT` dentro de `index.html` (documentado en `docs/CATALOGOS.md`) — versión simplificada para captura manual.
- **Maestro Excel:** `Matriz_Riesgo_Fideicomisos_LexQuo_v2.xlsx` (fuera del repo; hoja «3. BASE VARIABLES»).

## Documentación

| Doc | Contenido |
|---|---|
| `docs/METODOLOGIA.md` | Motor de cálculo: factores, pesos, escala, consolidación por grupo de rol, invalidaciones |
| `docs/CATALOGOS.md` | Catálogos y niveles 1–5 de cada variable |
| `docs/REGLAS_TRATAMIENTO.md` | Base de reglas TR-xx de tratamiento y monitoreo |
| `docs/ROADMAP.md` | Fase 2: Firebase, backend IA, catálogos completos |
| `CHANGELOG.md` | Historial de versiones |

## Contexto metodológico

Este instrumento es **distinto e independiente** de la MEBR/EBR de la entidad (requisito de la Guía CNBV 2019). Deriva de la Matriz de Riesgo de clientes BX+ 2026: reutiliza sus factores y escala, agrega los factores fiduciarios (serie FF/9000) y el rol como variable (FIR), y adapta la consolidación a la estructura multi-parte del fideicomiso.
