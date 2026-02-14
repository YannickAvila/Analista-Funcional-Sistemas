# ANÁLISIS FACTURACIÓN ELECTRÓNICA GNV/SEI
## MATRIZ DE DECISIÓN EJECUTIVA - 4 ESCENARIOS

---

## 📊 MATRIZ COMPARATIVA ESCENARIOS

### Contexto

Este documento analiza **4 escenarios** para implementar facturación electrónica GNV/SEI cumpliendo normativa francesa (generación XML UBL 2.1 + comunicación plataforma SERES):

- **Escenario 1:** Adaptar E4E (sistema actual registro fiscal)
- **Escenario 2:** SAP-ISU (CI sobre ISU actual) ⚠️ **Limitaciones arquitectónicas identificadas**
- **Escenario 3:** Kintsugi (hub Access/VBA actual)
- **Escenario 4:** Sistema especializado SAP (RFNO + BRIM) - **En debate estratégico**

**Objetivo matriz:** Facilitar decisión rápida comparando criterios clave de cada escenario.

---

### TABLA COMPARATIVA MULTI-CRITERIO

| Criterio | **ESC 1: E4E** | **ESC 2: SAP-ISU** | **ESC 3: Kintsugi** | **ESC 4: Especializado** |
|---|---|---|---|---|
| **PRODUCTOS SOPORTADOS** | | | | |
| GNV cíclico (abonados) | ✅ Sí | ✅ Sí | ✅ Sí | ✅ Sí |
| GNV one-shot (tarjeta) | ✅ Sí | ⚠️ Requiere "trucos" | ✅ Sí | ✅ Sí |
| SEI (servicios esporádicos) | ✅ Sí | ❌ **Incompatible** | ✅ Sí | ✅ Sí |
| **VIABILIDAD TÉCNICA** | | | | |
| Complejidad implementación | Media | **Alta** | Baja-Media | Alta |
| Riesgo técnico bloqueante | Medio (E4E rechaza) | **Alto (SEI inviable)** | Medio (VBA XML) | Bajo (módulos nativos) |
| Arquitectura | E4E ampliado | CI sobre ISU (utilities) | Access/VBA | RFNO+BRIM (Oil&Gas) |
| Configuración | Nueva capacidad E4E | **"Tramposa"** (forzar ISU) | Desarrollo autónomo | Nativa modelo negocio |
| **DEPENDENCIAS Y ORGANIZACIÓN** | | | | |
| Dependencia departamentos | ✅ E4E (crítica) | ✅ SAP/IT + ⚠️ IBIS/Iliade | ❌ Ninguna | ✅ SAP/IT |
| Autonomía funcional | ❌ Baja (depende E4E) | ❌ Baja (depende IT) | ✅ **Alta** (desarrollo interno) | ❌ Baja (depende IT) |
| Dependencia proveedor externo | No | ⚠️ IBIS/Iliade (si elegido) | No | No (corporativo SAP) |
| Capacidad equipo conocido | A validar E4E | Equipo SAP existe | ✅ Equipo Ops (VBA) | A validar (RFNO/BRIM) |
| **FUNCIONALIDADES CLAVE** | | | | |
| Gestión cobros integrada | ⚠️ A validar sistema Cobros | ✅ **SAP FI-CA** | ❌ Manual | ✅ **SAP FI-CA** |
| Estados SERES automáticos | ⚠️ Depende integración | ✅ Integrable SAP | ❌ Manual/semi-auto | ✅ Integrable SAP |
| Generación XML UBL | A desarrollar E4E | SAP capacidad (a validar) | A desarrollar VBA | ✅ BRIM nativo |
| Escalabilidad volumétrica | Medio (depende E4E) | ✅ Alta (SAP robusto) | ⚠️ **Limitada** (Access 2GB) | ✅ Alta (SAP robusto) |
| **PLAZO Y COSTE** | | | | |
| Plazo estimado | Meses (si E4E acepta) | Meses-Año | **Semanas-Meses** | Año (licensing+impl) |
| Coste desarrollo | Medio (E4E desarrollo) | Alto (IT+IBIS+interfaces) | **Bajo** (interno) | **Muy Alto** (licensing) |
| Coste licensing adicional | No | No (ya tienen CI) | No | ✅ Sí (RFNO+BRIM) |
| Rapidez implementación | Media | Baja | ✅ **Alta** | Baja |
| **SOLUCIÓN LARGO PLAZO** | | | | |
| Estrategia corporativa | ⚠️ E4E ¿evolución/legacy? | ⚠️ ISU utilities (no gasineras) | ❌ Parche transitorio | ✅ **Solución definitiva** |
| Mantenibilidad | Media (equipo E4E) | Media (equipo SAP) | ⚠️ Baja (conocimiento concentrado) | Alta (corporativo SAP) |
| Escalabilidad futura | Media | Alta (pero SEI bloqueado) | Baja (Access límites) | ✅ **Alta** |
| Integración proceso global | Sí (sistema corporativo) | Sí (SAP central) | ❌ No (perpetúa fragmentación) | ✅ Sí (SAP central) |
| **RIESGOS PRINCIPALES** | | | | |
| Bloqueante #1 | E4E rechaza proyecto | **SEI incompatible CI/ISU** | VBA no genera XML | Licensing prohibitivo |
| Bloqueante #2 | Plataforma E4E inviable XML | Configuración tramposa ISU | Volumetría supera Access | Equipo SAP sin capacidad |
| Bloqueante #3 | Sistema Cobros no integrable | IBIS no adaptable GNV | SERES rechaza homologación | Prioridad roadmap baja |
| **RECOMENDACIÓN** | | | | |
| **Perfil recomendado** | E4E estratégico + Cobros crítico | ⚠️ **NO RECOMENDADO** | Rapidez crítica + Autonomía | SAP estratégico + SEI crítico |
| **Cuándo elegir** | E4E confirma viabilidad técnica | **Solo si SEI descartado** | Obligación legal inminente | GNV/SEI negocio crecimiento |
| **Cuándo descartar** | E4E rechaza o inviable técnico | **Si SEI es producto crítico** | Integración cobros crítica | Licensing no viable |

---

### 🎯 RECOMENDACIONES POR PERFIL DE DECISIÓN

#### 🏆 **ESCENARIO RECOMENDADO SEGÚN CONTEXTO:**

**Si SEI es producto crítico y presupuesto disponible:**
→ **ESCENARIO 4 (Sistema especializado RFNO+BRIM)**
- Único que resuelve GNV+SEI completos sin configuraciones tramposas
- Solución corporativa SAP definitiva
- Requiere validar licensing RFNO/BRIM disponible en S/4HANA actual

**Si rapidez crítica y autonomía valorada:**
→ **ESCENARIO 3 (Kintsugi)**
- Implementación más rápida (semanas-meses)
- Sin dependencias IT/E4E
- Aceptar como puente temporal hasta decisión estratégica largo plazo

**Si E4E estratégico y gestión cobros integrada crítica:**
→ **ESCENARIO 1 (E4E)**
- Requiere validar E4E acepta proyecto y viabilidad técnica
- Resuelve GNV+SEI completos con integración cobros

**NUNCA elegir Escenario 2 (SAP-ISU) si:**
- ❌ SEI es producto crítico (arquitectónicamente incompatible)
- ❌ Se quiere invertir en SAP como solución largo plazo (usar Escenario 4, no forzar ISU)
- ❌ Experiencia previa ISU gasineras descartada (repetir mismo error)

---

### 📋 PRÓXIMOS PASOS SEGÚN DECISIÓN

#### **Si decisión explorar ESCENARIO 1 (E4E):**
1. Workshop departamento E4E (apertura proyecto, viabilidad técnica)
2. Estudio técnico plataforma E4E (capacidad generación XML)
3. Identificación sistema Cobros actual (viabilidad integración)
4. Estudio especificación SERES (glosario UBL, ambiente pruebas)

#### **Si decisión explorar ESCENARIO 2 (SAP-ISU):**
⚠️ **NO RECOMENDADO** - Solo si SEI explícitamente descartado
1. Validar con SAP/IT que SEI queda fuera de alcance
2. Estudio IBIS viabilidad GNV (Iliade)
3. Definir sub-escenario (2A vs 2C)

#### **Si decisión explorar ESCENARIO 3 (Kintsugi):**
1. Estudio técnico Access/VBA (librerías XML, validación XSD)
2. POC generación XML UBL desde VBA
3. Definir workflow gestión estados SERES manual
4. Plan contingencia si Access inviable (migración Esc 1/4)

#### **Si decisión explorar ESCENARIO 4 (Sistema especializado):**
1. ✅ **CRÍTICO:** Workshop SAP/IT validar disponibilidad RFNO/BRIM en S/4HANA
2. Estudio licensing (coste activación RFNO+BRIM)
3. POC técnico generación XML UBL desde BRIM
4. Análisis funcional completo Escenario 4 (mismo nivel profundidad Esc 1/2/3)
5. Decisión arquitectura (4A: RFNO+BRIM, 4B: IS-OIL, 4C: BRIM standalone)

#### **Si SEI marginal y GNV prioritario:**
- Opción híbrida: **GNV en Escenario 2 o 4** + **SEI en Escenario 1 o 3**
- Evita bloqueo SEI en SAP-ISU
- Permite aprovechar ventajas SAP para GNV cíclico (cobros integrados)

---

### ⚠️ DECISIÓN CRÍTICA INMEDIATA

**Pregunta estratégica para dirección:**

**¿Endesa tiene licencias RFNO y/o BRIM en S/4HANA actual?**

- **SI SÍ:** Escenario 4 viable → Análisis completo prioritario
- **SI NO:** ¿Presupuesto disponible para licensing?
  - Sí → Escenario 4 explorable
  - No → Escenarios 1 o 3 (E4E o Kintsugi)

**Esta pregunta determina si Escenario 4 es opción real o descartable.**

---

### 📊 RESUMEN EJECUTIVO 30 SEGUNDOS

| Escenario | GNV+SEI | Rapidez | Coste | Largo plazo | Veredicto |
|---|:---:|:---:|:---:|:---:|---|
| **1: E4E** | ✅ | Media | Medio | ⚠️ | Viable si E4E acepta |
| **2: SAP-ISU** | ❌ SEI | Baja | Alto | ⚠️ | ⚠️ **NO RECOMENDADO** |
| **3: Kintsugi** | ✅ | ✅ Alta | ✅ Bajo | ❌ | Puente temporal |
| **4: Especializado** | ✅ | Baja | Alto | ✅ | Solución definitiva |

**Recomendación general:** Si presupuesto disponible → **Escenario 4**. Si rapidez crítica → **Escenario 3**. Si E4E estratégico → **Escenario 1**. **Evitar Escenario 2** salvo SEI descartado.

---
---
---

# ESCENARIO 1: ADAPTAR E4E - VISIÓN FUNCIONAL
## Facturación Electrónica GNV/SEI

---

## RESUMEN EJECUTIVO

### ¿Qué es este escenario?

Este escenario propone **ampliar las capacidades de E4E** (sistema actual de registro fiscal y numeración de facturas) para que asuma la generación completa de XMLs UBL 2.1 y la comunicación con SERES como PDP (Plataforma de Desmaterialización Partner).

**Cambio respecto a hoy:** E4E pasa de ser un simple registro fiscal contable que recibe importes agregados, a convertirse en un sistema de facturación electrónica completo que gestiona datos maestros cliente/contrato, recibe desglose detallado de facturas, genera XMLs conformes a normativa francesa, comunica con SERES y provisiona estados de factura al proceso de Cobros.

**Flujo básico objetivo:** El proceso mantiene su estructura actual (Podio → GAIA → EVO → Kintsugi) pero E4E se enriquece para recibir datos completos desde Kintsugi, generar el XML UBL además de la numeración fiscal, enviarlo a SERES y recibir los estados de validación que alimentan el proceso de Cobros.

### Ventajas principales

- **Aprovecha infraestructura existente:** E4E ya está integrado en el flujo y tiene rol fiscal reconocido, reduciendo el cambio arquitectónico
- **Separación de responsabilidades clara:** Cada sistema mantiene su rol (GAIA calcula, Kintsugi transforma, E4E registra y comunica con SERES)
- **Mejora proceso Cobros:** Integración de estados SERES permite autorizar/bloquear cobros automáticamente según validación de factura
- **Escalabilidad corporativa:** Solución basada en sistema corporativo con soporte IT, preparada para crecimiento de volumen

### Limitaciones críticas

- **Dependencia del departamento E4E:** El escenario requiere que E4E acepte desarrollar capacidades que hoy no tiene (MDG ampliado, generación XML, integración externa)
- **GAP funcional alto:** E4E actualmente no almacena datos de contrato, no recibe desglose de factura, y es desconocida su capacidad técnica de generación XML
- **Complejidad integraciones:** Requiere 4 interfaces nuevas o modificadas (Kintsugi→E4E enriquecida, E4E→SERES bidireccional, E4E→Cobros)
- **Incertidumbre técnica:** No se conoce la plataforma técnica de E4E ni su viabilidad para generar XMLs UBL 2.1 conformes

### Riesgos bloqueantes

1. **Rechazo departamento E4E:** Si E4E declina asumir este rol ampliado, el escenario es inviable por completo
2. **Incapacidad técnica generación XML:** Si la plataforma E4E no puede generar XMLs válidos o validar contra esquema XSD, el núcleo del escenario falla
3. **Incompatibilidad sistema Cobros:** Si el sistema actual de Cobros no puede recibir/procesar estados SERES, se pierde una ventaja clave del escenario

### Criterio de decisión: ¿Profundizar o descartar?

**PROFUNDIZAR si:**
- Departamento E4E confirma apertura al proyecto y disponibilidad de equipo
- Estudio técnico E4E valida viabilidad generación XML (plataforma, librerías, esfuerzo razonable)
- Sistema Cobros identificado y viable para integración
- SERES confirma esquema UBL 2.1 alcanzable con datos disponibles en EVO

**DESCARTAR si:**
- E4E rechaza el proyecto o no dispone de equipo/presupuesto
- Plataforma técnica E4E incompatible con generación XML (esfuerzo desproporcionado)
- GAP datos EVO→UBL insalvable (información crítica no disponible)
- Sistema Cobros no integrable (anula ventaja estratégica del escenario)

---

## PREGUNTAS CLAVE PARA DIMENSIONAR ESFUERZO

### BLOQUE 1: Viabilidad organizacional

1. **¿El departamento E4E está abierto a asumir este proyecto?** ¿Consideran estratégico evolucionar E4E hacia generación facturación electrónica o prefieren mantener rol fiscal limitado actual?
2. **¿E4E dispone de equipo técnico y presupuesto para desarrollos?** ¿Qué capacidad tienen para acometer un proyecto de esta magnitud? ¿Plazos estimados?
3. **¿Cuál es la posición de E4E respecto a evolución de emisión de facturas corporativa?** ¿Ven E4E como plataforma de futuro o sistema legacy a reemplazar?
4. **¿Existe soporte directivo para este proyecto en E4E?** ¿Hay sponsor interno que impulse la evolución del sistema?

### BLOQUE 2: Capacidad técnica

5. **¿Qué plataforma técnica usa E4E actualmente?** (lenguaje, framework, base de datos, arquitectura)
6. **¿E4E tiene capacidad de generar XMLs?** ¿Experiencia previa con generación/validación documentos XML en E4E?
7. **¿Qué librerías o herramientas XML están disponibles en la plataforma E4E?** ¿Capacidad de validación contra esquemas XSD?
8. **¿E4E puede consumir/exponer APIs externas?** ¿Experiencia previa integraciones con sistemas externos a corporativo?
9. **¿El MDG (Master Data Governance) de E4E es extensible?** ¿Puede almacenar estructura completa cliente/contrato/líneas más allá de códigos contables actuales?
10. **¿La interface de entrada actual a E4E puede recibir desglose líneas factura?** ¿O solo maneja importes agregados como hoy?

### BLOQUE 3: Magnitud del GAP funcional

11. **¿Qué datos de cliente almacena E4E actualmente?** ¿Código deudor únicamente o información ampliada? ¿Qué falta para cumplir requisitos UBL?
12. **¿E4E gestiona hoy alguna estructura de contratos?** ¿O solo recibe peticiones facturación sin contexto contractual?
13. **¿Qué información recibe E4E actualmente desde Kintsugi?** ¿Importes agregados o hay algún desglose? ¿Formato de interface actual?
14. **¿Existe documentación técnica de las interfaces actuales de E4E?** (entrada desde Kintsugi, salida hacia sistemas contables)
15. **Comparando datos disponibles en EVO vs campos obligatorios UBL 2.1:** ¿Qué GAP de información existe? ¿Todo lo necesario está en EVO o hay datos adicionales a capturar?

### BLOQUE 4: Dependencias críticas externas

16. **¿SERES ha publicado especificación técnica definitiva?** (esquema UBL 2.1, API/FTP, autenticación, proceso homologación)
17. **¿Cuál es el glosario de campos obligatorios UBL 2.1 que SERES exige?** ¿Hay campos opcionales que SERES hace obligatorios?
18. **¿SERES ofrece ambiente de pruebas?** ¿Cuándo estará disponible? ¿Proceso de acceso?
19. **¿Qué sistema usa actualmente el departamento de Cobros?** ¿Está identificado? ¿Quién lo gestiona?
20. **¿El sistema de Cobros puede recibir información automáticamente desde E4E?** ¿O solo trabaja con inputs manuales/ficheros?
21. **¿Cómo recibe Cobros hoy la información de facturas GNV/SEI?** ¿Proceso manual? ¿Export Kintsugi? ¿Frecuencia?

### BLOQUE 5: Riesgos de plazo y coste

22. **¿Cuál es el esfuerzo estimado de desarrollo en E4E?** (MDG ampliado, interface entrada, generación XML, integración SERES, salida Cobros)
23. **¿E4E puede estimar plazo de implementación si decide aceptar el proyecto?** ¿Estamos hablando de meses o años?
24. **¿Hay costes de licencias adicionales?** (librerías XML, herramientas integración, certificados firma electrónica si SERES requiere)
25. **¿Qué recursos internos serían necesarios?** (equipo E4E, equipo Cobros, DSI coordinación, funcional Francia)
26. **Si E4E falla técnicamente, ¿existe plan B?** ¿Pivote a Escenario 2 (SAP) o 3 (Kintsugi) factible?

### BLOQUE 6: Valor añadido del escenario

27. **¿Qué problemas actuales resuelve este escenario?** (cumplimiento normativo facturación electrónica, integración Cobros, trazabilidad estados)
28. **¿Qué NO resuelve este escenario que sea importante?** ¿Quedan gaps funcionales en el proceso global GNV/SEI?
29. **¿La integración E4E-Cobros es diferencial vs otros escenarios?** ¿Escenario 2 (SAP) o 3 (Kintsugi) ofrecen mejor integración Cobros?
30. **¿Este escenario facilita evoluciones futuras?** ¿O perpetúa arquitectura fragmentada?

### BLOQUE 7: Comparativa con alternativas

31. **¿Por qué E4E en lugar de SAP (Escenario 2)?** ¿Qué hace E4E más viable/rápido/barato que SAP?
32. **¿Por qué E4E en lugar de Kintsugi (Escenario 3)?** ¿Qué ventajas aporta E4E que Kintsugi no pueda ofrecer?
33. **¿E4E es solución largo plazo o puente?** ¿Estrategia corporativa apunta a consolidar en E4E o migrar a SAP en futuro?
34. **Si SERES solo requiere XML (sin integración Cobros crítica), ¿sigue teniendo sentido E4E vs Kintsugi?** ¿O la ventaja de E4E se diluye?

---

## ANÁLISIS DETALLADO

### 1. DESCRIPCIÓN FUNCIONAL

E4E asume la generación de XMLs UBL 2.1 y la comunicación con SERES como PDP. Mantiene su rol actual de registro fiscal y añade capacidades de:
- Almacenamiento datos completos cliente/contrato
- Recepción detalles factura (no solo agregados contables)
- Generación XML conforme UBL 2.1
- Envío/recepción comunicaciones SERES
- Provisión estados factura a proceso Cobros

---

## 2. FLUJO FUNCIONAL OBJETIVO

```
Podio → GAIA → EVO → Kintsugi → E4E (enriquecido) → SERES
                                    ↓                   ↓
                                Num. fiscal       Estados factura
                                    ↓                   ↓
                          PDF (¿Kintsugi/E4E?)  Sistema Cobros
```

**Nota:** Generación PDF pendiente de decisión (ver sección 6.1)

---

## 3. CAPACIDADES FUNCIONALES REQUERIDAS EN E4E

La generación completa de facturación en E4E probablemente exige desarrollar:

1. **Gestión Master Data ampliada:**
   - Almacenamiento datos cliente completos (más allá del código deudor actual)
   - Creación y gestión estructura contratos GNV/SEI
   - Vinculación contratos-clientes-cuentas contables

2. **Recepción peticiones facturación enriquecidas:**
   - Interface entrada que soporte desglose completo factura (vs. importes agregados actual)
   - Datos necesarios para generación UBL 2.1

3. **Motor generación XML UBL 2.1:**
   - Mapeo datos factura E4E → estructura UBL
   - Validación conformidad esquema SERES
   - Firma electrónica (si requerida)

4. **Integración bidireccional SERES:**
   - Envío XML facturas (API o FTP)
   - Recepción estados factura (ENTREGADA/ACEPTADA/RECHAZADA)
   - Gestión errores y reintentos

5. **Provisión información proceso Cobros:**
   - Interface salida estados SERES hacia sistema Cobros
   - Lógica autorización/bloqueo cobro según estados

**Nota:** El detalle de requisitos técnicos y funcionales será objeto del estudio técnico del departamento E4E.

---

## 4. GAP FUNCIONAL E4E

| Capacidad requerida | ¿E4E puede? | GAP |
|---|---|---|
| Almacenar datos contrato | No | Alto - estructura datos nueva |
| Almacenar datos cliente completos | Parcial | Medio - ampliar MDG |
| Recibir desglose factura | No | Alto - interface entrada |
| Generar XML | Desconocido | A estudiar técnicamente |
| Comunicar con SERES | No | Medio - integración externa |
| Gestionar estados SERES | No | Medio - tabla estados |
| Informar sistema Cobros | Desconocido | Depende sistema Cobros |

---

## 5. INTEGRACIONES NECESARIAS

### 5.1. Entrada: Kintsugi (o GAIA) → E4E
- **Qué:** Peticiones facturación con desglose completo
- **Frecuencia:** Por batch facturación
- **Contenido:** EVO transformado a formato E4E

### 5.2. Salida: E4E → SERES
- **Qué:** XML UBL 2.1 facturas
- **Frecuencia:** Por factura o batch
- **Protocolo:** API REST o FTP (a definir SERES)

### 5.3. Entrada: SERES → E4E
- **Qué:** Estados factura
- **Frecuencia:** Tiempo real (push) o polling (pull)
- **Contenido:** ID factura, estado, fecha, motivo

### 5.4. Salida: E4E → Sistema Cobros
- **Qué:** Estados factura + autorización cobro
- **Frecuencia:** A definir
- **Contenido:** A definir según proceso Cobros

---

## 6. DECISIONES FUNCIONALES PENDIENTES

### 6.1. Generación documentos PDF
- ¿SERES requiere envío PDF adjunto al XML o solo XML?
- ¿Clientes finales necesitan PDF además del XML UBL?
- Si PDF necesario:
  - **Opción A:** Kintsugi mantiene generación PDF (proceso actual)
  - **Opción B:** E4E desarrolla generación PDF (centralización completa)
  - **Opción C:** SERES transforma XML a PDF para envío cliente (si disponible)
- ¿Envío PDF a cliente gestionado por SERES o proceso separado?

### 6.2. Gestión Master Data
- ¿Quién alimenta datos contrato en E4E? (B2B manual, carga Podio, interface GAIA)
- ¿Validación duplicados cliente Gas/Electricidad?
- ¿Histórico modificaciones contrato necesario?

### 6.3. Proceso facturación
- ¿E4E recibe EVO transformado desde Kintsugi o directo desde GAIA?
- ¿Numeración fiscal antes o después confirmación SERES?
- ¿Proceso paralelo (actual + E4E/SERES) durante piloto o cutover directo?

### 6.4. Gestión estados SERES
- Factura RECHAZADA → ¿Anulación en E4E? ¿Reemisión automática?
- ¿Alertas automáticas rechazos?
- ¿SLA respuesta SERES para puesta al cobro?

### 6.5. Integración Cobros
- ¿Qué sistema usa Cobros actualmente?
- ¿Proceso cobro espera aceptación SERES o procede en paralelo?
- ¿Interface automática o reporte manual?

---

## 7. DEPENDENCIAS CRÍTICAS PARA ESTUDIO

### Del proveedor SERES:
1. Glosario definitivo campos obligatorios UBL 2.1
2. Especificación técnica API o FTP
3. Estados factura que devuelve y sus códigos
4. Proceso homologación y requisitos
5. SLA respuesta estados

### Del departamento E4E:
6. Capacidad técnica generación XML
7. Extensibilidad MDG para datos adicionales
8. Viabilidad interface entrada enriquecida
9. Capacidad integración sistemas externos
10. Posición estratégica respecto evolución emisión facturas

### Del departamento Cobros:
11. Sistema utilizado actualmente
12. Proceso puesta al cobro (automático/manual)
13. Información necesaria de estados SERES
14. Viabilidad integración con E4E

### Interno funcional:
15. ¿Podio permanece como CRM o migración prevista?
16. ¿GAIA mantiene generación EVO o evoluciona?
17. Volumen facturas GNV/SEI actual y proyección

---

## 8. RIESGOS FUNCIONALES

| Riesgo | Impacto funcional |
|---|---|
| Departamento E4E rechaza proyecto | Escenario inviable |
| GAP UBL mayor que estimado | Datos no disponibles para XML |
| Sistema Cobros incompatible | Estados SERES no procesables |
| E4E no puede almacenar contratos | Imposible generar XML completo |
| SERES exige firma electrónica | Requisito técnico adicional |

---

## 9. PREGUNTAS PARA ESTUDIOS TÉCNICOS

### Estudio técnico E4E:
- ¿Plataforma técnica E4E permite generación XML?
- ¿MDG extensible para estructura contratos?
- ¿Interface entrada puede recibir desglose líneas?
- ¿E4E puede exponer/consumir APIs externas?
- ¿Esfuerzo estimado desarrollos?

### Estudio integración SERES:
- ¿Protocolo comunicación definitivo (API/FTP)?
- ¿Autenticación requerida?
- ¿Modelo push o pull estados?
- ¿Ambiente pruebas disponible cuándo?

### Estudio proceso Cobros:
- ¿Sistema Cobros actual identificado?
- ¿Cómo recibe hoy información facturas GNV/SEI?
- ¿Puede recibir estados SERES automáticamente?
- ¿Impacto estados en proceso cobro?

---

## NOTAS Y COMENTARIOS ADICIONALES

[Espacio para añadir notas durante el desarrollo del análisis]

---
---
---

# ESCENARIO 2: ADAPTAR SAP-ISU - VISIÓN FUNCIONAL
## Facturación Electrónica GNV/SEI

---

## RESUMEN EJECUTIVO

### ⚠️ IMPORTANTE: Este escenario analiza SAP con la arquitectura ACTUAL (CI sobre ISU)

**Lectura crítica para decisores:** Este escenario documenta las **limitaciones arquitectónicas fundamentales** de usar la infraestructura SAP actual (Convergent Invoicing instalado sobre SAP-ISU) para facturación GNV/SEI. El análisis técnico (sección 2.3) demuestra que **CI sobre ISU hereda restricciones de periodicidad que hacen SEI arquitectónicamente incompatible**. Si la decisión estratégica es invertir en SAP, debe ser con **módulos especializados** (RFNO/BRIM - ver Escenario 4 en sección 14), no forzando la configuración actual.

### ¿Qué es este escenario?

Este escenario propone que **SAP asuma el proceso completo de facturación GNV/SEI** utilizando la **arquitectura SAP actual**: Convergent Invoicing (CI) instalado sobre SAP-ISU existente, la misma configuración que factura Electricidad mediante ficheros VEMS desde IBIS.

**Hallazgo técnico crítico:** La instalación de CI sobre ISU tiene implicaciones arquitectónicas fundamentales:
- **CI actúa como consolidador** de billing streams (VEMS, otros), pero **NO controla el calendario de facturación**
- El **Contract Account (FI-CA/ISU)** define el **Billing Cycle obligatorio** (períodos regulares sin huecos)
- CI **hereda las restricciones de periodicidad de ISU** diseñadas para utilities (agua, luz, gas domiciliario)
- Esta arquitectura funciona para Electricidad porque IBIS genera VEMS mensualmente (billing cycle regular)

**Consecuencia para GNV/SEI:**
- ✅ **GNV cíclico (abonados):** Compatible - billing cycle mensual/bimestral aplicable
- ⚠️ **GNV one-shot (pago tarjeta):** Requiere "trucos" (billing plan items one-time) - no natural
- ❌ **SEI (servicios esporádicos):** **INCOMPATIBLE arquitectónicamente** - no hay billing cycle aplicable para eventos irregulares

**Cambio respecto a hoy:** SAP pasa de no gestionar GNV/SEI a convertirse en el sistema central de facturación, reemplazando Kintsugi como hub y E4E como registro fiscal. El proceso de cálculo (GAIA → EVO) se mantiene, pero SAP asume todo lo posterior: incorporación de datos, facturación, numeración fiscal, generación PDF/XML, comunicación SERES y gestión de cobros integrada.

**Sub-escenarios analizados:**
- **2A End-to-end:** SAP gestiona contratos y recibe EVO directamente (con o sin IBIS para master data)
- **2B Solo fiscal:** SAP reemplaza solo a E4E (descartado - no resuelve objetivo SERES)
- **2C Conversor VEMS:** Transformación EVO → VEMS para reutilizar interface existente de Electricidad

**⚠️ TODOS los sub-escenarios comparten la misma limitación:** CI sobre ISU con restricciones de periodicidad → SEI inviable.

### Ventajas principales

- **Cobro integrado en SAP:** Gestión automática de cobros vinculada a estados SERES (vs proceso manual externo actual), con conciliación bancaria integrada
- **Sistema corporativo robusto:** Infraestructura SAP con soporte IT disponible, sólida y escalable (vs soluciones departamentales como E4E o Kintsugi)
- **Escalabilidad probada:** Preparado para crecimiento de volumen sin límites técnicos (vs limitaciones Access en Kintsugi)
- **Experiencia reutilizable:** SAP ya factura Electricidad vía Convergent Invoicing, experiencia aprovechable para GNV (aprendizaje, integraciones, equipos)

### Limitaciones críticas (BLOQUEANTES)

- **SEI arquitectónicamente incompatible con CI sobre ISU:** No es "a validar", es **incompatible por diseño**. CI sobre ISU hereda el Contract Account de ISU que obliga billing cycle periódico (mensual, bimestral...). SEI requiere facturas esporádicas sin patrón (instalación hoy, mantenimiento en 3 meses, nada durante 6 meses). El sistema fuerza elegir entre: (A) billing cycle ficticio mensual → facturas vacías si no hay eventos, o (B) billing cycle on-demand → **NO soportado en ISU**. **Conclusión técnica:** SEI debe descartarse de este escenario o resolver con arquitectura alternativa (BRIM/RFNO - ver sección 14).

- **Configuración "tramposa" heredada del intento previo ISU:** SAP-ISU fue diseñado para utilities (agua, luz, gas domiciliario con períodos regulares). El intento previo de adaptar gasineras a ISU clásico fue descartado por "configuración tramposa y costosa". CI sobre ISU **mantiene esta misma base utilities**, por tanto forzar GNV/SEI replicaría el mismo problema: configuraciones no naturales, workarounds frágiles, mantenimiento complejo. **Si se invierte en SAP, debe ser con módulos diseñados para el negocio** (RFNO Oil & Gas, BRIM servicios), no forzando ISU.

- **Complejidad arquitectónica sin resolver el problema core:** Múltiples sistemas involucrados (SAP, IBIS, GAIA, SERES, módulo Cobros), múltiples interfaces a desarrollar (EVO→SAP o EVO→VEMS, SAP→SERES, gestión master data), coordinación IT corporativo necesaria, y **al final SEI sigue sin resolverse**. Invertir esfuerzo/presupuesto en un escenario que no resuelve uno de los dos productos objetivo (SEI) no es estratégico.

- **Dependencia crítica IBIS/Iliade sin valor añadido claro:** Si se elige ruta con IBIS (sub-escenarios 2A opción A, 2C opción 1), se añade dependencia de proveedor externo (Iliade) con coste y plazo desconocidos, para adaptar IBIS a modelo negocio GNV (capacidad técnica IBIS no validada). Esta dependencia no aporta valor diferencial vs Escenarios 1 (E4E) o 3 (Kintsugi) que son autónomos.

### Riesgos bloqueantes

1. **Inversión en arquitectura equivocada (criticidad CRÍTICA):** Invertir esfuerzo y presupuesto en adaptar CI sobre ISU actual para GNV/SEI replica el error del intento previo ISU gasineras: forzar un sistema diseñado para utilities a un modelo de negocio diferente. **El riesgo no es técnico (tiene workarounds), es estratégico:** consolidar una solución "parche" que perpetúa complejidad, no resuelve SEI, y bloquea evolución futura. **Si la decisión es SAP, debe ser con módulos especializados** (RFNO/BRIM disponibles en S/4HANA), no configuraciones tramposas sobre ISU.

2. **SEI descartado por limitación arquitectónica, no funcional (criticidad ALTA):** CI sobre ISU hace SEI arquitectónicamente inviable (no es falta de desarrollo, es incompatibilidad de diseño). Avanzar este escenario significa **aceptar explícitamente que SEI queda fuera de SAP** y debe resolverse en Escenario 1 (E4E) o 3 (Kintsugi). Si SEI es producto crítico, este escenario no cumple objetivo completo.

3. **Dependencias externas críticas sin validar (criticidad ALTA):** Si se elige ruta IBIS, dependencia Iliade para adaptaciones con viabilidad técnica desconocida (¿IBIS puede modelo GNV? ¿Iliade quiere/puede desarrollarlo? ¿Coste? ¿Plazo?). Si se elige ruta conversor EVO→VEMS, viabilidad técnica transformación desconocida (estructura datos compatible, esfuerzo desarrollo). **Ambas rutas tienen incertidumbre técnica alta** que puede bloquear proyecto avanzado.

### Criterio de decisión: ¿Profundizar o descartar?

**⚠️ RECOMENDACIÓN: DESCARTAR este escenario y explorar Escenario 4 (módulos especializados) si se quiere invertir en SAP**

**DESCARTAR (Escenario 2 con CI sobre ISU) si:**
- ✅ **SEI es producto crítico** → CI sobre ISU no lo resuelve arquitectónicamente
- ✅ **Se quiere invertir en SAP como solución largo plazo** → Debe ser con módulos especializados (RFNO/BRIM), no configuraciones tramposas ISU
- ✅ **Experiencia previa intento ISU gasineras descartado** → Repetir mismo enfoque utilities en CI tendrá mismo resultado
- ✅ **Escenarios 1 (E4E) o 3 (Kintsugi) resuelven objetivo con menor complejidad** → Sin limitación SEI, sin dependencias IT/Iliade
- ✅ **Presupuesto limitado** → Inversión SAP sin resolver SEI no es eficiente

**PROFUNDIZAR (solo GNV cíclico, sin SEI) si:**
- SEI es producto marginal y aceptable resolverlo fuera de SAP (Escenario 1 o 3)
- GNV cíclico es producto principal (abonados con billing cycle mensual/bimestral)
- Decisión estratégica ya tomada: SAP con configuración actual (sin inversión módulos nuevos)
- Ventaja cobro integrado SAP es crítica (vs gestión manual Cobros en Escenarios 1/3)

**REDIRIGIR a Escenario 4 (sistema especializado) si:**
- ✅ **SAP es estratégico Y SEI es crítico** → Requiere BRIM (one-time charges) + potencialmente RFNO (operaciones gasineras)
- ✅ **Presupuesto disponible para inversión SAP seria** → Activación módulos especializados tiene coste licensing/consultoría
- ✅ **GNV/SEI es negocio de crecimiento largo plazo** → Justifica inversión solución corporativa robusta
- ✅ **Lección aprendida intento previo ISU** → Si SAP, entonces módulo correcto (Oil & Gas / Servicios), no utilities

**Pregunta clave para decidir:** ¿Tiene sentido invertir esfuerzo/presupuesto en SAP con CI sobre ISU que NO resuelve SEI, cuando existen módulos SAP especializados (RFNO/BRIM) que SÍ lo resuelven? Si la respuesta es "invertir en SAP sí, pero con módulos adecuados", entonces explorar **Escenario 4** (sección 14), no este.

---

### 🎯 CONCLUSIÓN EJECUTIVA

**Escenario 2 (CI sobre ISU actual) NO es la opción óptima para inversión en SAP.**

**Por qué:**
1. **Limitación arquitectónica fundamental:** SEI incompatible por diseño (no "a estudiar", es incompatible). Solo resuelve GNV cíclico.
2. **Repite error intento previo:** Forzar sistema utilities (ISU) a modelo negocio gasineras/servicios → configuración tramposa, mantenimiento complejo.
3. **Existen módulos SAP especializados:** RFNO (Oil & Gas gasineras) + BRIM (servicios one-time) diseñados nativamente para este caso de uso.

**Recomendación:**
- **Si decisión es SAP:** Explorar **Escenario 4 con RFNO/BRIM** (sección 14), no forzar CI sobre ISU.
- **Si presupuesto limitado o rapidez crítica:** Escenarios **1 (E4E)** o **3 (Kintsugi)** resuelven GNV+SEI completos con menor complejidad.
- **Escenario 2 solo viable si:** SEI descartado explícitamente y GNV cíclico es único producto (caso muy específico).

**Lección aprendida:** No invertir en adaptar sistema diseñado para utilities a modelo negocio diferente. Si SAP es la vía estratégica, usar el módulo correcto desde el inicio.

**Próximo paso:** Validar con SAP/IT disponibilidad RFNO/BRIM en S/4HANA actual antes de decidir ruta SAP (Escenario 2 vs Escenario 4).

---

## PREGUNTAS CLAVE PARA DIMENSIONAR ESFUERZO

### BLOQUE 1: Viabilidad organizacional

1. **¿SAP/IT considera estratégico centralizar facturación GNV/SEI en SAP?** ¿Hay visión corporativa de consolidar facturación en SAP o preferencia mantener soluciones departamentales?
2. **¿Equipo SAP tiene disponibilidad y capacidad para proyecto?** ¿Qué recursos humanos pueden dedicarse? ¿Plazos estimados?
3. **¿Cuál es la prioridad de este proyecto en roadmap SAP?** ¿Hay otros proyectos que puedan retrasar o bloquear este?
4. **¿Presupuesto disponible para desarrollos SAP + posible contratación Iliade?** ¿Hay aprobación previa o requiere business case detallado?

### BLOQUE 2: Capacidad técnica SAP

5. **¿Existe módulo SAP específico para modelo de negocio gasineras?** (crítico - intento previo SAP-ISU clásico descartado por configuración compleja)
6. **¿Convergent Invoicing soporta facturación one-shot sin períodos regulares?** (crítico para GNV pago tarjeta)
7. **¿Qué alternativa a CI existe en SAP para facturación SEI?** (CI incompatible identificado - ¿hay módulo SAP alternativo?)
8. **¿SAP puede generar XML UBL 2.1?** ¿Qué librerías o herramientas XML están disponibles? ¿Experiencia previa?
9. **¿SAP tiene experiencia previa en integraciones externas similares a SERES?** (API REST, gestión estados, reintentos)
10. **¿Qué esfuerzo requiere desarrollar interface entrada EVO → SAP?** (Sub-escenario 2A - interface directa)

### BLOQUE 3: Decisiones arquitectura (sub-escenarios)

11. **¿Qué sub-escenario se considera más viable técnicamente?** (2A end-to-end vs 2C conversor VEMS)
12. **Si Sub-escenario 2A: ¿Master data vía IBIS (opción A) o directo SAP (opción B)?** ¿Pros/contras de cada ruta?
13. **Si Sub-escenario 2C: ¿Transformación EVO→VEMS vía IBIS (opción 1) o conversor independiente (opción 2)?** ¿Cuál es más factible?
14. **¿Viabilidad técnica transformación EVO → VEMS?** ¿Estructura de datos compatible? ¿VEMS soporta conceptos GNV/SEI? ¿Esfuerzo desarrollo?
15. **¿Qué criterios usar para elegir entre sub-escenarios?** (coste, plazo, dependencias, riesgo, mantenibilidad)

### BLOQUE 4: Dependencia IBIS/Iliade

16. **¿IBIS es técnicamente adaptable al modelo de negocio GNV?** (OpenCell diseñado para utilities - ¿encaja GNV gasineras?)
17. **¿Iliade puede y quiere desarrollar adaptaciones IBIS para GNV?** (capacidad IBIS gestionar contratos GNV, transformar EVO→VEMS)
18. **¿Coste y plazo estimado adaptación IBIS?** ¿SLA soporte futuro? ¿Modelo licencias afectado?
19. **Si IBIS no viable: ¿desarrollo conversor independiente EVO→VEMS más factible?** ¿Esfuerzo comparado con interface directa EVO→SAP?
20. **¿Dependencia IBIS es estratégica o preferible evitarla?** (riesgo concentración proveedor externo)

### BLOQUE 5: GAP funcional y Master Data

21. **¿Qué datos mínimos cliente/contrato necesita SAP para generar UBL completo?** (comparado con datos disponibles en Podio/GAIA)
22. **¿Cómo resolver conflictos datos actuales clientes Gas/Electricidad antes de añadir GNV?** (problema identificado - ¿estrategia limpieza?)
23. **¿Estrategia códigos BP clientes: mezclados Gas/Elec/GNV o separados por línea de negocio?** ¿Impacto en complejidad?
24. **¿Migración clientes GNV/SEI actuales a SAP o solo nuevos contratos?** ¿Volumen migración? ¿Esfuerzo carga datos históricos?
25. **¿Podio se mantiene como CRM origen o migración prevista?** (impacta flujo alta clientes/contratos)

### BLOQUE 6: Riesgos de plazo y coste

26. **¿Esfuerzo estimado desarrollo interface EVO → SAP?** (Sub-escenario 2A - desarrollo interno SAP)
27. **¿Esfuerzo desarrollo conversor EVO → VEMS vs interface directa?** (comparativa sub-escenarios 2C vs 2A)
28. **¿Plazo global estimado proyecto SAP?** (desde inicio hasta producción - ¿meses o años?)
29. **¿Costes: licencias SAP, consultoría Iliade, desarrollos internos, homologaciones?** ¿Orden de magnitud?
30. **¿Existe plan B si SAP falla técnicamente?** ¿Pivote a Escenario 1 (E4E) o 3 (Kintsugi) factible en plazo razonable?

### BLOQUE 7: Valor añadido del escenario

31. **¿Qué problemas actuales resuelve este escenario que otros no resuelven?** (cobro integrado principalmente)
32. **¿La integración cobros en SAP es ventaja diferencial suficiente?** ¿Justifica mayor complejidad vs Escenarios 1 o 3?
33. **¿Este escenario facilita evoluciones futuras?** (ampliación productos, nuevos países, consolidación sistemas)
34. **¿Incompatibilidad SEI con CI diluye el valor del escenario?** Si SEI queda fuera, ¿sigue siendo atractivo SAP solo para GNV?

### BLOQUE 8: Comparativa con alternativas

35. **¿Por qué SAP en lugar de E4E (Escenario 1)?** ¿Qué ventajas justifican mayor complejidad y coste?
36. **¿Por qué SAP en lugar de Kintsugi (Escenario 3)?** ¿Ventaja cobro integrado suficiente vs rapidez Kintsugi?
37. **¿Visión largo plazo: SAP como solución definitiva o puente temporal?** ¿Estrategia corporativa facturación a 3-5 años?
38. **Si SERES solo requiere XML (sin integración cobros crítica inmediata), ¿sigue teniendo sentido SAP?** ¿O ventaja principal se diluye?

---

## ANÁLISIS DETALLADO

### 1. DESCRIPCIÓN FUNCIONAL

SAP-ISU asume el proceso completo de facturación GNV/SEI, desde la gestión de datos maestros hasta la generación de XMLs UBL 2.1 y comunicación con SERES. Este escenario aprovecha la infraestructura corporativa SAP existente e integra cobros dentro del sistema.

**Alcance potencial:**
- Gestión clientes/contratos en SAP
- Recepción datos cálculo (desde GAIA)
- Facturación y numeración fiscal
- Generación PDF
- Generación XML UBL 2.1
- Comunicación SERES
- Gestión cobros
- Procesamiento estados SERES

---

## 2. CONTEXTO SAP ACTUAL

### 2.1. SAP-ISU (Gas)

**Configuración:**
- Módulo ISU clásico con modelo utilities complejo (contrato, cuenta contrato, suministro, instalación, aparato, numeradores)
- Intento previo adaptar gasineras a ISU → descartado (configuración "tramposa" y costosa)

**Frontales:**
- **Magia:** Base MSSQL, interfaz BRF con SAP. Estado: congelado, a decomisar
- **Salesforce:** Réplica + cálculo PxQ en ÁGORA externo

**Procesamiento:**
- Medidas y switching gestionados dentro de SAP

### 2.2. SAP Convergent Invoicing (Electricidad)

**Configuración:**
- Misma instancia SAP, módulo CI activado
- Modelo más flexible que ISU clásico

**Sistema externo IBIS:**
- Desarrollado y operado por Iliade (basado en OpenCell)
- Gestiona: medidas, switching, altas clientes, altas contratos, cálculos
- Frontal: PPC

**Flujo:**
- IBIS genera ficheros VEMS (petición facturación)
- SAP incorpora VEMS → factura → imprime

**Conflicto identificado:**
- Clientes compartidos Gas/Electricidad → ocasionales conflictos datos

### 2.3. ARQUITECTURA CI SOBRE ISU: IMPLICACIONES TÉCNICAS PARA GNV/SEI

**Contexto crítico:** La instalación de CI sobre SAP-ISU existente tiene implicaciones arquitectónicas fundamentales que explican por qué SEI y GNV one-shot presentan incompatibilidades. Esta sección es **clave** para entender las limitaciones identificadas y las posibles soluciones.

#### 2.3.1. Cómo funciona CI sobre ISU (configuración actual Electricidad)

**Flujo técnico VEMS → CI → Factura:**

```
IBIS genera VEMS (fichero petición facturación)
    ↓
VEMS entra como billing stream en CI
    ↓
Contract Account (FI-CA) define billing cycle (mensual, bimestral...)
    ↓
CI consolida billing streams según billing cycle del Contract Account
    ↓
CI crea invoicing order (tabla DFKKINV_TRIG) con atributo Target Process = ISU1
    ↓
ISU invoicing procesa invoicing order → factura final
```

**Elementos clave de la arquitectura:**

1. **Contract Account (FI-CA)** es el master data que controla la facturación
   - Hereda del modelo ISU utilities (agua, luz, gas domiciliario)
   - Define el **Billing Cycle** obligatorio (períodos regulares sin huecos)
   - Determina target date of billing y target date of invoicing

2. **CI actúa como motor de consolidación** de billing streams
   - Recibe streams de múltiples fuentes (VEMS, otros sistemas)
   - **Respeta el billing cycle del Contract Account** (no lo controla)
   - Consolida streams en una factura según periodicidad definida

3. **ISU invoicing procesa la factura final**
   - CI crea invoicing orders que ISU invoicing ejecuta
   - ISU aplica sus reglas de facturación (períodos sin huecos, una factura por período)

**Conclusión técnica:** VEMS es un billing stream externo que CI consolida, pero el **trigger y calendario de facturación** siguen controlados por el **Contract Account ISU/FI-CA**.

**Fuentes:** [SAP ISU Invoicing Integration with CI](https://sachinhpatil.com/sapis-utilities/sap-isu-invoicing-integration-with-sap-convergent-invoicing/), [Convergent Invoicing Architecture](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/fc005cff24e9430691c1e05ffd5f0eee/e414f62e5dae4df993320bdcb1b2e1ea.html)

#### 2.3.2. Por qué las restricciones ISU persisten en CI

**El Billing Cycle es el culpable:**

El Contract Account define el Billing Cycle que determina:
- ✅ Periodicidad obligatoria (mensual, bimestral, trimestral...)
- ✅ Prohibición huecos entre períodos de facturación
- ✅ Una factura por período (no múltiples facturas esporádicas)
- ✅ Fecha objetivo facturación vinculada al ciclo

**Impacto por producto:**

| Producto | Modelo facturación | Compatibilidad CI sobre ISU | Razón |
|---|---|:---:|---|
| **Electricidad (actual)** | Cíclica mensual | ✅ | Billing cycle mensual natural, VEMS generado mensualmente |
| **GNV cíclico (abonados)** | Cíclica mensual/bimestral | ✅ | Billing cycle aplicable, facturación regular |
| **GNV one-shot (tarjeta)** | Eventos irregulares | ⚠️ | Requiere "trucos" (billing plan items one-time), no natural |
| **SEI** | Facturas esporádicas sin patrón | ❌ | Incompatible - no hay billing cycle aplicable |

**Por qué SEI es incompatible técnicamente:**

SEI requiere facturar eventos esporádicos sin periodicidad (instalación hoy, mantenimiento dentro de 3 meses, nada durante 6 meses...). El Contract Account **obliga** a definir un billing cycle, lo que fuerza a:
- Opción A: Billing cycle ficticio (ej. mensual) → facturas vacías si no hay eventos
- Opción B: Billing cycle "on-demand" → **NO soportado en ISU**, requiere período predefinido

**Conclusión:** CI sobre ISU hereda las restricciones de periodicidad de ISU, haciendo SEI arquitectónicamente incompatible sin solución alternativa.

**Fuentes:** [Contract Accounts for Convergent Invoicing](https://learning.sap.com/learning-journeys/implementing-sap-convergent-invoicing/describing-contract-accounts-for-convergent-invoicing), [Convergent Invoicing Scheduling](https://sapisurdg.wordpress.com/2014/10/29/convergent-invoicing-scheduling/)

#### 2.3.3. La diferencia crítica: CI sobre ISU vs CI standalone

**Configuración actual (CI sobre ISU):**

| Aspecto | Implementación | Limitación | Impacto GNV/SEI |
|---|---|---|---|
| **Billing trigger** | Billing cycle del Contract Account | Periodicidad obligatoria | ❌ SEI inviable |
| **Master data** | Contract Account (FI-CA/ISU) | Modelo utilities | ⚠️ No diseñado para gasineras |
| **Invoicing order** | Creada por CI, procesada por ISU | Hereda restricciones ISU | ❌ One-shot complejo |
| **Facturación** | ISU invoicing ejecuta | Períodos sin huecos obligatorios | ❌ SEI bloqueado |

**CI standalone (sin ISU):**

| Aspecto | Implementación | Flexibilidad | Beneficio GNV/SEI |
|---|---|---|---|
| **Billing trigger** | Event-driven o manual | Sin periodicidad obligatoria | ✅ SEI viable |
| **Master data** | Provider Contract (CI puro) | Flexible (subscription, one-time, usage) | ✅ Mix modelos natural |
| **Invoicing order** | CI gestiona ciclo completo | Sin restricciones ISU | ✅ One-shot nativo |
| **Facturación** | CI controla todo | Libertad calendario | ✅ Facturas esporádicas OK |

**Conclusión arquitectónica:** Vuestra instalación CI está "atada" a ISU, heredando limitaciones de periodicidad que hacen SEI incompatible. CI standalone resolvería el problema, pero requiere arquitectura diferente.

**Fuentes:** [ISU to CI Integration Case](https://community.sap.com/t5/financial-management-blog-posts-by-members/sap-billing-and-revenue-innovation-management-and-utilities-case-4-isu-to/ba-p/13551130), [Billing Process Execution](https://learning.sap.com/learning-journeys/implementing-sap-convergent-invoicing/explaining-the-billing-process-execution)

#### 2.3.4. Soluciones técnicas identificadas

**Opción 1: BRIM (Billing and Revenue Innovation Management)**

BRIM permite **CI standalone** (sin Contract Account ISU) usando **Provider Contract**:

```
Provider Contract (CI puro) → Billing Plan → Plan Items:
  - PROF (one-time fees) → SEI ✅
  - PROR (recurring charges) → GNV cíclico ✅
  - PROP (usage-based charges) → Si aplica ✅
```

**Ventajas BRIM:**
- ✅ SEI viable (one-time charges nativos, sin billing cycle obligatorio)
- ✅ GNV one-shot viable (event-driven billing)
- ✅ Mix modelos en mismo sistema (cíclico + one-shot)
- ✅ Diseñado para servicios (no utilities), más natural para gasineras

**Arquitectura posible:**
```
Gas ISU → Mantiene Contract Account (facturación cíclica actual)
GNV/SEI → BRIM nuevo (Provider Contract) → CI consolidado
Ambos coexisten en mismo S/4HANA
```

**Pregunta crítica SAP/IT:** ¿Podéis crear Provider Contracts (CI standalone) para GNV/SEI sin tocar ISU Gas? ¿BRIM está disponible en vuestra instalación S/4HANA?

**Fuentes:** [SAP BRIM Overview](https://www.sap.com/products/financial-management/billing-revenue-innovation-management.html), [BRIM Commodity and Non-Commodity](https://blogs.sap.com/2023/03/20/sap-billing-and-revenue-innovation-management-commodity-and-non-commodity-services-on-one-or-separate-invoice-is-no-longer-a-dream/)

**Opción 2: RFNO (Retail Fuel Network Operations)**

Módulo S/4HANA **específico para redes de estaciones de servicio** (gasineras):

**Diseñado para:**
- Gestión operativa gasineras (inventario combustible, fleet cards, POS integrado)
- Modelos COCO, CODO, DODO (company/dealer owned/operated)
- Payment handling tarjetas pago (crítico para GNV one-shot)

**Arquitectura propuesta:**
```
RFNO → Gestión operativa gasineras + clientes/contratos
BRIM → Facturación flexible (mix cíclico + one-shot)
ISU Gas → Independiente (sin tocar)
```

**Ventajas vs ISU clásico:**
- ✅ RFNO diseñado **nativamente** para modelo negocio gasineras (no "trucos")
- ✅ Evita configuración "tramposa" del intento previo ISU
- ✅ Solución industria Oil & Gas corporativa (no departamental)

**Pregunta crítica SAP/IT:** ¿Tenéis RFNO licenciado en S/4HANA? ¿Es compatible RFNO + BRIM para facturación GNV/SEI?

**Fuentes:** [Understanding RFNO in S/4HANA](https://community.sap.com/t5/enterprise-resource-planning-blog-posts-by-members/understanding-retail-fuel-network-operations-rfno-in-s-4hana-what-why-and/ba-p/13746939), [SAP S/4HANA RFNO](https://www.implico.com/sap-s-4-hana-rfno/)

**Opción 3: IS-OIL Downstream con SSR (Service Station Retailing)**

Solución industria Oil & Gas específica para downstream (refinación, distribución, retail):

**Componentes:**
- **SSR:** Operaciones retail gasineras, integración POS tiempo real
- **Sales & Distribution:** Billing específico fuel sales
- **Formula & Average Pricing:** Lógica pricing automática integrada

**Aplicabilidad:** Diseñado para distribución secundaria desde terminales a retail (modelo B2B suministro GNV).

**Pregunta crítica SAP/IT:** ¿Endesa tiene IS-OIL implementado para otro negocio? ¿Esfuerzo activar SSR para gasineras?

**Fuentes:** [SAP IS-OIL Downstream Solutions](https://www.cleverence.com/articles/sap-documentation/sap-oil-&-gas-(is-oil-downstream)-8421/), [IS-OIL Complete Guide](https://www.multisoftsystems.com/article/sap-oil-&-gas-is-oil-downstream-a-complete-guide)

**Opción 4: "Workarounds" en CI actual (NO recomendado)**

Intentar forzar CI sobre ISU actual con trucos:
- Billing Plan Items con one-time fees (customización forzada)
- Contract Account "dummy" con billing cycle artificial
- Event-based billing triggers (desarrollo custom)

**Valoración:**
- ❌ Configuración "tramposa" (mismo problema intento previo ISU gasineras)
- ❌ Mantenimiento complejo y frágil
- ❌ No natural para el negocio, solución parche
- ❌ SEI seguiría siendo problemático

**Conclusión:** Descartar esta opción. Si SAP es la vía, debe ser con módulo adecuado (BRIM/RFNO/IS-OIL).

#### 2.3.5. Impacto en los sub-escenarios 2A, 2B, 2C

**Todos los sub-escenarios actuales asumen CI sobre ISU**, por tanto:

| Sub-escenario | GNV cíclico | GNV one-shot | SEI | Comentario |
|---|:---:|:---:|:---:|---|
| **2A: End-to-end** | ✅ | ⚠️ | ❌ | SEI requiere BRIM/RFNO alternativo |
| **2B: Solo fiscal** | N/A | N/A | ❌ | No resuelve SERES (descartado) |
| **2C: Conversor VEMS** | ✅ | ⚠️ | ❌ | Mismas limitaciones que 2A |

**Actualización criterio decisión:**

- Si **BRIM/RFNO/IS-OIL NO disponibles** → SEI debe descartarse de Escenario 2 (resolver en Escenario 1 o 3)
- Si **BRIM/RFNO/IS-OIL SÍ disponibles** → Escenario 2 viable para GNV+SEI, pero con arquitectura diferente (ver sección 14)

---

## 3. SUB-ESCENARIOS

### SUB-ESCENARIO 2A: SAP END-TO-END

#### Descripción
SAP asume todo el proceso: desde gestión contratos hasta generación XML y comunicación SERES.

#### Flujo funcional
```
Podio/GAIA → Alta cliente/contrato → SAP (IBIS o directo)
                                        ↓
             GAIA → EVO → SAP (interface entrada)
                            ↓
                SAP: Facturación + PDF + XML → SERES
                            ↓                      ↓
                         Cobros              Estados factura
```

#### Características
- **Master Data:** Clientes y contratos gestionados en SAP (¿vía IBIS o directo?)
- **Cálculo:** GAIA mantiene cálculo (no se toca)
- **Interface entrada:** Nueva interface SAP para incorporar EVO
- **Facturación:** SAP genera factura, PDF, XML UBL
- **Cobros:** Integrado en SAP (mejora vs situación actual)
- **SERES:** SAP gestiona envío/recepción estados

#### Decisiones arquitectura pendientes

**Gestión Master Data:**
- **Opción A:** IBIS centraliza alta clientes/contratos (GNV + Electricidad)
  - Pros: Aprovecha infraestructura existente, único punto entrada
  - Contras: Dependencia Iliade, capacidad IBIS adaptarse a GNV desconocida
  
- **Opción B:** Alta directa en SAP desde Podio/GAIA
  - Pros: Sin dependencia IBIS, control directo
  - Contras: Nueva interface a desarrollar, duplicidad arquitectura vs Electricidad

**Comunicación frontal → SAP:**
- ¿Podio comunica con IBIS/SAP o sigue siendo exportación manual?
- ¿GAIA envía EVO directo a SAP o vía Kintsugi?

**Clientes compartidos:**
- ¿Mezclamos clientes Gas/Electricidad/GNV en mismo código BP?
- ¿Códigos BP separados por línea negocio?
- ¿Cómo gestionamos conflictos datos actuales Gas/Electricidad?

#### Aplicabilidad por producto

**GNV:**
- **Facturación cíclica (abonados):** Compatible con CI (períodos regulares)
- **Facturación one-shot (pago tarjeta):** A validar compatibilidad CI
  - ¿CI obliga período sin huecos? → Análisis necesario
  - ¿Proceso pago tarjeta integrable en SAP?

**SEI:**
- **Facturas one-shot no cíclicas:** INCOMPATIBLE con CI
  - CI requiere períodos de cálculo sin huecos
  - SEI son facturas esporádicas sin periodicidad
  - **Conclusión:** SEI no viable en Sub-escenario 2A con CI

#### GAP funcional principal
- Datos mínimos cliente/contrato en IBIS+SAP (a determinar con IT)
- Viabilidad interface EVO → SAP
- ¿IBIS adaptable a modelo negocio GNV? (consulta Iliade necesaria)
- SEI requeriría solución alternativa fuera de CI

---

### SUB-ESCENARIO 2B: SAP REEMPLAZA SOLO E4E

#### Descripción
SAP asume únicamente el rol de E4E (registro fiscal). Resto del proceso sin cambios.

#### Flujo funcional
```
GAIA → EVO → Kintsugi → SAP (registro fiscal) 
                           ↓
                      Num. fiscal
                           ↓
                    Kintsugi (PDF)
                           ↓
                      ¿SERES?
```

#### Características
- **Alcance limitado:** SAP solo registra contablemente
- **Kintsugi:** Mantiene generación PDF y hub central
- **Mejora:** Cobro integrado en SAP (vs E4E actual)
- **Problema crítico:** SAP no tendría datos completos para generar UBL → NO resuelve comunicación SERES

#### Valoración
**No recomendado:** No resuelve el objetivo principal (facturación electrónica SERES). Cambio incremental sin resolver problema de fondo.

---

### SUB-ESCENARIO 2C: IBIS/CONVERSOR COMO TRANSFORMADOR EVO→VEMS

#### Descripción
Reutilizar interface VEMS existente de Electricidad transformando ficheros EVO en VEMS.

#### Flujo funcional - Opción 1 (vía IBIS)
```
GAIA → EVO → IBIS (transforma EVO a VEMS)
                ↓
             VEMS → SAP (interface existente Electricidad)
                      ↓
            SAP: Facturación + PDF + XML → SERES
```

#### Flujo funcional - Opción 2 (conversor independiente)
```
GAIA → EVO → Conversor EVO-VEMS (desarrollo nuevo)
                ↓
             VEMS → SAP (interface existente Electricidad)
                      ↓
            SAP: Facturación + PDF + XML → SERES
```

#### Características
- **Ventaja principal:** Reutiliza camino abierto para Electricidad (interface VEMS ya probada)
- **Transformación crítica:** EVO → VEMS (viabilidad técnica desconocida)

#### Viabilidad técnica a validar
- ¿Estructura EVO compatible con VEMS? (formatos, datos, granularidad)
- ¿VEMS soporta conceptos específicos GNV/SEI?
- Si vía IBIS: ¿Iliade puede/quiere adaptar IBIS para transformación EVO?
- Si conversor: ¿Esfuerzo desarrollo conversor vs interface directa EVO-SAP?

#### Aplicabilidad por producto
- **GNV cíclico:** Potencialmente viable (similar a Electricidad)
- **GNV one-shot:** A validar (misma limitación que 2A)
- **SEI:** INCOMPATIBLE (misma razón que 2A - CI requiere períodos)

---

## 4. PREGUNTA ESTRATÉGICA ABIERTA → **RESPONDIDA**

**¿Existe módulo SAP específico para modelo negocio gasineras?**

Contexto: Intento previo adaptar gasineras a SAP-ISU clásico descartado por configuración compleja y poco natural.

### ✅ RESPUESTA: SÍ, EXISTEN 3 MÓDULOS ESPECÍFICOS

**1. SAP RFNO (Retail Fuel Network Operations)** ⭐ MÁS RELEVANTE

Módulo S/4HANA **diseñado específicamente para redes de estaciones de servicio**:
- **Modelos soportados:** COCO, CODO, DODO (company/dealer owned/operated)
- **Funcionalidades gasineras:** Gestión inventario combustible, payment handling tarjetas, fleet card management, integración POS tiempo real
- **Ventaja vs ISU clásico:** Diseñado nativamente para modelo negocio gasineras (sin configuraciones "tramposas")

**2. SAP IS-OIL Downstream con SSR (Service Station Retailing)**

Solución industria Oil & Gas específica downstream:
- **SSR:** Operaciones retail gasineras, billing fuel sales, integración POS
- **Aplicabilidad:** Distribución secundaria desde terminales a retail (modelo B2B suministro GNV)
- **Componentes:** Sales & Distribution específico, Formula & Average Pricing integrado

**3. SAP BRIM (Billing and Revenue Innovation Management)** ⭐ CRÍTICO PARA SEI

Suite facturación compleja que **resuelve incompatibilidad SEI con CI**:
- **Modelos soportados:** One-time charges (SEI), recurring (GNV cíclico), usage-based, bundles
- **Arquitectura:** Provider Contract (CI standalone) sin restricciones Contract Account ISU
- **Ventaja crítica:** Mix facturación cíclica + one-shot en mismo sistema (imposible con CI sobre ISU actual)

### 🎯 Impacto en el análisis Escenario 2

**Riesgos mitigados:**
- ✅ "No existe módulo SAP gasineras" → **RFNO/IS-OIL existen y están diseñados para esto**
- ✅ "CI incompatible SEI" → **BRIM soporta one-time charges nativamente**
- ✅ "Configuración compleja como intento previo" → **RFNO evita configuraciones tramposas**

**Escenario 2 se bifurca en dos rutas:**
- **Ruta A (actual):** CI sobre ISU → Solo viable para GNV cíclico, SEI descartado
- **Ruta B (nueva):** BRIM/RFNO/IS-OIL → Viable para GNV+SEI, arquitectura especializada

**Decisión estratégica abierta:** ¿Mantener Escenario 2 con limitaciones ISU o explorar **Escenario 4: Sistema especializado gasineras** (RFNO+BRIM)? Ver sección 14.

---

## 5. MATRIZ COMPARATIVA SUB-ESCENARIOS

| Aspecto | 2A: End-to-end | 2B: Solo fiscal | 2C: Conversor VEMS |
|---|---|---|---|
| **Alcance funcional** | Completo | Mínimo | Completo |
| **Resuelve SERES** | Sí | No | Sí |
| **Resuelve Cobros** | Sí | Sí | Sí |
| **Reutiliza existente** | Parcial (IBIS?) | Total | Sí (interface VEMS) |
| **Complejidad** | Alta | Baja | Media-Alta |
| **GNV cíclico** | Viable | N/A | Viable |
| **GNV one-shot** | A validar | N/A | A validar |
| **SEI** | No viable (CI) | N/A | No viable (CI) |
| **Dependencia Iliade** | Si usa IBIS | No | Si opción 1 |
| **Viabilidad técnica** | Depende IBIS/CI | Probada | Desconocida (EVO-VEMS) |

---

## 6. GAP FUNCIONAL PRINCIPAL

| Elemento | Estado actual | Requerido | GAP |
|---|---|---|
| **Alta cliente GNV/SEI en SAP** | No existe | Necesario | Alto - definir proceso |
| **Alta contrato GNV/SEI en SAP** | No existe | Necesario | Alto - modelo datos |
| **Interface entrada EVO** | No existe | Necesario (2A, 2C) | Alto - desarrollo |
| **Transformación EVO→VEMS** | No existe | Si 2C | Desconocido - viabilidad |
| **Generación XML UBL SAP** | Desconocido | Necesario | A estudiar |
| **Integración SAP-SERES** | No existe | Necesario | Medio - similar otras integraciones |
| **Modelo CI para GNV one-shot** | No validado | Necesario | Desconocido |
| **Modelo CI para SEI** | Incompatible | Alternativa requerida | Crítico |

---

## 7. INTEGRACIONES NECESARIAS

### 7.1. Entrada: Frontal → SAP (Master Data)

**Opciones:**
- **A:** Podio → IBIS → SAP (clientes/contratos)
- **B:** Podio → SAP directo
- **C:** GAIA → SAP (contratos, si GAIA centraliza)

**A definir:**
- Flujo aprobado
- Datos mínimos cliente/contrato
- Frecuencia sincronización

### 7.2. Entrada: GAIA → SAP (Cálculos)

**Opciones:**
- **2A:** EVO → Interface SAP directa
- **2C opción 1:** EVO → IBIS → VEMS → SAP
- **2C opción 2:** EVO → Conversor → VEMS → SAP

**A definir:**
- Viabilidad técnica cada opción
- Esfuerzo desarrollo

### 7.3. Salida: SAP → SERES

**Funcionalidad:**
- Generación XML UBL 2.1
- Envío (API o FTP)
- Recepción estados

**Similitud:** Otras integraciones SAP con externos (experiencia aprovechable)

### 7.4. Interna: SAP Cobros

**Ventaja:** Ya integrado (vs situación actual E4E)
- Estados SERES → Proceso cobro automático
- Conciliación bancaria en SAP

---

## 8. DECISIONES FUNCIONALES PENDIENTES

### 8.1. Arquitectura Master Data
- ¿IBIS centraliza clientes/contratos GNV o gestión separada?
- ¿Clientes mezclados Gas/Electricidad/GNV o códigos BP independientes?
- ¿Cómo resolver conflictos datos actuales Gas/Electricidad?
- ¿Podio se mantiene como CRM origen o migración prevista?

### 8.2. Interface cálculos
- ¿EVO directo a SAP o transformación VEMS?
- Si transformación: ¿vía IBIS o conversor independiente?
- ¿GAIA mantiene generación EVO o evoluciona?

### 8.3. Alcance por producto
- ¿Solo GNV en Escenario 2 y SEI en Escenario 3?
- ¿Solución SAP diferente para SEI (fuera CI)?
- ¿GNV one-shot pago tarjeta cómo se gestiona?

### 8.4. Generación documentos
- ¿SAP genera PDF o Kintsugi mantiene esta función?
- ¿SERES requiere PDF además de XML?

### 8.5. Estrategia clientes
- ¿Migración clientes GNV/SEI actuales a SAP o solo nuevos?
- ¿Coexistencia temporal procesos (actual + SAP)?

---

## 9. DEPENDENCIAS CRÍTICAS PARA ESTUDIO

### Del proveedor Iliade (si se usa IBIS):
1. Capacidad técnica IBIS para adaptarse a modelo GNV
2. Viabilidad transformación EVO → VEMS en IBIS
3. Coste y plazo adaptación IBIS
4. SLA soporte IBIS para GNV

### Del departamento SAP/IT:
5. ¿Módulo SAP específico gasineras existe?
6. Modelo datos cliente/contrato mínimo SAP para UBL
7. Viabilidad CI para GNV one-shot (períodos no regulares)
8. Alternativa SEI fuera de CI
9. Capacidad técnica SAP generación XML UBL
10. Experiencia previa integraciones SAP-externos (SERES similar)

### Del proveedor SERES:
11. Glosario definitivo campos obligatorios UBL 2.1
12. Especificación técnica API o FTP
13. Estados factura y códigos
14. Proceso homologación

### Interno funcional:
15. Estrategia Podio (mantener o migrar CRM)
16. Estrategia GAIA (EVO permanente o evolución)
17. Volumen GNV cíclico vs one-shot (% distribución)
18. Volumen SEI proyectado
19. Decisión producto único (GNV+SEI) o separado

---

## 10. RIESGOS FUNCIONALES

| Riesgo | Impacto funcional | Criticidad |
|---|---|---|
| IBIS no adaptable a GNV | Sub-escenario 2C inviable | Alta si se elige 2C |
| CI incompatible GNV one-shot | Parte GNV fuera de SAP | Media |
| CI incompatible SEI | SEI requiere solución alternativa | Alta |
| Clientes compartidos conflictos | Datos inconsistentes Gas/Elec/GNV | Media |
| EVO no transformable a VEMS | Sub-escenario 2C inviable | Alta si se elige 2C |
| No existe módulo SAP gasineras | Configuración compleja como intento previo | Media |
| Iliade no disponible/costoso | Dependencia externa crítica | Media-Alta |

---

## 11. PREGUNTAS PARA ESTUDIOS TÉCNICOS

### Estudio SAP/CI:
- ¿Existe módulo SAP específico gasineras?
- ¿CI soporta facturación one-shot sin períodos regulares?
- ¿Qué alternativa a CI para SEI en SAP?
- ¿Modelo datos mínimo cliente/contrato SAP para UBL?
- ¿SAP puede generar XML UBL 2.1? ¿Librerías disponibles?
- ¿Esfuerzo desarrollo interface entrada EVO?

### Estudio IBIS/Iliade:
- ¿IBIS técnicamente adaptable a modelo negocio GNV?
- ¿IBIS puede transformar EVO en VEMS?
- ¿Coste y plazo adaptación IBIS?
- ¿Alternativa: desarrollo conversor EVO-VEMS independiente más viable?

### Estudio viabilidad EVO-VEMS:
- ¿Estructura EVO compatible con VEMS?
- ¿VEMS soporta conceptos específicos GNV/SEI?
- ¿Esfuerzo desarrollo conversor vs interface directa?

### Estudio integración SERES:
- ¿Experiencia previa SAP integraciones similares?
- ¿Protocolo comunicación definitivo (API/FTP)?
- ¿Esfuerzo estimado integración SAP-SERES?

### Estudio Master Data:
- ¿Estrategia clientes: mezclados o separados por línea negocio?
- ¿Cómo resolver conflictos datos actuales Gas/Electricidad?
- ¿Migración datos Podio → SAP necesaria? ¿Volumen?

---

## 12. VENTAJAS ESTRATÉGICAS ESCENARIO 2

Independientemente del sub-escenario elegido:

1. **Cobro integrado:** Gestión automática en SAP (vs manual actual)
2. **Sistema corporativo:** Infraestructura robusta y soportada
3. **Escalabilidad:** Preparado para crecimiento volumen
4. **Centralización:** Reduce dependencia herramientas desconectadas (Podio, Kintsugi)
5. **Experiencia:** SAP ya factura Electricidad (aprendizaje reutilizable)
6. **Soporte IT:** Equipo SAP disponible (vs resistencia E4E)

---

## 13. LIMITACIONES IDENTIFICADAS

1. **SEI incompatible con CI:** Requiere solución alternativa o mantener fuera de SAP
2. **GNV one-shot:** Compatibilidad CI a validar (posible limitación períodos)
3. **Complejidad:** Mayor que Escenario 1 o 3 (múltiples sistemas involucrados)
4. **Dependencia IBIS:** Si se elige ruta IBIS, dependencia Iliade crítica
5. **Conflicto clientes:** Gas/Electricidad actual a resolver antes de añadir GNV
6. **Datos maestros:** Requiere poblar SAP con información no disponible hoy

---

## 14. HACIA UN ESCENARIO 4: SISTEMA ESPECIALIZADO GASINERAS/SEI

**Contexto del debate estratégico:**

El análisis técnico de la arquitectura CI sobre ISU (sección 2.3) y el descubrimiento de módulos SAP especializados (RFNO, BRIM, IS-OIL) abren una **cuarta línea de análisis** no contemplada inicialmente: implementar un **sistema SAP especializado dedicado** para el modelo de negocio gasineras/SEI, independiente de la infraestructura ISU Gas/Electricidad actual.

### 14.1. ¿Por qué considerar un Escenario 4 separado?

**Diferencias fundamentales con Escenario 2 (CI sobre ISU):**

| Aspecto | Escenario 2 (actual) | Escenario 4 (especializado) |
|---|---|---|
| **Arquitectura base** | CI sobre ISU existente | RFNO/BRIM/IS-OIL independiente |
| **Limitaciones ISU** | Hereda restricciones billing cycle | Sin restricciones ISU |
| **SEI viable** | ❌ No (incompatibilidad CI) | ✅ Sí (BRIM one-time charges) |
| **Configuración** | Adaptación forzada utilities | Nativo modelo gasineras |
| **Complejidad** | "Trucos" y workarounds | Diseñado para el caso de uso |
| **Modelo negocio** | Utilities (períodos) | Oil & Gas retail / Servicios |

**Conclusión:** Escenario 4 no es una variante de Escenario 2, sino una **arquitectura diferente** que merece análisis separado.

### 14.2. Arquitectura propuesta Escenario 4

**Opción 4A: RFNO + BRIM**

```
┌─────────────────────────────────────────────────┐
│ GAS ISU (actual)                                │
│ - Facturación Gas domiciliario (sin cambios)    │
│ - Contract Account ISU/FI-CA                    │
└─────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────┐
│ ELECTRICIDAD CI sobre ISU (actual)              │
│ - IBIS → VEMS → SAP CI                          │
│ - Contract Account ISU/FI-CA                    │
└─────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────┐
│ GNV/SEI RFNO + BRIM (NUEVO)                     │
│                                                  │
│ RFNO: Gestión operativa gasineras               │
│ - Inventario combustible estaciones             │
│ - Fleet card management (B2B)                   │
│ - Payment handling tarjetas (one-shot)          │
│ - POS integrado tiempo real                     │
│                                                  │
│ BRIM: Facturación flexible                      │
│ - Provider Contract (CI standalone)             │
│ - PROF items: SEI one-time charges ✅           │
│ - PROR items: GNV cíclico recurring ✅          │
│ - Generación XML UBL 2.1                        │
│ - Integración SERES                             │
│ - Gestión cobros integrada                      │
│                                                  │
│ Datos entrada: EVO desde GAIA                   │
└─────────────────────────────────────────────────┘

Todo en mismo S/4HANA, módulos coexistentes
```

**Ventajas arquitectura 4A:**
- ✅ SEI completamente viable (BRIM one-time charges nativos)
- ✅ GNV one-shot sin "trucos" (event-driven billing)
- ✅ RFNO diseñado para modelo negocio gasineras (no adaptación forzada)
- ✅ Independiente de ISU Gas/Electricidad (sin conflictos clientes, sin tocar configuración actual)
- ✅ Solución industria corporativa (RFNO Oil & Gas + BRIM servicios)

**Complejidad arquitectura 4A:**
- ⚠️ Tres mundos SAP coexistentes (ISU Gas, ISU+CI Electricidad, RFNO+BRIM GNV/SEI)
- ⚠️ Licensing adicional (RFNO + BRIM si no disponibles)
- ⚠️ Gestión clientes compartidos entre módulos (Gas/Electricidad/GNV cliente mismo)

---

**Opción 4B: IS-OIL Downstream completo**

```
┌─────────────────────────────────────────────────┐
│ IS-OIL DOWNSTREAM (NUEVO)                       │
│                                                  │
│ SSR (Service Station Retailing):                │
│ - Operaciones retail gasineras                  │
│ - Integración POS tiempo real                   │
│ - Billing fuel sales específico                 │
│                                                  │
│ Sales & Distribution Oil & Gas:                 │
│ - Pedidos, entregas, facturación B2B            │
│ - Formula & Average Pricing integrado           │
│                                                  │
│ Transportation & Distribution:                  │
│ - Logística productos refinados                 │
│ - Distribución secundaria (modelo GNV)          │
│                                                  │
│ Billing integrado:                              │
│ - Facturación cíclica + one-shot                │
│ - Generación XML UBL (a validar)                │
│ - Integración SERES (a desarrollar)             │
└─────────────────────────────────────────────────┘

Gas/Electricidad: Sin cambios (ISU actual)
```

**Ventajas arquitectura 4B:**
- ✅ Solución industria Oil & Gas end-to-end (SSR específico gasineras)
- ✅ Modelo negocio nativo (distribución secundaria, retail fuel)
- ✅ Si Endesa ya tiene IS-OIL: aprovechamiento infraestructura existente

**Complejidad arquitectura 4B:**
- ⚠️ IS-OIL es suite completa (mayor alcance que RFNO+BRIM)
- ⚠️ ¿Generación XML UBL en IS-OIL nativa o requiere desarrollo?
- ⚠️ Curva aprendizaje si Endesa no tiene IS-OIL actualmente

---

**Opción 4C: BRIM standalone (solo facturación)**

```
┌─────────────────────────────────────────────────┐
│ BRIM STANDALONE GNV/SEI (NUEVO)                 │
│                                                  │
│ Subscription Order Management (SOM):            │
│ - Provider Contract (sin ISU)                   │
│ - Billing Plan flexible                         │
│ - PROF/PROR/PROP items mix                      │
│                                                  │
│ Convergent Invoicing (CI standalone):           │
│ - Sin Contract Account ISU                      │
│ - Event-driven billing                          │
│ - One-shot + recurring sin restricciones        │
│                                                  │
│ Convergent Charging:                            │
│ - Rating real-time/batch                        │
│                                                  │
│ FI-CA independiente:                            │
│ - Cuentas clientes GNV/SEI                      │
│ - Gestión cobros integrada                      │
│                                                  │
│ Datos entrada: EVO desde GAIA                   │
│ Master data: Desde Podio/GAIA (a definir)       │
└─────────────────────────────────────────────────┘

Sin gestión operativa gasineras (solo facturación)
```

**Ventajas arquitectura 4C:**
- ✅ Menor complejidad que 4A/4B (solo billing, no operaciones)
- ✅ SEI/GNV one-shot completamente viables
- ✅ BRIM diseñado para servicios (modelo subscription + one-time natural)

**Limitaciones arquitectura 4C:**
- ❌ Sin gestión operativa gasineras (RFNO features perdidas)
- ⚠️ Requiere gestión master data separada (clientes/contratos GNV)

### 14.3. Preguntas estratégicas críticas para decidir Escenario 4

**BLOQUE 1: Viabilidad licensing y coste**

1. **¿Endesa tiene licencias RFNO, BRIM, IS-OIL en S/4HANA actual?** (si ya disponibles, cambia análisis coste)
2. **¿Coste licensing activar RFNO+BRIM vs mantener CI sobre ISU?** (inversión nueva vs workarounds)
3. **¿Esfuerzo implementación RFNO+BRIM vs desarrollos custom en CI actual?** (meses, años, recursos)
4. **¿Existe presupuesto aprobado para módulos SAP nuevos?** (o requiere business case)

**BLOQUE 2: Estrategia corporativa SAP**

5. **¿Visión Endesa largo plazo: consolidar en SAP o arquitectura distribuida?** (si consolidar → Escenario 4 prioritario)
6. **¿GNV/SEI es negocio estratégico de crecimiento?** (si sí → inversión sistema especializado justificada)
7. **¿Posibilidad expansión modelo gasineras otros países?** (si sí → solución corporativa RFNO escalable)
8. **¿Roadmap SAP Endesa incluye modernización módulos?** (ventana oportunidad añadir RFNO/BRIM)

**BLOQUE 3: Capacidad técnica y organizacional**

9. **¿Equipo SAP tiene capacidad absorber proyecto RFNO+BRIM?** (recursos, conocimiento, bandwidth)
10. **¿Experiencia interna Endesa con BRIM o IS-OIL en otros negocios?** (curva aprendizaje)
11. **¿Prioridad proyecto GNV/SEI vs otros proyectos SAP?** (puede bloquear por falta prioridad)
12. **¿Iliade (IBIS) puede/quiere integrarse con RFNO?** (si se elige opción con IBIS)

**BLOQUE 4: Comparativa con alternativas**

13. **¿Escenario 4 (RFNO+BRIM) vs Escenario 1 (E4E)?** ¿Ventajas justifican complejidad/coste?
14. **¿Escenario 4 vs Escenario 3 (Kintsugi)?** ¿Inversión SAP vs autonomía rápida?
15. **¿Arquitectura híbrida viable?** (GNV cíclico en CI sobre ISU, SEI en E4E/Kintsugi)
16. **¿Escenario 4 como solución definitiva o Escenario 3 como puente temporal?** (estrategia fases)

### 14.4. Criterio de decisión: ¿Explorar Escenario 4?

**EXPLORAR ESCENARIO 4 (análisis completo) si:**
- ✅ RFNO/BRIM/IS-OIL disponibles en S/4HANA actual (o licensing viable)
- ✅ GNV/SEI es negocio estratégico de crecimiento largo plazo
- ✅ SEI es producto crítico (incompatibilidad CI sobre ISU bloqueante)
- ✅ Visión corporativa consolidar facturación en SAP
- ✅ Presupuesto disponible para proyecto envergadura (meses, equipo, consultoría)
- ✅ Equipo SAP tiene capacidad y prioriza proyecto

**DESCARTAR ESCENARIO 4 si:**
- ❌ RFNO/BRIM no disponibles y licensing prohibitivo
- ❌ GNV/SEI es negocio marginal (no justifica inversión)
- ❌ SEI puede resolverse en Escenario 1 (E4E) o 3 (Kintsugi) aceptablemente
- ❌ Estrategia corporativa NO es consolidación SAP
- ❌ Presupuesto/recursos insuficientes
- ❌ Prioridad SAP baja (proyecto bloqueado en roadmap)

### 14.5. Próximos pasos si Escenario 4 viable

1. **Workshop SAP/IT:** Presentar hallazgos RFNO/BRIM/IS-OIL, validar disponibilidad módulos
2. **Estudio licensing:** Coste activación RFNO+BRIM, comparativa vs Escenarios 1/2/3
3. **POC técnico:** Validar generación XML UBL desde BRIM, integración SERES
4. **Análisis funcional completo Escenario 4:** Mismo nivel profundidad que Escenarios 1/2/3
5. **Matriz decisión final:** Comparativa 4 escenarios (E4E, SAP-ISU, Kintsugi, RFNO+BRIM)

### 14.6. Impacto en documento actual

**Escenario 2 (actual) queda como:**
- Análisis válido para GNV cíclico con CI sobre ISU
- SEI descartado en este escenario (incompatibilidad técnica CI sobre ISU)
- Base comparativa para entender limitaciones arquitectura actual

**Escenario 4 (potencial) sería:**
- Sistema especializado Oil & Gas / Servicios (RFNO+BRIM)
- Resuelve SEI + GNV cíclico + GNV one-shot en arquitectura nativa
- Requiere análisis completo separado si decisión estratégica es explorarlo

**Decisión necesaria:** ¿Mantenemos Escenarios 1/2/3 como opciones finales o abrimos estudio formal Escenario 4?

---

## NOTAS Y COMENTARIOS ADICIONALES

**Actualización arquitectura CI sobre ISU:**
- Sección 2.3 añadida explicando limitaciones técnicas CI sobre ISU y por qué SEI incompatible
- Sección 4 actualizada con hallazgos RFNO/BRIM/IS-OIL (módulos especializados existen)
- Sección 14 añadida abriendo debate Escenario 4 (sistema especializado)

**Próxima iteración:**
- Si decisión explorar Escenario 4: crear análisis completo con estructura Escenarios 1/2/3
- Si decisión descartar Escenario 4: actualizar matriz comparativa final 3 escenarios

[Espacio para notas adicionales durante desarrollo del análisis]

---
---
---

# ESCENARIO 3: KINTSUGI COMO GENERADOR XML - VISIÓN FUNCIONAL
## Facturación Electrónica GNV/SEI

---

## RESUMEN EJECUTIVO

### ¿Qué es este escenario?

Este escenario propone **mantener el proceso actual de facturación GNV/SEI sin cambios estructurales** y añadir capacidades a Kintsugi (hub actual Access/VBA) para que asuma la generación de XMLs UBL 2.1 y la comunicación con SERES como PDP.

**Cambio respecto a hoy:** Kintsugi pasa de ser únicamente un hub de transformación EVO → E4E + generación PDF, a incorporar dos funcionalidades nuevas: (1) generación de XML UBL 2.1 conforme a especificación SERES, y (2) comunicación bidireccional con plataforma SERES (envío XML + recepción estados). El resto del proceso permanece idéntico: Podio → GAIA → EVO → Kintsugi → E4E (registro fiscal) → PDF cliente.

**Flujo básico objetivo:** El proceso mantiene toda su cadena actual intacta. Kintsugi, tras recibir el fichero EVO desde GAIA, realiza tres outputs en paralelo: (1) envío a E4E para numeración fiscal (actual), (2) generación PDF (actual), y (3) generación + envío XML UBL a SERES (nuevo). Los estados de factura que SERES devuelve se almacenan en Kintsugi y se gestionan manualmente por el equipo de Operaciones para informar al proceso de Cobros.

**Ventaja diferencial:** Todos los datos necesarios para generar el XML UBL ya están disponibles en el fichero EVO que Kintsugi recibe actualmente, sin necesidad de enriquecer información desde otros sistemas.

### Ventajas principales

- **Impacto mínimo en arquitectura:** Proceso actual sin cambios, sin dependencias de otros departamentos (E4E, SAP, IT corporativo), sin necesidad de coordinación multi-equipo
- **Rapidez de implementación:** Alcance desarrollo acotado y controlado, sin homologaciones internas IT/Seguridad, solo homologación SERES necesaria, puesta en producción independiente
- **Autonomía funcional completa:** Desarrollo interno por equipo funcional (con Claude Code u otro soporte), control total sobre evoluciones y mantenimiento, sin SLA externos, flexibilidad para adaptaciones rápidas
- **Datos completos disponibles:** EVO ya contiene TODA la información necesaria para UBL 2.1, mapeo EVO → UBL relativamente directo, sin necesidad enriquecer desde otros sistemas
- **Coste contenido:** Sin licencias adicionales, sin desarrollos IT corporativo, sin consultorías externas, solo coste PDP SERES (común a todos escenarios)

### Limitaciones críticas

- **NO resuelve gestión cobros integrada:** Proceso cobros sigue siendo externo y manual, estados SERES no integrados automáticamente con sistema Cobros, equipo Operaciones debe informar manualmente a Cobros sobre rechazos, sin bloqueo automático cobro si factura rechazada
- **NO resuelve circuito automático estados SERES:** Recepción estados manual (polling) o semi-automática, decisiones sobre estados (reenvío, anulación) manuales, sin workflow automático gestión rechazos, requiere intervención continua Operaciones
- **Kintsugi como punto único de fallo crítico:** Access como plataforma no corporativa y sin alta disponibilidad, escalabilidad limitada (volumetría futura puede superar capacidad), dependencia conocimiento concentrado en equipo reducido, backups y continuidad negocio dependen proceso manual
- **Complejidad técnica desarrollo desconocida:** Generación XML en Access/VBA con viabilidad técnica a validar, librerías XML disponibles en VBA a investigar, validación XSD desde Access con complejidad desconocida, firma electrónica (si requerida) con factibilidad en VBA incierta, llamadas API REST desde Access posibles pero no estándar
- **Mantenibilidad largo plazo cuestionable:** Evoluciones esquema UBL requieren adaptación manual, cambios especificaciones SERES requieren desarrollo interno, soporte técnico basado solo en conocimiento interno equipo, documentación código crítica para continuidad
- **Sin integración proceso global:** Solución "parche" que perpetúa arquitectura fragmentada, no contribuye a modernización/consolidación sistemas, Kintsugi seguirá siendo necesario indefinidamente

### Riesgos bloqueantes

1. **Access/VBA no puede generar XML válido (criticidad CRÍTICA):** Si Access/VBA no puede generar XMLs conformes al esquema UBL 2.1 o validarlos contra XSD, el núcleo del escenario es inviable
2. **SERES exige firma electrónica compleja incompatible con VBA (criticidad ALTA):** Si SERES requiere firma electrónica avanzada que VBA no puede implementar, el escenario requiere componente externo o es inviable
3. **Volumetría futura supera capacidad Access (criticidad MEDIA-ALTA):** Si proyección crecimiento facturas GNV/SEI supera límites técnicos Access (2GB base datos, performance), solución tiene fecha caducidad próxima

### Criterio de decisión: ¿Profundizar o descartar?

**PROFUNDIZAR si:**
- Estudio técnico Access/VBA valida viabilidad generación XML (librerías disponibles, complejidad asumible)
- Rapidez implementación es crítica (obligación legal inminente, presión normativa)
- Autonomía funcional es valorada estratégicamente (vs dependencia IT corporativo)
- Gestión manual estados SERES es aceptable operativamente (equipo capacidad asumirlo)
- Escenario 3 aceptado como puente temporal hasta decisión estratégica futura (E4E o SAP)

**DESCARTAR si:**
- Access/VBA técnicamente inviable para XML (complejidad excesiva, librerías inexistentes)
- Integración cobros automática es requisito crítico inmediato (ventaja Escenarios 1 o 2)
- Solución largo plazo corporativa es necesaria desde inicio (no se acepta transitorio)
- Volumetría proyectada claramente supera capacidad Access a corto plazo
- Equipo Operaciones no tiene capacidad para asumir desarrollo/mantenimiento

---

## PREGUNTAS CLAVE PARA DIMENSIONAR ESFUERZO

### BLOQUE 1: Viabilidad organizacional

1. **¿Rapidez implementación es factor crítico?** ¿Existe obligación legal con plazo inminente que favorece solución rápida vs robusta?
2. **¿Autonomía funcional es prioritaria vs coordinación IT?** ¿Equipo Operaciones prefiere control total desarrollo aunque sea solución no corporativa?
3. **¿Equipo Operaciones dispuesto a asumir responsabilidad desarrollo y mantenimiento?** ¿Capacidad técnica y tiempo disponible?
4. **¿Presupuesto limitado favorece solución low-cost?** ¿Disponibilidad presupuesto para Escenarios 1 o 2 vs restricción actual?

### BLOQUE 2: Capacidad técnica Kintsugi/Access

5. **¿Access/VBA puede generar XML válido conforme UBL 2.1?** (crítico - viabilidad técnica núcleo escenario)
6. **¿Qué librerías XML están disponibles en VBA?** (MSXML 6.0, alternativas, capacidades de cada una)
7. **¿Validación automática contra esquema XSD desde VBA es posible?** ¿Complejidad implementación?
8. **¿Access puede consumir API REST para comunicar con SERES?** (objeto WinHTTP, alternativas)
9. **¿Firma electrónica XML desde VBA es factible?** (si SERES requiere - librerías crypto disponibles)
10. **¿Cuáles son las limitaciones volumetría Access?** (2GB límite base datos, performance queries, proyección crecimiento GNV/SEI)

### BLOQUE 3: Magnitud del GAP funcional

11. **¿EVO contiene TODOS los datos necesarios para generar UBL 2.1 completo?** (validación campo por campo vs glosario SERES)
12. **¿Complejidad mapeo EVO → UBL?** ¿Transformaciones simples (renombrar campos) o lógica compleja necesaria?
13. **¿Kintsugi tiene documentación código existente?** ¿Estado documentación? ¿Suficiente para continuidad?
14. **¿Cuántas personas en equipo Operaciones conocen Access/VBA?** ¿Nivel expertise? ¿Riesgo concentración conocimiento?
15. **¿Backups automáticos Kintsugi implementados actualmente?** ¿Frecuencia? ¿Proceso recuperación probado?

### BLOQUE 4: Dependencias críticas externas

16. **¿SERES ha publicado especificación técnica API definitiva?** (endpoint, autenticación, formatos request/response)
17. **¿Glosario campos obligatorios UBL 2.1 está definitivo y completo?** ¿O puede cambiar durante desarrollo?
18. **¿SERES requiere envío PDF además de XML?** ¿PDF adjunto al XML o comunicaciones separadas?
19. **¿Ambiente de pruebas SERES está disponible?** ¿Cuándo? ¿Acceso inmediato o proceso solicitud?
20. **¿Cuál es el proceso de homologación SERES?** ¿Casos prueba requeridos? ¿Plazo estimado validación?
21. **¿SLA respuesta SERES para estados factura?** (tiempo real, horario, diario - impacta diseño polling)

### BLOQUE 5: Gestión estados SERES y cobros

22. **¿Proceso cobros puede operar con gestión manual de estados?** ¿O integración automática es crítica?
23. **¿Qué frecuencia mínima actualización estados necesita departamento Cobros?** (tiempo real, diaria, semanal)
24. **¿Qué información específica de estados SERES necesita Cobros?** (solo ACEPTADA/RECHAZADA o detalles adicionales)
25. **¿Workflow factura RECHAZADA manual es operativamente viable?** (detección Kintsugi → corrección GAIA/Podio → reenvío)
26. **¿Workflow factura ACEPTADA manual es viable?** (export Excel → envío email Cobros → carga manual sistema Cobros)
27. **¿Quién corrige datos origen si factura rechazada por SERES?** ¿Proceso definido? ¿Responsable? ¿Plazo SLA interno?

### BLOQUE 6: Riesgos de plazo y coste

28. **¿Esfuerzo estimado desarrollo generación XML en Kintsugi?** (días, semanas - mapeo EVO→UBL + validación XSD)
29. **¿Esfuerzo desarrollo comunicación API SERES?** (envío XML + recepción estados + gestión errores)
30. **¿Esfuerzo desarrollo interface consulta/alertas estados?** (pantalla Access, export Excel, emails automáticos)
31. **¿Plazo global estimado proyecto?** (desde inicio desarrollo hasta producción - ¿semanas o meses?)
32. **¿Coste PDP SERES?** (tarifa mensual, por factura, setup inicial - común a todos escenarios)
33. **Si Access falla técnicamente, ¿alternativa Python/herramienta externa viable?** (script externo lee Access → genera XML)

### BLOQUE 7: Valor añadido del escenario

34. **¿Qué problemas actuales resuelve este escenario?** (cumplimiento normativo facturación electrónica Francia principalmente)
35. **¿Qué NO resuelve que sea crítico?** (cobros integrados, automatización completa estados, escalabilidad largo plazo)
36. **¿Escenario 3 como puente temporal es aceptable estratégicamente?** (hasta decisión E4E o SAP en 1-2 años)
37. **¿Experiencia real con UBL/SERES es útil para informar decisión futura?** (aprendizaje proceso, GAPs identificados, requisitos validados)
38. **¿Este escenario facilita evoluciones futuras?** ¿O complica migración posterior a E4E/SAP?

### BLOQUE 8: Comparativa con alternativas

39. **¿Por qué Kintsugi en lugar de E4E (Escenario 1)?** ¿Rapidez/autonomía más importante que robustez/integración cobros?
40. **¿Por qué Kintsugi en lugar de SAP (Escenario 2)?** ¿Simplicidad más importante que centralización corporativa?
41. **¿Visión largo plazo: Kintsugi solución definitiva o transitoria?** ¿Estrategia explícita o indefinida?
42. **¿Trigger migración futura está definido?** (volumetría límite, plazo temporal, decisión corporativa consolidación)

---

## ANÁLISIS DETALLADO

### 1. DESCRIPCIÓN FUNCIONAL

Mantener el proceso actual sin modificaciones estructurales. Kintsugi asume la responsabilidad adicional de generar XMLs UBL 2.1 y comunicarse con SERES para cumplir con la obligación de facturación electrónica.

**Alcance:**
- Proceso actual intacto (Podio → GAIA → EVO → Kintsugi → E4E → PDF)
- Kintsugi añade:
  - Generación XML UBL 2.1 desde datos EVO
  - Envío XML a SERES (API o FTP)
  - Recepción confirmación envío
- E4E mantiene registro fiscal (sin cambios)
- Gestión estados SERES manual o semi-automática
- Proceso cobros sin cambios (externo)

---

## 2. FLUJO FUNCIONAL OBJETIVO

```
Podio → GAIA → EVO → Kintsugi (genera XML) → SERES
                        ↓           ↓              ↓
                     E4E       PDF        Estados factura
                      ↓                          ↓
                 Num. fiscal              Gestión manual
                      ↓                          ↓
              Kintsugi (PDF final)      Sistema Cobros
                      ↓
                  Envío PDF
```

**Cambios respecto a proceso actual:**
1. Kintsugi genera XML UBL 2.1 además de PDF
2. Kintsugi envía XML a SERES (nuevo)
3. Kintsugi recibe/almacena estados SERES (nuevo)
4. Operaciones gestiona manualmente impacto estados en cobros

---

## 3. CAPACIDADES FUNCIONALES REQUERIDAS EN KINTSUGI

La generación XML y comunicación SERES en Kintsugi requiere desarrollar:

1. **Motor generación XML UBL 2.1:**
   - Mapeo datos EVO → estructura UBL
   - Validación conformidad esquema
   - Firma electrónica (si requerida)

2. **Módulo comunicación SERES:**
   - Envío XML (API REST o FTP)
   - Recepción estados factura
   - Gestión reintentos y errores

3. **Gestión estados:**
   - Almacenamiento estados por factura
   - Interface consulta/alertas
   - Export para sistema Cobros

**Ventaja:** Kintsugi ya dispone de TODOS los datos necesarios para UBL provenientes del EVO.

**Nota:** El detalle de viabilidad técnica será objeto del estudio técnico Access/VBA.

---

## 4. VENTAJAS ESCENARIO 3

### 4.1. Impacto mínimo
- Arquitectura existente sin cambios
- Sin dependencias otros departamentos (E4E, SAP, Cobros)
- Sin necesidad coordinación IT corporativo
- Aprendizaje equipo Operaciones mínimo (interfaz conocida)

### 4.2. Rapidez implementación
- Alcance desarrollo acotado y controlado
- Sin homologaciones internas (IT, Seguridad...)
- Solo homologación SERES necesaria
- Puesta en producción independiente

### 4.3. Autonomía
- Desarrollo interno: equipo funcional + Claude Code
- Control total sobre evoluciones
- Sin SLA externos para mantenimiento
- Flexibilidad adaptaciones rápidas

### 4.4. Datos completos disponibles
- EVO ya contiene TODA la información necesaria para UBL
- Sin necesidad enriquecer datos desde otros sistemas
- Mapeo EVO→UBL relativamente directo

### 4.5. Coste contenido
- Sin licencias adicionales
- Sin desarrollos IT externos
- Solo coste PDP SERES (común a todos escenarios)

---

## 5. LIMITACIONES ESCENARIO 3

### 5.1. NO resuelve gestión cobros
- Proceso cobros sigue siendo externo y manual
- Estados SERES no integrados automáticamente con sistema Cobros
- Operaciones debe informar manualmente a Cobros sobre rechazos
- Sin bloqueo automático cobro si factura rechazada

### 5.2. NO resuelve circuito automático estados SERES
- Recepción estados: manual (polling) o semi-automática
- Decisiones sobre estados (reenvío, anulación): manuales
- Sin workflow automático gestión rechazos
- Requiere intervención Operaciones

### 5.3. Kintsugi punto único de fallo crítico
- Access como plataforma no corporativa
- Escalabilidad limitada (volumetría futura)
- Dependencia conocimiento concentrado (equipo reducido)
- Backups y continuidad negocio dependen proceso manual
- Sin alta disponibilidad

### 5.4. Complejidad técnica desarrollo desconocida
- Generación XML en Access/VBA: viabilidad a validar
- Librerías XML disponibles en VBA: a investigar
- Validación XSD desde Access: complejidad desconocida
- Firma electrónica (si requerida): ¿factible en VBA?
- Llamadas API REST desde Access: posible pero no estándar

### 5.5. Mantenibilidad largo plazo
- Evoluciones esquema UBL: adaptación manual
- Cambios especificaciones SERES: desarrollo interno
- Soporte técnico: solo conocimiento interno equipo
- Documentación código: crítica para continuidad

### 5.6. Sin integración proceso global
- Solución "parche" que perpetúa arquitectura fragmentada
- No contribuye a modernización/consolidación sistemas
- Kintsugi seguirá siendo necesario indefinidamente

---

## 6. GAP FUNCIONAL KINTSUGI

| Capacidad requerida | ¿Kintsugi puede? | GAP |
|---|---|---|
| Generar XML UBL 2.1 | Desconocido | A estudiar técnicamente |
| Validar esquema XSD | Desconocido | A estudiar técnicamente |
| Comunicar API REST | Desconocido | A estudiar técnicamente |
| Firmar XML (si requiere) | Desconocido | A estudiar técnicamente |
| Almacenar estados SERES | Sí (tabla Access) | Bajo |
| Gestionar volumetría futura | Desconocido | Depende proyección |

---

## 7. INTEGRACIONES NECESARIAS

### 7.1. Salida: Kintsugi → SERES (envío XML)
- **Qué:** XML UBL 2.1 por factura
- **Protocolo:** API REST (preferido) o FTP
- **Frecuencia:** Por batch facturación
- **Autenticación:** Según SERES especifique

### 7.2. Entrada: SERES → Kintsugi (estados)
- **Qué:** Estados factura (ENTREGADA/ACEPTADA/RECHAZADA)
- **Protocolo:** Polling API o FTP
- **Frecuencia:** A definir (¿horaria? ¿diaria?)
- **Contenido:** ID factura, estado, fecha, motivo

### 7.3. Salida: Kintsugi → Cobros (manual)
- **Qué:** Listado facturas con estados
- **Protocolo:** Export Excel o email
- **Frecuencia:** Según necesidad Cobros
- **Contenido:** Número factura, cliente, importe, estado

---

## 8. DECISIONES FUNCIONALES PENDIENTES

### 8.1. Comunicación SERES
- ¿API REST o FTP? (SERES debe especificar recomendación)
- ¿Autenticación requerida? (certificado, OAuth, API key)
- ¿Envío factura individual o batch múltiples XMLs?

### 8.2. Recepción estados
- ¿Polling cada cuánto? (frecuencia consultas SERES)
- ¿Almacenamiento histórico estados o solo último?
- ¿Alertas automáticas si rechazo?

### 8.3. Gestión estados SERES

**Factura RECHAZADA:**
- ¿Anulación manual en E4E necesaria?
- ¿Reenvío automático tras corrección o manual?
- ¿Quién corrige datos origen (GAIA, Podio)?

**Factura ACEPTADA:**
- ¿Exportación automática listado para Cobros?
- ¿Frecuencia envío información a Cobros?

### 8.4. Generación documentos
- ¿SERES requiere envío PDF además de XML?
- Si no: ¿Kintsugi sigue generando PDF para envío cliente?
- Si sí: ¿PDF adjunto al XML o envío separado?

### 8.5. Continuidad
- ¿Backups automáticos Kintsugi implementados?
- ¿Documentación código Access existente?
- ¿Cuántas personas del equipo conocen Access/VBA?

---

## 9. DEPENDENCIAS CRÍTICAS PARA ESTUDIO

### Del proveedor SERES:
1. Glosario definitivo campos obligatorios UBL 2.1
2. Especificación técnica API o FTP
3. Estados factura que devuelve y códigos
4. Autenticación requerida
5. Proceso homologación y requisitos
6. SLA respuesta estados
7. ¿SERES requiere PDF adjunto o solo XML?

### Estudio técnico Kintsugi/Access:
8. ¿Access/VBA puede generar XML válido?
9. ¿Librerías XML disponibles en VBA? (MSXML, alternativas)
10. ¿Validación XSD desde VBA factible?
11. ¿Access puede consumir API REST?
12. ¿Firma electrónica XML desde VBA posible? (si SERES requiere)
13. ¿Limitaciones volumetría Access? (proyección crecimiento)

### Del departamento Cobros:
14. ¿Qué información estados SERES necesitan?
15. ¿Formato preferido recepción info?
16. ¿Frecuencia mínima actualización estados?

### Interno funcional:
17. ¿Quién corrige datos si factura rechazada? (flujo vuelta a GAIA/Podio)
18. ¿Volumen facturas GNV/SEI mensual actual y proyección?
19. ¿Kintsugi tiene backups automáticos?
20. ¿Documentación existente código Kintsugi?

---

## 10. RIESGOS FUNCIONALES

| Riesgo | Impacto funcional | Criticidad |
|---|---|---|
| Access/VBA no puede generar XML válido | Escenario inviable | Crítica |
| SERES exige firma electrónica compleja | Desarrollo VBA inviable | Alta |
| Volumetría futura supera capacidad Access | Límites plataforma | Media-Alta |
| Conocimiento VBA concentrado | Continuidad riesgo | Media |
| Estados SERES no procesables manualmente | Gestión cobros impactada | Media |
| Kintsugi fallo sin backup | Pérdida datos crítica | Alta |
| Homologación SERES rechaza solución | Escenario inviable | Media |

---

## 11. PREGUNTAS PARA ESTUDIOS TÉCNICOS

### Estudio viabilidad técnica Access/VBA:
- ¿Qué librería XML usar en VBA? (MSXML, alternativas)
- ¿Complejidad mapeo EVO → UBL 2.1?
- ¿Validación XSD automática desde VBA?
- ¿Objeto WinHTTP suficiente para API REST SERES?
- ¿Gestión autenticación OAuth/token desde VBA?
- ¿Firma XML desde VBA si SERES requiere?
- ¿Límite volumetría Access? (2GB base, performance)

### Estudio proceso gestión estados:
- Workflow factura RECHAZADA (detección → corrección → reenvío)
- Workflow factura ACEPTADA (detección → export → envío Cobros)
- ¿Alertas automáticas necesarias? ¿Cómo implementar?

### Estudio homologación SERES:
- ¿Ambiente pruebas disponible cuándo?
- ¿Casos prueba requeridos?
- ¿Plazo homologación estimado?

---

## 12. CRITERIOS ÉXITO ESCENARIO 3

### Técnicos:
- XML UBL 2.1 generado conforme esquema SERES (100% válidos)
- Homologación SERES aprobada
- Envío XML exitoso >95% casos
- Performance aceptable (<5 min generación batch mensual)

### Funcionales:
- Estados SERES recibidos y almacenados correctamente
- Workflow rechazo ejecutado sin incidencias
- Información Cobros entregada en tiempo
- Equipo Operaciones autónomo gestión

### Negocio:
- Cumplimiento normativa facturación electrónica Francia
- Sin impacto clientes
- Coste implementación contenido

---

## 13. PLAN CONTINGENCIA

### Si Access no puede generar XML UBL:
- **Alternativa A:** Desarrollo Python/herramienta externa que lee Access, genera XML
- **Alternativa B:** Migración urgente a Escenario 1 o 2
- **Alternativa C:** Subcontratación desarrollo XML a proveedor externo

### Si SERES rechaza homologación:
- Análisis motivos rechazo
- Corrección según feedback SERES
- Si irresoluble: pivote a Escenario 1 o 2

### Si volumetría supera capacidad Access:
- Optimización código (batch procesamiento)
- Migración base Access a SQL Server (backend)
- Si insuficiente: migración Escenario 1 o 2

---

## 14. VISIÓN LARGO PLAZO

**Escenario 3 como solución transitoria:**

Este escenario puede verse como puente hacia una solución más robusta:
- Cumple obligación legal facturación electrónica a corto plazo
- Permite tiempo para estudiar y decidir entre Escenario 1 (E4E) o 2 (SAP)
- Genera experiencia real con UBL y SERES que informa decisión futura
- Desarrollo autónomo mantiene operación sin dependencias hasta decisión estratégica

**Trigger migración futura:**
- Volumetría supera capacidad Access
- Equipo no puede mantener complejidad
- Necesidad integración cobros se vuelve crítica
- Decisión estratégica consolidación sistemas

---

## NOTAS Y COMENTARIOS ADICIONALES

[Espacio para añadir notas durante el desarrollo del análisis]
