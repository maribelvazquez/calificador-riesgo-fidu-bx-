# Metodología del calificador

## Alcance

Instrumento de **grado de riesgo de cliente** (fideicomiso y sus integrantes), distinto e independiente de la MEBR/EBR de la entidad. Escala **100–500** y bandas de la Tabla 5 de la Matriz de Riesgo BX+ (modelo de clientes): 100–223 BAJO · 224–258 MEDIO · 259–290 MEDIO ALTO · 291–500 ALTO.

## Nivel 1 — Riesgo por integrante

Puntaje = Σ(nivel de la variable × peso). Pesos (suman 100):

| Factor | Peso |
|---|---|
| Tipo de persona | 15 |
| Actividad económica | 23 |
| País de nacimiento | 9 |
| Nacionalidad (proxy por país de nacimiento) | 11 |
| País del domicilio | 11 |
| Estado del domicilio | 12 |
| Edad / constitución | 7 |
| Rol en el fideicomiso | 12 |

## Nivel 2 — Riesgo estructural del vehículo

| Factor | Peso |
|---|---|
| Tipología | 18 |
| Patrimonio en especie | 12 |
| Valor del patrimonio | 12 |
| Antigüedad | 8 |
| Número de partes (automático) | 10 |
| Actividad Vulnerable LFPIORPI | 15 |
| Procedencia de recursos | 10 |
| USD / transfronterizo | 8 |
| Desviación del fin (V2) | 7 |

## Nivel 3 — Consolidación

1. **Ponderación por grupo de rol**: se promedia el riesgo dentro de cada rol y después se pondera el rol (fideicomitente 40 %, fideicomisario 25 %, comité técnico 20 %, apoderado/tercero 15 %, normalizados entre los roles presentes). Con esto un grupo numeroso de bajo riesgo no diluye a un grupo pequeño de alto riesgo (p. ej. 100 fideicomisarios vs. 20 fideicomitentes).
2. **Consolidado** = MAX(estructural del vehículo, ponderado de integrantes).
3. **Peor parte**: si algún integrante alcanza ALTO (≥291), el consolidado no puede ser menor que esa peor parte.
4. **Invalidaciones** (cascada, antes de leer la banda):
   - **Tipo B — PROHIBITIVO**: alguna parte en listas de sanciones (OFAC/ONU/GAFI negra).
   - **Tipo A — mínimo ALTO**: PEP, o Beneficiario Controlador no identificado hasta persona física (>25 %).

El fiduciario (la institución) no se califica: es el sujeto regulado, no un cliente.

## Trazabilidad de datos

Cada factor lleva etiqueta según el recorrido en sistema (checklist ago-2026): **V1** dato en sistema · **V1\*** extracción/proxy · **V2** sin dato aún (actividad económica = prioridad 1) · **AUTO** calculado.
