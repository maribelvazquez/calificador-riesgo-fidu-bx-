# Roadmap

## V1 (actual)
Single-file, datos locales por navegador, registro con reabrir/actualizar, CSV, cédula PDF, reglas de tratamiento deterministas.

## Fase 2 — candidatos
- **Firebase (Firestore + Auth): IMPLEMENTADO en v1.5** (bimodal). Pendiente solo: pegar el firebaseConfig, crear usuarios y reglas (ver README).
- **Recomendaciones con IA:** solo vía backend (Netlify Function que guarde la API key del lado servidor). Nunca poner la key en el frontend: aun con contraseña, viaja al navegador y es extraíble. Las reglas deterministas se mantienen como base auditable; la IA redactaría el plan de monitoreo a partir de ellas.
- **Catálogos completos:** cargar los catálogos reales del banco (actividad económica 1,378 claves, países 259, estados ZPLD) con buscador, en lugar del catálogo simplificado.
- **Monto individual por evento patrimonial:** incorporar el factor V1 pendiente cuando se defina la extracción del reporte mensual.
- **Histórico de calificaciones:** guardar cada recalificación con fecha para ver la evolución (hoy solo se guarda la última con su fecha).

## Deuda conocida
- Catálogo simplificado (operable a mano) vs. claves del sistema: mapear cuando llegue la integración.
- `actividad económica` de las partes: campo existe en sistema, no poblado (prioridad 1 del plan V2 del modelo).
