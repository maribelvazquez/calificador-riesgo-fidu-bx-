# Changelog

## v1.9 — 2026-09-24 (modelo acordado el 4 y 5 de septiembre + precarga de la base CIFRE)
- Repeso del Bloque A (Matriz v2.4/v2.5): tipo 16 · patrimonio 10 · valor 11 · antigüedad 7 · partes 9 · actividad vulnerable 14 · procedencia 10 · USD 6 · operación distinta al fin 5 · ubicación del patrimonio 12 = 100.
- Nuevo factor FF10 «Ubicación del patrimonio»: se captura el estado por nombre y toma su nivel de la tabla F7 del banco; bien en el extranjero = 4. Si el patrimonio no tiene ubicación física (efectivo, derechos) el factor no aplica y su peso se reparte entre los demás (renormaliza a 100).
- Ruta heredada del Bloque B: casilla «Cliente banco» y puntaje CIFRE por integrante. Puntaje del integrante = MAX(puntaje banco ; nivel banco × 80 + nivel rol × 20), con nivel banco = puntaje ÷ 100. El piso impide que el rol baje el juicio del banco. Las invalidaciones (listas, PEP, BC, auxiliares) siguen aplicando encima.
- Carga masiva: columnas opcionales UbicacionPatrimonio, ClienteBanco, PuntajeBanco y, para precarga, Precarga, CuentasCIFRE, BandaCIFRE, ListasCIFRE, FechaCIFRE. Los registros de precarga muestran el aviso «Precarga CIFRE — pendiente de captura» y toman el puntaje CIFRE sin ajuste por rol.
- Opción «No determinado» en todos los factores del vehículo (y número de partes en precarga) con nivel 2.58 = límite superior de MEDIO (puntaje 258): sin información no se presume riesgo bajo; un fideicomiso sin datos queda en MEDIO documentado (criterio de acotamiento), no en BAJO por omisión ni en ALTO por falta de dato. No dispara TR-20.
- Cobertura de datos: % por fideicomiso en la captura y tablero «Cobertura de datos» en el registro (vehículos completos vs. con faltantes, precarga, datos faltantes más frecuentes por factor, integrantes con actividad no capturada y calificados por puntaje del banco).
- Corrección: la carga masiva en modo nube ahora sí guarda en Firestore (en lotes de 400) y fecha cada registro; antes sólo quedaba en pantalla.
- Botón «Quitar precarga CIFRE (n)»: elimina de un golpe todos los registros de precarga (nube o local) sin tocar los fideicomisos capturados.
- Buscador: escribir el nombre exacto de una banda (ALTO, MEDIO ALTO, MEDIO, BAJO, PROHIBITIVO) filtra sólo esa banda; «precarga» muestra sólo los registros de la base CIFRE.
- Export CSV del registro con columnas de precarga (puntaje y banda CIFRE, campo listas).
- Registros guardados antes de v1.9 se leen con «No aplica» en ubicación: su puntaje estructural cambia por el repeso al reabrirlos y guardarlos.
- Pendiente: captura de países de integrantes por nombre (tabla F4/F5 del banco).

## v1.8 — 2026-09-24 (comentarios de BX+ · lenguaje más básico)
- Catálogos en lenguaje llano, conforme a las observaciones de Héctor Camacho (23-sep) y a la Matriz v2.5:
  - Tipo de fideicomiso: «Testamentario / planeación patrimonial»; «Público / gubernamental» se sustituye por «Recibido por sustitución fiduciaria» (nivel 4; los públicos no son alcance de Fiduciario).
  - Patrimonio: efectivo en numerario / valores bursátiles cotizados en custodia (1) · inmuebles y bienes muebles (3) · mixto (3) · acciones, partes sociales y otros títulos no cotizados (4) · derechos de cobro, fideicomisarios y otros bienes (4).
  - Procedencia: ejemplos en recursos bancarizados y en venta de activos.
  - FF9 se muestra como «Operación distinta al fin del contrato» con opciones en lenguaje llano (mismos niveles; sigue siendo V2).
  - «Efectivo intensivo» pasa a «Alto manejo de efectivo (casas de empeño, gasolineras, restaurantes, menudeo)» en la actividad de integrantes y del fideicomiso. TR-21 intacta.
  - Rol «Tercero / garante» pasa a «Tercero administrador / garante / depositario».
- «Tipología del fideicomiso» se renombra «Tipo de fideicomiso» (acuerdo 4-sep: en PLD/FT «tipología» designa un patrón de lavado).
- Catálogo de rol reanclado a piso 1 (acuerdo 5-sep, ya en la Matriz v2.4): tercero 1 · apoderado 2 · fideicomisario 3 · comité técnico 4 · fideicomitente 4 · doble rol 5.
- Migración automática: los registros guardados con los nombres anteriores (nube, local, respaldo JSON y CSV) se leen y se muestran con los nombres nuevos; no se pierde ningún dato. El puntaje guardado de un registro se actualiza al reabrirlo y guardarlo.
- Descarga de la Matriz del modelo actualizada a v2.5. Layout de carga y plantilla CSV con los catálogos nuevos.
- Pendiente para v1.9 (acordado el 4/5-sep, aún no en la app): repeso del Bloque A con FF10 ubicación del patrimonio, ruta heredada 80/20 del puntaje del banco, captura de países y estados por nombre.

## v1.7.3 — 2026-09-03
- Botones de descarga del Layout de carga y de la Matriz del modelo (Excel) junto al importador de CSV — siempre bajan la versión vigente del sitio; solo visibles cuando la app corre publicada.

## v1.7.2 — 2026-09-03
- FI1 Tipo de persona depurado a forma jurídica pura: Persona física (1) · PF con actividad empresarial (2) · Persona moral (3) · Mandato (4) · Fideicomiso/vehículo (5). Se eliminó «PM extranjera» (doble conteo: lo extranjero ya lo miden país de nacimiento, nacionalidad y domicilio, 31% del peso). Los registros guardados con valores anteriores se migran solos al calificar.
- Edad PF en forma de U: mayores de 65 años suben a nivel 4 (tipología de adultos mayores como prestanombres), igual que 18–24 y menores de edad.
- TR-26 ajustada: interposición = persona moral/mandato/vehículo con domicilio fuera de México en rol de control.
- Matriz v2.2 y Layout v1.3 homologados con ambos cambios.

## v1.7.1 — 2026-09-03
- FI7 «Edad / antigüedad» ahora es dinámico por tipo de persona: personas físicas califican por EDAD (25–50, 51–65, +65, 18–24, menor de edad) y morales/vehículos por ANTIGÜEDAD de constitución. El combo cambia solo al cambiar el tipo de persona; la importación CSV valida según el tipo de cada fila.
- Layout v1.3: catálogo «Edad / antigüedad parte» ampliado con los rangos de edad de PF. Matriz Excel v2.2 con el mismo catálogo en FI7.

## v1.7 — 2026-09-03
- Catálogo propio para la ACTIVIDAD DEL FIDEICOMISO (14 giros típicos del vehículo, anclados a las fracciones de la LFPIORPI y tipologías: tenencia patrimonial, prestaciones laborales, sucesorio, garantía/fuente de pago, inversiones, zona restringida, arrendamiento XV, donativos XIII, préstamos IV, comercio exterior, entidad auxiliar, desarrollo inmobiliario V/V Bis, efectivo intensivo). Antes reutilizaba el catálogo de actividades de personas, que no describe al vehículo.
- TR-23 ahora dispara por nivel del catálogo (giro ≥4), robusto a renombres; TR-22 (auxiliares) intacta.
- Layout de carga v1.2: columna ActividadFideicomiso validada contra el catálogo nuevo (CATÁLOGOS col. O). El catálogo de actividad económica de INTEGRANTES no cambia.

## v1.6.1 — 2026-09-02 (tipologías Impacto360)
- TR-24 (CRÍTICA): transmisión de dominio sin origen trazable — tipología de lavado inmobiliario por transferencias no financiadas.
- TR-26 (ALTA): estructura extranjera interpuesta — desglosar UBO >25%; no presumir transparencia de LLCs de EE. UU. (exención CTA/FinCEN).
- Panorama: detección de partes presentes en varios fideicomisos del registro (firmantes/fideicomitentes recurrentes — señal de red).

## v1.6 — 2026-09-02
- Panorama del registro: gráfica de distribución por grado de riesgo (semáforo) y reporte por actividad vulnerable (Tipo A / B / C / sin dato) con n, %, «en alto» y promedio — visible cuando hay fideicomisos guardados.
- Próxima revisión sugerida por banda (ALTO 6m · MEDIO ALTO 12m · MEDIO 24m · BAJO 36m): en la tarjeta de resultado, en el registro (en rojo si ya venció), en la cédula PDF y en el export CSV.
- Paleta del semáforo recalibrada (validación de accesibilidad): naranja y rojo ahora se distinguen entre sí y para daltonismo.

## v1.5.2 — 2026-09-02
- Bandas en semáforo: BAJO verde, MEDIO ámbar, MEDIO ALTO naranja, ALTO/PROHIBITIVO rojo — en chips, tarjeta de consolidado, registro, prioridades de tratamiento (CRÍTICA roja, ALTA naranja), conteo «En alto», avisos de invalidación y cédula PDF. Tonos sobrios, legibles en modo claro y oscuro.
- Modo oscuro: corregido el texto blanco fijo sobre fondos de marca invertidos (tarjeta de consolidado, botones primarios, encabezados de tabla, etiquetas V1, toasts, fila de total).

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
