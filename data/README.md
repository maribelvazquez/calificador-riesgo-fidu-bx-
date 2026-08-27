# Base de variables

`base_variables_bx.csv` es la **fuente de verdad del modelo**: las 2,628 variables del modelo de
clientes BX+ (factores F1–F26, con clave, probabilidad y multiplicador tal como viven en el sistema
del banco) más las 45 variables fiduciarias nuevas (series FF/9000 y FIR rol), con su peso % y la
marca de si aplican al modelo fiduciario.

La app (`index.html`) usa un **catálogo simplificado operable** (docs/CATALOGOS.md) para captura
manual; este CSV es el insumo para la fase 2 (catálogos completos con buscador e integración con
el sistema). El archivo Excel maestro (`Matriz_Riesgo_Fideicomisos_LexQuo_v2.xlsx`) vive fuera del
repo por tamaño; este CSV se regenera desde su hoja «3. BASE VARIABLES».
