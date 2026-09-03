# Changelog

## v1.5.1 — 2026-09-02
- Firebase activado: firebaseConfig del proyecto `calificador-fiduciario` integrado en index.html (login por correo/contraseña del equipo, registro compartido en Firestore).
- Aviso inferior coherente con el modo: en nube sin sesión ya no muestra el texto del modo local; indica iniciar sesión para usar el registro compartido.
- data/base_variables_bx.csv: agregados los CATÁLOGOS OPERATIVOS V1 (serie 9100) de integrantes, homologados con la Matriz Excel v2.1.

## v1.5 — 2026-08-27
- Modo nube (Firebase Auth + Firestore), bimodal: con firebaseConfig pegado, el registro es compartido para todo el equipo, con login por usuario, sincronización en vivo, historial de recalificaciones por fideicomiso y botón para migrar lo guardado en modo local. Sin config (o donde Firebase no carga), sigue el modo local por navegador.

## v1.4 — 2026-08-27 (retro de la sesión de validación con BX+)
- Política interna: entidad auxiliar del crédito (SOFOM/SOFIPO/SOFOL/arrendadora/aseguradora) → ALTO por default; bancos no la activan. Nueva regla TR-22 y opciones nuevas en el catálogo de actividad.
- Campo nuevo «Actividad del fideicomiso» (informativo/reglas; TR-23 giro de riesgo del vehículo). Columna opcional ActividadFideicomiso en layout v1.1 e importación.
- Corrección (bug de la demo): PEP/Listas/BC ahora se reflejan en el riesgo del propio integrante (mín. ALTO / PROHIBITIVO), no solo en el consolidado.
- Tablero y cédula PDF: columna «En alto» por grupo de rol (caso 95 bajos + 5 altos visible).
- Buscador en el registro (ID/nombre/banda) preparando llegar a 100+.
- Guía rápida paso a paso en PDF (docs/) y Excel modelo: pesos editables resaltados y hojas de captura ocultas.

## v1.3 — 2026-08-27
- Cédula PDF (composición por rol, armado de la calificación, recomendaciones, detalle de integrantes).
- Tablero del fideicomiso por grupo de rol y distribución por banda.
- Base de 21 reglas de tratamiento/monitoreo (TR-01 a TR-30) con fundamento; visibles en app y PDF.
- Reabrir y actualizar fideicomisos guardados (con fecha y comparativa antes → ahora).
- Descargas duales: visor de Claude y navegador normal (Netlify).

## v1.2 — 2026-08-27
- Datos privados por navegador (localStorage); la página ya no se guarda a sí misma.
- Etiquetas de trazabilidad por factor (V1 / V1* / V2 / AUTO).
- Plantilla CSV e importación masiva (una fila por integrante, agrupa por ID).

## v1.1 — 2026-08-27
- Rol como variable de riesgo (FIR) además de ponderador (decisión conservadora documentada).
- Ponderación por grupo de rol: evita que un grupo numeroso de bajo riesgo diluya a uno pequeño de alto riesgo.

## v1.0 — 2026-08-27
- Motor 100–500 espejo de la Matriz BX+: integrantes + vehículo + consolidación + invalidaciones A/B.
