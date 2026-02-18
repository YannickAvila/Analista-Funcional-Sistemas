# ANÁLISIS FACTURACIÓN ELECTRÓNICA GNV/SEI
## Matriz ejecutiva — Estado exploración inicial

*Actualizado: 18 febrero 2026. Exploración inicial completada en Escenarios 1, 2 y 3.*

---

## CONTEXTO

Obligación normativa francesa: generación XML UBL 2.1 + comunicación con SERES como PDP (Plataforma de Desmaterialización Partner).

**Restricción transversal:** SERES no ha publicado la especificación técnica completa. Solo disponible un Excel UBL 2.1 genérico; sin campos obligatorios específicos energía/GNV/SEI, sin documentación de API ni proceso de homologación. Esta limitación afecta a todos los escenarios por igual.

---

## GNV Y SEI: DOS UNIVERSOS DISTINTOS

GNV y SEI no son un monolito. Su naturaleza de facturación es radicalmente diferente, y esto tiene implicaciones directas sobre qué escenarios pueden cubrir cada producto.

| | **GNV (abonados gasineras)** | **SEI (servicios ingeniería)** |
|---|---|---|
| **Volumen** | 250 facturas/mes | ~5 facturas/mes (irregular) |
| **Importe** | 17MM EUR/año | 1,8MM EUR/año |
| **Tipo** | Periódica regular (billing cycle) | Esporádica sin patrón |
| **Esc 1 — E4E** | Sí | Sí |
| **Esc 2 — SAP-ISU** | Sí (GNV cíclico, con condiciones) | No — incompatible por diseño |
| **Esc 3 — Kintsugi** | Sí | Sí |
| **Esc 4 — SAP especializado** | Sí | Sí (BRIM diseñado para eventos esporádicos) |

**Nota Escenario 2:** CI sobre ISU hereda el billing cycle periódico de ISU (utilities). SEI no tiene patrón regular — forzarlo exigiría configuraciones artificiales. En España, servicios equivalentes van por módulo SD. La vía para SEI en SAP queda abierta: SD Francia, integración con España, u otra solución.

---

## ESTADO DE EXPLORACIÓN POR ESCENARIO

| Escenario | Estado actual | Señal dominante | Condición de desbloqueo |
|---|---|---|---|
| **1 — E4E** | En espera | Alerta | Posición formal E4E tras valoración (congelado hasta abril) |
| **2 — SAP-ISU** | Condicional (solo GNV) | Negativa para SEI / Verde para Cobros | DSI confirma viabilidad CI-ISU para GNV cíclico sin configuraciones artificiales |
| **3 — Kintsugi** | Viable como transitorio | Verde con alertas | SERES confirma sin firma XML + Cobros define proceso estados + dirección formaliza cobertura |
| **4 — SAP especializado** | Concepto a visibilizar | Pendiente | DSI confirma disponibilidad licencias BRIM/RFNO en S/4HANA actual |

---

## MATRIZ COMPARATIVA — HALLAZGOS REALES

| Criterio | **ESC 1: E4E** | **ESC 2: SAP-ISU** | **ESC 3: Kintsugi** | **ESC 4: SAP especializado** |
|---|---|---|---|---|
| **COBERTURA PRODUCTOS** | | | | |
| GNV cíclico | Sí | Sí (con condiciones) | Sí | Sí |
| GNV one-shot | Sí | Requiere workaround | Sí | Sí |
| SEI esporádico | Sí | No (incompatible diseño) | Sí | Sí (BRIM nativo) |
| **STACK TÉCNICO REAL** | | | | |
| Arquitectura | E4E (módulo SAP customizado) | CI sobre SAP-ISU (utilities) | MySQL + Python / app externa | RFNO + BRIM (módulos especializados) |
| Generación XML UBL | A desarrollar (capacidad a confirmar) | A desarrollar (capacidad a confirmar) | A desarrollar (Python sobre MySQL) | Nativo BRIM |
| Firma electrónica SERES | A confirmar | A confirmar | Pendiente (FTP sugiere sin firma) | A confirmar |
| **ORGANIZACIÓN Y DEPENDENCIAS** | | | | |
| Dependencia interna | E4E (no quiere el proyecto; congelado hasta abril) | IT corporativo + Iliade si ruta IBIS | Ninguna (equipo Operaciones autónomo) | IT corporativo |
| Autonomía funcional | Baja | Baja | Alta | Baja |
| Riesgo organizacional | Alto (E4E rechaza + congelado) | Medio (IT disponible; Iliade externo) | Medio (dependencia 2 personas clave) | Bajo (IT corporativo involucrado) |
| **DATOS Y GAPS** | | | | |
| Datos disponibles para UBL | GAP estructural: interface Kintsugi→E4E solo sube importes contables; rediseño completo necesario | A validar (EVO → SAP vía conversor o directo) | Completos: EVO/MySQL contiene toda la información necesaria | A validar |
| **COBROS** | | | | |
| Integración cobros | Ventaja diluida: Cobros GNV/SEI opera fuera de sistemas | FICA real: gestión centralizada + bloqueo por rechazo SERES | Manual (Cobros sin proceso definido para estados SERES) | FICA real: misma ventaja que Esc 2 |
| Estados SERES | A integrar (depende E4E) | Integrable vía SAP | Manual / semi-automático | Integrable vía SAP |
| **PLAZO Y COSTE** | | | | |
| Plazo orientativo | Meses (si E4E acepta) | Meses–año | Semanas–meses | Año+ (licensing + implementación) |
| Coste desarrollo | Medio | Alto (IT + interfaces + Iliade si aplica) | Bajo (interno) | Muy alto (licensing RFNO/BRIM) |
| Coste licensing | Sin adicional | Sin adicional (CI ya activo) | Sin adicional | Sí (RFNO y/o BRIM) |
| **HORIZONTE** | | | | |
| Naturaleza de la solución | Corporativa (E4E rol a redefinir) | Corporativa (con ISU utilities como base) | Transitoria (sin integración proceso global) | Corporativa definitiva (módulos nativos) |
| ISU-Francia como base | N/A | Riesgo: ISU-Francia ya acumula exceso de adaptaciones; añadir más aleja del estándar | N/A | No — módulos especializados separados de ISU |
| **RIESGOS BLOQUEANTES** | | | | |
| Riesgo #1 | E4E rechaza formalmente tras valoración de abril | SEI incompatible por diseño (no resoluble con desarrollo) | Complejidad UBL 2.1 subestimada sin soporte técnico externo | Licensing BRIM/RFNO no disponible o prohibitivo |
| Riesgo #2 | GAP rediseño interface desproporcionado (Kintsugi→E4E) | ISU-Francia sobrecargado de adaptaciones — añadir más aumenta la deuda técnica | Dependencia en 2 personas sin cobertura formal | Prioridad baja en roadmap IT corporativo |
| Riesgo #3 | Capacidad XML E4E customizado sin confirmar | Iliade/IBIS añade coordinación externa que recae en Negocio | Cobros sin proceso definido para gestión estados SERES | Equipo SAP sin experiencia en RFNO/BRIM |

---

## INCÓGNITAS TRANSVERSALES (afectan a todos los escenarios)

| Incógnita | Estado | Acción necesaria |
|---|---|---|
| Especificación técnica SERES completa | Sin publicar: solo Excel UBL 2.1 genérico; sin campos energía ni API | Reunión SERES para obtener spec energía + documentación API + proceso homologación |
| Firma electrónica SERES | Sin confirmar (modelo FTP sugiere sin XMLDSig) | Pregunta directa a SERES: ¿firma a nivel documento o solo autenticación canal FTP? |
| Proceso Cobros GNV/SEI para estados SERES | No definido: Cobros asumía transferencias, pero GNV/SEI va en domiciliado | Reunión Cobros para definir workflow rechazos/aceptaciones (prerequisito de cualquier escenario) |
| Escenario 4 (BRIM/RFNO) — disponibilidad licencias | Desconocida: DSI no tenía este concepto en el radar | Pregunta a DSI: ¿S/4HANA actual incluye licencias BRIM y/o RFNO? |

---
---
---

# ESCENARIO 1: ADAPTAR E4E - VISIÓN FUNCIONAL
## Facturación Electrónica GNV/SEI

---

## RESUMEN EJECUTIVO

### ¿Qué es este escenario?

Este escenario propone **ampliar las capacidades de E4E** (sistema actual de registro fiscal y numeración de facturas) para que asuma la generación completa de XMLs UBL 2.1 y la comunicación con SERES como PDP (Plataforma de Desmaterialización Partner).

**Cambio respecto a hoy:** E4E pasa de ser un registro fiscal contable que recibe importes agregados, a convertirse en el hub de facturación electrónica que genera XMLs conformes a normativa francesa, comunica con SERES y provisiona estados de factura al proceso de Cobros.

### Ventajas principales

- **Aprovecha infraestructura existente:** E4E ya está integrado en el flujo y tiene rol fiscal reconocido
- **Separación de responsabilidades clara:** GAIA calcula, Kintsugi transforma, E4E registra y comunica con SERES
- **Potencial integración Cobros:** Estados SERES podrían autorizar/bloquear cobros según validación de factura
- **Escalabilidad corporativa:** Sistema corporativo con soporte IT institucional

### Limitaciones críticas (actualizadas con hallazgos)

- **Apertura organizacional comprometida:** E4E actualmente no quiere el proyecto; considera que su rol es contable, no de facturación electrónica
- **GAP datos estructural:** E4E solo recibe importes contables agregados — la interface requiere rediseño completo para soportar UBL
- **Ventaja Cobros diluida:** El departamento de Cobros GNV/SEI ya opera fuera de sistemas; la integración E4E-Cobros no aporta el valor diferencial esperado
- **Capacidad XML desconocida:** E4E es módulo SAP customizado — la capacidad de generar XML UBL no está confirmada

---

## HALLAZGOS DE LA EXPLORACIÓN INICIAL

### 1. Apertura organizacional — Señal de alerta

**Pregunta:** ¿El departamento E4E está abierto a asumir este proyecto?

**Respuesta:** E4E no quiere el proyecto. Considera que su sistema tiene rol contable, no de facturación electrónica. El equipo está congelado hasta abril. El jefe de área está presionando para que hagan la valoración.

**Análisis:** La resistencia no es técnica sino de posicionamiento. E4E defiende un perímetro funcional acotado y no quiere ampliarlo. La presión del liderazgo puede forzar la evaluación, pero no garantiza la ejecución ni la calidad del estudio técnico resultante.

**Implicación para el escenario:** Si E4E no asume el proyecto con convicción, el riesgo de ejecución deficiente o abandono a medio plazo es alto. El escenario depende críticamente de un cambio de posición de E4E — hecho o voluntad política, no confirmados aún.

---

### 2. Capacidad técnica XML — Pendiente de confirmación

**Pregunta:** ¿E4E tiene capacidad técnica para generar XMLs UBL 2.1?

**Respuesta:** E4E es un módulo SAP. La capacidad específica de generación XML no está confirmada.

**Lo que sabemos:** SAP en general sí soporta generación de XML para facturación electrónica (documentado en módulos FI/SD; capacidad de importar esquemas XSD UBL en SAP ERP 6.0). Sin embargo, E4E parece ser un desarrollo customizado sobre SAP — lo que existe en SAP estándar no implica que esté activado o desarrollado en E4E.

**Incógnita clave:** ¿E4E tiene esta funcionalidad activada, o requeriría nuevo desarrollo ABAP? ¿Integración vía SAP PI/CPI con sistemas externos?

**Implicación:** Dimensión no bloqueante por sí sola, pero crítica para estimar esfuerzo. A confirmar en estudio técnico DSI.

---

### 3. GAP datos EVO → UBL — Señal negativa

**Pregunta:** ¿Qué datos recibe E4E actualmente desde Kintsugi? ¿El EVO contiene información suficiente para construir un XML UBL 2.1?

**Respuesta:** La interface actual Kintsugi → E4E solo sube importes contables agregados. Sin títulos de factura. Sin desglose por concepto. E4E no recibe estructura de factura, solo movimientos contables.

**Análisis:** El UBL 2.1 exige desglose detallado por línea (descripción, cantidad, precio unitario, tipo impuesto, importe). La interface actual no transmite nada de esto. No es un GAP de datos faltantes en EVO — es que la interface fue diseñada para contabilidad, no para facturación electrónica.

**Implicación:** La interface Kintsugi → E4E requiere **rediseño completo**, no ampliación. Esfuerzo significativo en el lado Kintsugi (Access/VBA) y en E4E. Esto aplica independientemente de la capacidad XML de E4E.

---

### 4. Integración Cobros — Señal negativa (ventaja diferencial diluida)

**Pregunta:** ¿Cómo funciona el proceso de Cobros GNV/SEI? ¿Puede integrarse con E4E para automatizar la puesta al cobro según estados SERES?

**Respuesta:** El departamento de Cobros GNV/SEI ya opera fuera de los sistemas. E4E solo hace reconciliación bancaria contable — no gestiona el proceso de cobro. Riesgo adicional: las respuestas PDP (estados SERES) también podrían gestionarse fuera de sistemas.

**Análisis:** Una de las ventajas diferenciales del Escenario 1 era que E4E, al ser sistema corporativo, permitiría integrar estados SERES con el proceso de Cobros (autorizar/bloquear cobros automáticamente). Si Cobros ya es proceso externo a sistemas, esa integración no es posible o no aporta valor.

**Implicación:** La ventaja estratégica que diferenciaba E4E de Kintsugi (Escenario 3) se reduce significativamente. Kintsugi ya hace facturación — E4E ya no tiene una ventaja funcional clara que justifique el esfuerzo de desarrollo adicional.

---

### 5. Especificación técnica SERES — Parcialmente disponible

**Pregunta:** ¿SERES ha publicado la especificación técnica definitiva (esquema UBL 2.1, campos obligatorios, API)?

**Respuesta:** Solo disponible un Excel con los campos UBL 2.1 Francia. Sin especificación técnica de campos energía (GNV/SEI). Sin documentación de API ni proceso de homologación.

**Análisis:** La especificación disponible es un punto de partida, no un estándar técnico completo. Los campos específicos del sector energético (consumos, periodos, tipos de suministro) son los más relevantes para GNV/SEI y están sin definir.

**Implicación:** Esta limitación **aplica a todos los escenarios**, no es específica de E4E. No es bloqueante para evaluar el escenario, pero impide dimensionar con precisión el esfuerzo de mapping UBL. Requiere trabajo conjunto funcional + técnico con SERES.

---

## RESUMEN DE SEÑALES

| # | Dimensión | Señal | Observación |
|---|---|---|---|
| 1 | Apertura organizacional | Alerta | E4E no quiere el proyecto; congelado hasta abril; presión del liderazgo |
| 2 | Capacidad técnica XML | Pendiente | SAP tiene capacidad nativa pero E4E es customizado — a confirmar |
| 3 | GAP datos EVO → UBL | Negativa | Interface actual solo agrega importes contables; rediseño completo necesario |
| 4 | Integración Cobros | Negativa | Cobros GNV/SEI ya es externo a sistemas; ventaja diferencial diluida |
| 5 | Especificación SERES | Parcial | Solo Excel UBL 2.1; sin spec energía; aplica a todos los escenarios |

3 señales negativas o de alerta · 1 pendiente · 1 parcial (transversal)

---

## CRITERIO DE DECISIÓN (actualizado)

**PROFUNDIZAR si:**
- E4E confirma apertura al proyecto tras valoración (no solo bajo presión, sino con compromiso real)
- Estudio técnico DSI confirma viabilidad generación XML en el módulo E4E customizado
- Se identifica una ventaja funcional concreta de E4E vs Kintsugi que justifique el esfuerzo adicional

**EN ESPERA / CONDICIONAL:**
- Mientras E4E esté congelado (hasta abril) y la evaluación dependa de presión del liderazgo
- Mientras no esté confirmada la capacidad XML del módulo customizado
- Mientras el proceso de Cobros siga siendo externo a sistemas (la ventaja diferencial no aplica)

**DESCARTAR si:**
- E4E rechaza formalmente el proyecto tras la valoración impulsada por el liderazgo
- El GAP de rediseño de interface resulta desproporcionado (coste Kintsugi + E4E > alternativas)
- No existe ventaja funcional clara de E4E sobre Kintsugi una vez descartada la integración Cobros

---

## PRÓXIMOS PASOS — ESTUDIO TÉCNICO DSI

La DSI debe analizar las siguientes dimensiones antes de que este escenario pueda avanzar:

1. **Posición E4E:** Obtener valoración formal del departamento E4E sobre viabilidad y disposición al proyecto (no solo confirmación de que "lo estudiarán")
2. **Capacidad XML del módulo E4E:** ¿El customizado SAP tiene generación XML activa? ¿Vía ABAP, PI/CPI u otro? ¿Esfuerzo estimado de desarrollo?
3. **Rediseño interface Kintsugi → E4E:** Dimensionar esfuerzo de pasar de interface contable a interface de facturación completa (desglose UBL)
4. **Proceso Cobros GNV/SEI:** Confirmar si Cobros opera fuera de sistemas y si existe posibilidad de integración futura — o si la ventaja Cobros está definitivamente descartada
5. **Especificación SERES energía:** Trabajo conjunto con SERES para obtener campos obligatorios específicos GNV/SEI (aplica a todos los escenarios)

---
---
---

# ESCENARIO 2: ADAPTAR SAP-ISU - VISIÓN FUNCIONAL
## Facturación Electrónica GNV/SEI

---

## RESUMEN EJECUTIVO

### ¿Qué es este escenario?

Este escenario propone que **SAP asuma la facturación GNV/SEI** utilizando la arquitectura SAP actual: Convergent Invoicing (CI) instalado sobre SAP-ISU, la misma configuración que factura Electricidad mediante ficheros VEMS desde IBIS.

**Hallazgo estructural crítico — GNV y SEI son universos distintos:**
- **GNV cíclico (abonados gasineras):** facturación periódica regular → compatible en principio con CI sobre ISU (billing cycle mensual/bimestral aplicable)
- **SEI (servicios de ingeniería/instalación):** facturación esporádica sin patrón → **arquitectónicamente incompatible con ISU** (el billing cycle de ISU exige períodos regulares). En España, servicios equivalentes van por módulo SD. Para Francia las opciones quedan abiertas: SD Francia, integración con España, solución casera — **pregunta a resolver explícitamente y por separado**

El análisis de este escenario cubre principalmente GNV. SEI no es un monolito con GNV — requiere decisión independiente.

### Ventajas principales

- **Cobros integrado en FICA:** Gestión centralizada de cobros en SAP con bloqueo automático por rechazo SERES — ventaja real y diferencial frente a E4E y Kintsugi
- **Sistema corporativo con soporte IT:** Infraestructura con respaldo institucional y escalabilidad sin límites técnicos
- **Cálculo externo preservado:** CI sobre ISU no obliga a recalcular en SAP — GAIA/EVO siguen siendo el motor de cálculo; SAP asume facturación, numeración fiscal y comunicación SERES

### Limitaciones críticas (actualizadas con hallazgos)

- **SEI no encaja en CI sobre ISU sin configuraciones artificiales:** El billing cycle periódico es incompatible por diseño con eventos esporádicos. No es resoluble con desarrollo adicional — es una limitación de arquitectura
- **ISU-Francia ya sobrecargado de adaptaciones:** El ISU francés acumula demasiados customizings y ya está lejos del estándar SAP. Añadir CI sobre ISU para GNV/SEI introduce más capas sobre una base frágil — riesgo técnico real a largo plazo
- **Evidencia del fracaso previo con participación funcional:** ISU clásico fue descartado para gasineras (universo de instalaciones no natural, cálculo interno tramposo y costoso). CI sobre ISU resuelve el universo de instalaciones pero hereda la base utilities que genera la incompatibilidad con SEI
- **Dependencia Iliade si se elige ruta IBIS:** Añade un integrador externo fuera del control de DSI; el seguimiento técnico y coordinación recaerían sobre Negocio

---

## HALLAZGOS DE LA EXPLORACIÓN INICIAL

### 1. SEI vs GNV en el perímetro del escenario — Señal de alerta

**Pregunta:** ¿SEI es producto crítico que debe resolver el mismo escenario que GNV, o es marginal?

**Respuesta:** Actualmente se visualizan en conjunto, pero son universos distintos. SEI no encaja en ISU/CI-ISU sin trampas. En España los servicios equivalentes van por módulo SD.

**Análisis:** El tratamiento como "monolito GNV/SEI" oculta una asimetría arquitectónica relevante: CI sobre ISU puede absorber GNV cíclico, pero para SEI no hay billing cycle natural. Forzarlo implica configuraciones artificiales — exactamente el patrón que hizo fracasar el intento ISU previo.

**Implicación:** El resumen ejecutivo debe dejar explícito que este escenario cubre GNV cíclico y que SEI requiere decisión separada. Los ejecutivos deben entender esto antes de cualquier decisión de inversión SAP.

---

### 2. Evidencia del intento previo ISU gasineras — Señal negativa (bien documentada)

**Pregunta:** ¿Cuál fue la razón exacta del descarte? ¿Hay documentación?

**Respuesta:** Fue un estudio con participación directa del área funcional. ISU clásico exigía crear universo completo de instalaciones y aparatos — no natural para gasineras. El cálculo dentro de SAP resultó tramposo, difícil y costoso frente al tamaño del negocio.

**Análisis:** CI sobre ISU elimina el problema del universo de instalaciones. Pero hereda la base utilities de ISU, origen de la incompatibilidad con SEI. La vía viable es CI sobre ISU con cálculos externos (GAIA/EVO) — pero con riesgo de desvío del estándar en un ISU-Francia ya sobrecargado.

**Implicación:** La experiencia previa es un argumento técnico sólido y documentado. Refuerza que cualquier inversión SAP seria debe contemplar módulos especializados (Escenario 4), no repetir la lógica utilities sobre ISU.

---

### 3. Módulo SAP especializado (Escenario 4) — Señal pendiente con intención de visibilizar

**Pregunta:** ¿Hay voluntad y presupuesto para explorar módulos SAP especializados (BRIM, RFNO)?

**Respuesta:** Concepto nuevo para DSI — no estaba en su radar. El objetivo es ponerlo sobre la mesa ejecutiva: (a) a largo plazo la opción especializada es superior; (b) las adaptaciones sobre ISU-CI son workarounds que alejan del estándar, y el ISU-Francia ya tiene demasiadas.

**Análisis:** No es una decisión tomada — es una palanca de información para los ejecutivos. El riesgo de no visibilizarlo es invertir en adaptaciones ISU sin conocer que existen alternativas diseñadas específicamente para este modelo de negocio.

**Implicación:** El Escenario 2 simplificado debe concluir con remisión explícita al Escenario 4 como opción estratégica superior si la decisión es SAP. No como recomendación ejecutada, sino como concepto a incluir en el mapa de decisión ejecutivo.

---

### 4. Ventaja real de Cobros integrado en SAP — Señal verde

**Pregunta:** ¿Cobros en SAP es ventaja real o teórica, dado que Cobros GNV/SEI opera fuera de sistemas?

**Respuesta:** Sería un beneficio real. FICA centralizado en SAP aporta gestión de cobros robusta. El desarrollo de bloqueo de cobro por rechazo SERES podría reutilizarse naturalmente dentro de SAP.

**Análisis:** A diferencia de E4E (donde Cobros ya es externo → integración sin valor), en SAP la integración tiene sentido porque FICA es el módulo de gestión financiera de clientes, no solo contabilidad. El argumento Cobros sí diferencia SAP de E4E y Kintsugi.

**Implicación:** La ventaja Cobros es el argumento más sólido a favor de este escenario. Debe mantenerse en el resumen con claridad, independientemente de las limitaciones arquitectónicas sobre SEI.

---

### 5. Dependencia IBIS/Iliade — Señal de alerta

**Pregunta:** ¿Se ha sondeado a Iliade sobre viabilidad de adaptar IBIS para GNV?

**Respuesta:** Solo comentario informal, sin estudio formal. Si se aprovechan interfaces IBIS, se añade un integrador externo (Iliade) fuera del control de DSI. El seguimiento técnico y coordinación recaerían sobre Negocio.

**Análisis:** El modelo de coordinación con Iliade en Electricidad ya tiene sus roces. Extender esa dependencia a GNV/SEI sobre un proyecto no natural para IBIS añade un vector de riesgo de gestión que no está bajo control del área funcional ni de DSI.

**Implicación:** Los sub-escenarios que pasan por IBIS tienen una complejidad de gestión adicional — coordinación con Iliade recayendo en Negocio — que debe ser explícita en el análisis de riesgos.

---

## RESUMEN DE SEÑALES

| # | Dimensión | Señal | Observación |
|---|---|---|---|
| 1 | SEI vs GNV en el alcance | Alerta | Son universos distintos; SEI no encaja en CI/ISU; decisión SEI pendiente y separada |
| 2 | Intento previo ISU gasineras | Negativa | Descartado con evidencia real; CI sobre ISU resuelve instalaciones pero hereda base utilities |
| 3 | Escenario 4 (módulos especializados) | Pendiente | Concepto nuevo para DSI; objetivo es visibilizarlo para decisión ejecutiva informada |
| 4 | Cobros integrado en SAP (FICA) | Verde | Ventaja real y diferencial; reutilizable para bloqueo por rechazo SERES |
| 5 | Dependencia IBIS/Iliade | Alerta | Complejidad de gestión con integrador externo que recaería en Negocio |

1 señal verde · 1 negativa · 2 alertas · 1 pendiente

---

## CRITERIO DE DECISIÓN (actualizado)

**PROFUNDIZAR (solo GNV cíclico, sin SEI) si:**
- La decisión estratégica es SAP con configuración actual (sin inversión en módulos nuevos)
- SEI se acepta resolver por vía separada (SD Francia, integración España, solución casera)
- La ventaja de Cobros en FICA justifica la complejidad de la adaptación CI sobre ISU
- El riesgo de añadir más adaptaciones al ISU-Francia se acepta explícitamente

**EN ESPERA / REDIRIGIR a Escenario 4 si:**
- SAP es estratégico a largo plazo Y SEI debe resolverse en la misma plataforma
- La dirección quiere conocer las opciones de módulos especializados (BRIM/RFNO) antes de decidir
- Se quiere evitar replicar el patrón de adaptaciones ISU que ya aleja el sistema del estándar

**DESCARTAR (este escenario, no SAP en general) si:**
- CI sobre ISU no puede absorber GNV cíclico sin configuraciones artificiales (a confirmar con DSI)
- La complejidad de coordinación con Iliade (si se elige ruta IBIS) es inaceptable para Negocio
- Escenario 3 (Kintsugi/MySQL + Python) cubre el objetivo a corto plazo y SAP se reserva para el largo plazo con módulos adecuados

---

## PRÓXIMOS PASOS — ESTUDIO TÉCNICO DSI

1. **Separar GNV y SEI como preguntas independientes:** Solicitar a DSI análisis formal diferenciado — ¿cómo factura CI-ISU GNV cíclico con cálculos externos? ¿Qué hace España con servicios equivalentes a SEI (SD)? ¿Es trasladable a Francia?
2. **Viabilidad CI sobre ISU para GNV cíclico:** ¿Puede CI absorber GNV con GAIA/EVO como motor de cálculo externo, sin universo de instalaciones? ¿Qué adaptaciones serían necesarias? ¿Esfuerzo y coste estimado?
3. **Visibilización Escenario 4 a dirección:** Presentar concepto de módulos SAP especializados (BRIM para servicios esporádicos, RFNO/IS-OIL para operaciones gasineras) — sin compromisos, solo para que los ejecutivos decidan con mapa de opciones completo
4. **Validación ventaja Cobros en FICA:** Confirmar con equipo Cobros GNV/SEI si la integración con FICA SAP es operativamente viable y cómo se articula el bloqueo de cobro por rechazo SERES
5. **Evaluación ruta IBIS/Iliade (si se explora):** Sondeo formal con Iliade sobre capacidad técnica y voluntad para adaptar IBIS a GNV — con posición clara sobre quién gestiona la coordinación (no puede recaer indefinidamente en Negocio)

---

[Espacio para notas adicionales durante desarrollo del análisis]

---
---
---

# ESCENARIO 3: KINTSUGI COMO GENERADOR XML - VISIÓN FUNCIONAL
## Facturación Electrónica GNV/SEI

---

## RESUMEN EJECUTIVO

### ¿Qué es este escenario?

Este escenario propone **mantener el proceso actual de facturación GNV/SEI sin cambios estructurales** y añadir capacidades al ecosistema Kintsugi para que asuma la generación de XMLs UBL 2.1 y la comunicación con SERES como PDP.

**Hallazgo arquitectónico clave:** Kintsugi no es una aplicación Access/VBA monolítica — Access es solo la capa de visualización. Las tablas están en MySQL, lo que abre opciones técnicas más robustas: un script Python leyendo directamente MySQL puede generar el XML UBL 2.1 y comunicarse con SERES vía FTP o API, sin tocar la lógica Access.

**Flujo básico objetivo:** Proceso actual intacto (Podio → GAIA → EVO → Kintsugi → E4E → PDF). Tras recibir el fichero EVO, el módulo de generación XML (Python u otro) produce el XML UBL y lo deposita en el servidor FTP SERES. Los estados de retorno se gestionan manualmente por Operaciones hasta que Cobros defina su proceso.

### Ventajas principales

- **Impacto mínimo en arquitectura:** Sin cambios en cadena existente, sin dependencias de E4E, SAP ni IT corporativo
- **Autonomía funcional completa:** Desarrollo y mantenimiento controlados por el equipo, sin SLA externos ni procesos de homologación IT interna
- **Datos completos en MySQL:** EVO ya contiene toda la información necesaria para UBL 2.1; sin necesidad de enriquecer desde otros sistemas
- **Volumetría muy manejable:** 255 facturas/mes (250 GNV + 5 SEI), sin proyección de crecimiento — cualquier solución técnica lo aguanta con margen
- **Coste contenido:** Sin licencias adicionales ni consultoría externa; solo coste PDP SERES (común a todos los escenarios)

### Limitaciones críticas (actualizadas con hallazgos)

- **Complejidad UBL sin apoyo técnico externo:** Generar XML UBL 2.1 conforme al esquema SERES requiere dominio del estándar — la responsabilidad recaerá sobre personas cuya función principal no es sistemas. Riesgo real de subestimar la complejidad
- **Proceso Cobros pendiente de definir:** Cobros GNV/SEI aún no ha estudiado cómo gestionará los estados SERES; el modelo domiciliado hace que los rechazos sean funcionalmente críticos. No hay proceso definido
- **Dependencia en 2 personas clave:** La solución funciona mientras esas personas estén disponibles; sin cobertura formal ni succession plan, es un riesgo de continuidad
- **Firma electrónica SERES sin confirmar:** El modelo FTP sugiere que no se requiere XMLDSig, pero no está confirmado; si SERES exige firma avanzada, abre una complejidad adicional

---

## HALLAZGOS DE LA EXPLORACIÓN INICIAL

### 1. Viabilidad técnica del stack — Señal verde con matiz

**Pregunta:** ¿Access/VBA puede generar XML válido? ¿O es una incógnita total?

**Respuesta:** Access es solo la capa de visualización. Las tablas están en MySQL. Esto abre opciones más robustas: Python (con librerías como `lxml` o `xmlschema`) u otra aplicación externa puede leer MySQL y generar el XML sin pasar por VBA.

**Análisis:** La incógnita no es si VBA puede hacerlo — es si el equipo tiene capacidad de construir y mantener el generador XML UBL 2.1 sin soporte técnico externo. La complejidad del estándar UBL (estructura jerárquica, namespaces, validación XSD) no es trivial aunque el volumen sea bajo.

**Implicación:** El stack es viable en principio. El riesgo real es la complejidad de implementación asumida por personas con perfil funcional, no técnico.

---

### 2. Firma electrónica SERES — Señal pendiente (probablemente favorable)

**Pregunta:** ¿SERES exige firma electrónica XML (XMLDSig)?

**Respuesta:** No comunicado por SERES. El modelo de integración confirmado es servidor FTP dedicado — la autenticación es para la conexión FTP, no necesariamente para el contenido XML.

**Análisis:** En modelos de integración vía FTP con PDP, lo habitual es que la firma sea del canal (FTPS/SFTP), no del documento XML. Sin embargo, no está explícitamente confirmado. Si SERES exigiera firma avanzada XML, sería complejidad adicional pero resoluble (servicios de firma externos, certificado digital).

**Implicación:** Probablemente no bloqueante, pero a confirmar con SERES antes de iniciar desarrollo. Pregunta concreta a hacer en la siguiente reunión SERES.

---

### 3. Volumetría GNV/SEI — Señal verde

**Pregunta:** ¿Cuántas facturas se emiten mensualmente? ¿Hay crecimiento proyectado?

**Respuesta:** GNV: 250 facturas/mes (17MM EUR anuales). SEI: ~5 facturas/mes irregulares (1,8MM EUR anuales). Sin proyección de crecimiento.

**Análisis:** 255 facturas/mes es un volumen muy bajo para cualquier solución técnica. MySQL no tendrá problemas. Un script Python puede procesar este volumen en segundos. La escalabilidad no es un factor de decisión en este escenario.

**Implicación:** Dimensión completamente descartada como riesgo. La solución puede ser técnicamente sencilla y seguirá siendo válida indefinidamente en términos de volumetría.

---

### 4. Operativa estados SERES con Cobros — Señal de alerta

**Pregunta:** ¿Cobros GNV/SEI puede operar con gestión manual de estados SERES?

**Respuesta:** Cobros no ha definido su proceso. Asumían pagos por transferencia (como en España), pero GNV/SEI opera en domiciliado — los estados SERES (aceptada/rechazada) son funcionalmente críticos para el ciclo de cobro. No hay estudio de cómo gestionarán los rechazos.

**Análisis:** Este es el GAP funcional más relevante del escenario. No es un problema técnico — es un proceso de negocio no definido. Una factura rechazada por SERES en un esquema domiciliado implica que el cobro no puede ejecutarse; el workflow de corrección y reenvío afecta directamente a la tesorería. Sin proceso definido en Cobros, Operaciones no tiene con quién coordinarse.

**Implicación:** Antes de entrar en producción, Cobros debe definir su proceso de gestión de estados. Este es un deliverable funcional independiente del escenario técnico elegido — aplica a todos los escenarios.

---

### 5. Aceptabilidad como solución transitoria — Señal de alerta con condición

**Pregunta:** ¿La dirección acepta Kintsugi como puente temporal?

**Respuesta:** Implícitamente sí — la dirección sabe que otras opciones (E4E, SAP) no tendrán tiempo hábil. Pero la solución recae sobre 2 personas cuya función principal no es sistemas, y no existe cobertura formal ni marco de soporte explícito.

**Análisis:** "Transitoria aceptada por descarte de alternativas" no es lo mismo que "transitoria aceptada con visión estratégica". Sin formalización de la cobertura (quién da soporte, qué pasa si una persona no está, cuándo se migra) el escenario tiene riesgo de continuidad real.

**Implicación:** Para que el escenario sea viable como transitorio, la dirección debe formalizar: (1) quién da cobertura técnica, (2) el horizonte temporal explícito, (3) el trigger de migración. Sin esto, el riesgo de dependencia en personas clave es el mayor riesgo del escenario.

---

## RESUMEN DE SEÑALES

| # | Dimensión | Señal | Observación |
|---|---|---|---|
| 1 | Viabilidad técnica stack | Verde con matiz | MySQL + Python viable; riesgo real es complejidad UBL sin soporte técnico |
| 2 | Firma electrónica SERES | Pendiente | FTP sugiere sin firma XML; a confirmar con SERES explícitamente |
| 3 | Volumetría GNV/SEI | Verde | 255 facturas/mes, sin crecimiento — descartado como riesgo |
| 4 | Operativa Cobros / estados | Alerta | Proceso no definido; domiciliado hace los rechazos funcionalmente críticos |
| 5 | Solución transitoria | Alerta | Aceptada por necesidad, no por convicción; sin cobertura formal ni horizonte explícito |

2 señales verdes · 2 alertas · 1 pendiente (probablemente favorable)

---

## CRITERIO DE DECISIÓN (actualizado)

**PROFUNDIZAR si:**
- SERES confirma que no requiere firma XML avanzada (o que la firma del canal FTP es suficiente)
- El equipo puede dimensionar honestamente la complejidad del generador UBL (prototipo mínimo como validación)
- Cobros acepta comprometerse a definir su proceso de gestión de estados antes de producción
- La dirección formaliza el marco de cobertura y el horizonte temporal de la solución transitoria

**EN ESPERA / CONDICIONAL:**
- Mientras SERES no confirme el requerimiento de firma electrónica
- Mientras Cobros no haya iniciado la definición de su proceso de gestión de rechazos
- Mientras la dirección no haya formalizado el marco de soporte para las 2 personas clave

**DESCARTAR si:**
- SERES exige firma electrónica avanzada (XMLDSig con certificado) incompatible con las capacidades del equipo
- La dirección exige solución corporativa definitiva desde el inicio (no acepta transitorio)
- El equipo valora honestamente que la complejidad UBL supera sus capacidades sin apoyo técnico externo

---

## PRÓXIMOS PASOS — ESTUDIO TÉCNICO DSI

1. **Confirmar requerimiento firma electrónica SERES:** Pregunta directa y documentada en siguiente contacto con SERES — ¿el XML debe llevar XMLDSig o la autenticación es solo a nivel FTP/SFTP?
2. **Prototipo generador XML UBL 2.1:** Validar complejidad real con un prototipo mínimo (Python leyendo MySQL, generando XML conforme al Excel SERES disponible) — este es el test de viabilidad técnica más directo
3. **Proceso Cobros GNV/SEI:** Reunión específica con Cobros para definir workflow de gestión de estados SERES (aceptada, rechazada, corrección, reenvío) — deliverable independiente del escenario técnico
4. **Marco de cobertura y horizonte temporal:** Formalizar con dirección: quién da cobertura a las 2 personas clave, cuál es el trigger de migración a solución definitiva, qué nivel de soporte técnico externo se autoriza
5. **Especificación SERES energía:** Trabajo conjunto con SERES para obtener campos obligatorios específicos GNV/SEI (aplica a todos los escenarios)

---

## NOTAS Y COMENTARIOS ADICIONALES

[Espacio para añadir notas durante el desarrollo del análisis]
