# Registro de Estudios y Análisis

Visión global de todos los análisis funcionales realizados o en curso.

## Estudios

| # | Nombre | Estado | Archivo | Inicio | Última actualización |
|---|--------|--------|---------|--------|---------------------|
| 1 | Facturación electrónica GNV/SEI — Análisis 4 escenarios + Matriz decisión | **En curso** | [`proyecto_facturacion_electronica.md`](proyecto_facturacion_electronica.md) | 2025 | 18 Feb 2026 |

## Estados posibles

- **En curso** — Análisis activo, con decisiones pendientes
- **En espera** — Análisis pausado, pendiente de inputs externos
- **Completado** — Análisis finalizado con conclusiones/decisión
- **Archivado** — Análisis cerrado sin continuidad

---

## Detalle Estudio #1: Facturación Electrónica GNV/SEI

### Estado actual (18 feb 2026)

| | |
|---|---|
| **Plazo normativo** | **Septiembre 2026** — ~7 meses. Urgencia confirmada. |
| **Postura recomendada** | Avanzar Escenario 3 (Kintsugi/MySQL+Python) como solución puente para sep 2026; en paralelo, visibilizar Escenario 4 a dirección como objetivo SAP definitivo |
| **Prerequisitos bloqueantes** | (1) Spec técnica SERES incompleta → reunión SERES urgente; (2) Proceso Cobros GNV/SEI sin definir → kick-off Cobros; (3) Firma electrónica SERES sin confirmar |
| **Escenario 1 — E4E** | 🔴 En espera — congelado hasta abril; posición E4E pendiente |
| **Escenario 2 — SAP-ISU** | 🟡 Condicional — viable solo GNV; SEI incompatible por arquitectura |
| **Escenario 3 — Kintsugi** | 🟢 Viable como transitorio — opción más rápida para sep 2026 |
| **Escenario 4 — SAP BRIM/RFNO** | ⚪ Concepto a visibilizar — pendiente validación licencias DSI |

---

### Objetivo

Analizar escenarios para implementar facturación electrónica GNV/SEI cumpliendo normativa francesa:
- Generación XML UBL 2.1 conforme especificación SERES
- Comunicación bidireccional con plataforma SERES (PDP - Plataforma de Desmaterialización Partner)
- Gestión estados factura (ENTREGADA/ACEPTADA/RECHAZADA)
- Integración proceso cobros (idealmente)

### Productos en alcance

- **GNV (Gas Natural Vehicular) — dos flujos distintos:**
  - **GNV cíclico:** Abonados con facturación mensual/bimestral regular → factura emitida → en alcance e-invoicing
  - **GNV ventas tarjeta:** Ventas directas en gasinera con pago por tarjeta bancaria → actualmente solo apunte contable del total en E4E (conciliación bancaria, sin factura emitida) → **alcance normativo pendiente aclarar:** ¿caen bajo e-reporting DGFiP? Si sí, amplía el alcance del proyecto
- **SEI (Servicios):**
  - Facturas esporádicas sin periodicidad (instalación, mantenimiento, otros servicios) → factura emitida → en alcance e-invoicing

### Escenarios analizados

**Matriz de decisión ejecutiva comparando 4 escenarios disponible al inicio del documento.**

#### **Escenario 1: Adaptar E4E**
- **Arquitectura:** Ampliar E4E (registro fiscal actual) para generación XML + comunicación SERES
- **Productos:** ✅ GNV cíclico, ✅ SEI | GNV ventas tarjeta: sin cambio previsto (pendiente aclaración e-reporting)
- **Ventajas:** Infraestructura existente, integración cobros (a validar), sistema corporativo
- **Limitaciones:** Dependencia departamento E4E (apertura, viabilidad técnica), GAP funcional alto (MDG, XML, SERES)
- **Riesgo bloqueante:** E4E rechaza proyecto o plataforma técnica inviable para XML
- **Estado análisis:** ✅ Completo (Resumen Ejecutivo + 34 preguntas dimensionadoras + Análisis Detallado)

#### **Escenario 2: SAP-ISU (CI sobre ISU actual)** ⚠️
- **Arquitectura:** Convergent Invoicing instalado sobre SAP-ISU existente (configuración actual Electricidad)
- **Productos:** ✅ GNV cíclico, ❌ **SEI incompatible** | GNV ventas tarjeta: sin cambio previsto (pendiente aclaración e-reporting)
- **HALLAZGO CRÍTICO:** CI sobre ISU hereda restricciones periodicidad de ISU (billing cycle obligatorio). SEI requiere facturas esporádicas sin patrón → **arquitectónicamente incompatible**.
- **Ventajas:** Cobros integrados SAP FI-CA, sistema corporativo robusto, experiencia SAP Electricidad
- **Limitaciones:** SEI inviable, configuración "tramposa" (forzar utilities a gasineras), complejidad alta, dependencia IBIS/Iliade
- **Riesgo bloqueante:** Inversión en arquitectura equivocada (repetir error intento previo ISU gasineras)
- **Recomendación:** ⚠️ **NO RECOMENDADO** - Si SEI crítico o inversión SAP largo plazo → Explorar Escenario 4 con módulos especializados
- **Estado análisis:** ✅ Completo (Resumen Ejecutivo + Sección 2.3 arquitectura CI/ISU + 38 preguntas + Análisis Detallado + Sección 14 hacia Escenario 4)

#### **Escenario 3: Kintsugi (Access/VBA)**
- **Arquitectura:** Mantener proceso actual, Kintsugi añade generación XML + comunicación SERES (MySQL+Python como stack real)
- **Productos:** ✅ GNV cíclico, ✅ SEI | GNV ventas tarjeta: sin cambio previsto (pendiente aclaración e-reporting)
- **Ventajas:** Impacto mínimo, rapidez implementación, autonomía funcional completa, datos completos en EVO, coste bajo
- **Limitaciones:** NO resuelve cobros integrados, gestión estados SERES manual, Access punto único fallo, escalabilidad limitada (2GB), mantenibilidad largo plazo
- **Riesgo bloqueante:** Complejidad UBL 2.1 subestimada sin soporte técnico externo; proceso Cobros sin definir (domiciliado hace rechazos críticos); dependencia en 2 personas sin cobertura formal
- **Recomendación:** Válido como **puente temporal** si rapidez crítica o como solución definitiva si autonomía prioritaria y cobros manuales aceptables
- **Estado análisis:** ✅ Completo (Resumen Ejecutivo + 42 preguntas dimensionadoras + Análisis Detallado)

#### **Escenario 4: Sistema Especializado SAP (RFNO/BRIM/IS-OIL)** 🆕
- **Arquitectura:** Módulos SAP especializados Oil & Gas / Servicios, independiente de ISU Gas/Electricidad
- **Opciones arquitectura:**
  - 4A: RFNO (Retail Fuel Network Operations) + BRIM (Billing Revenue Innovation Management)
  - 4B: IS-OIL Downstream completo con SSR (Service Station Retailing)
  - 4C: BRIM standalone (solo facturación, sin operaciones gasineras)
- **Productos:** ✅ GNV cíclico, ✅ SEI (BRIM nativo) | GNV ventas tarjeta: sin cambio previsto (pendiente aclaración e-reporting)
- **Ventajas:** Solución definitiva corporativa, SEI viable (BRIM Provider Contract sin restricciones ISU), RFNO diseñado para gasineras (no configuración tramposa), cobros integrados SAP, escalabilidad alta
- **Limitaciones:** Coste licensing alto (RFNO+BRIM), plazo implementación largo (año), complejidad tres mundos SAP coexistentes
- **Riesgo bloqueante:** Licensing prohibitivo, equipo SAP sin capacidad, prioridad roadmap baja
- **Recomendación:** **Solución óptima si SAP estratégico + SEI crítico + presupuesto disponible**
- **Estado análisis:** 🔄 **Placeholder estructurado completo** — misma estructura que Esc 1/2/3 (qué es, ventajas hipotéticas, alertas, resumen señales, criterio de decisión, 5 preguntas a DSI). No explorado con DSI — objetivo es incluirlo en mapa de decisión ejecutivo antes de comprometer inversión en Escenario 2.

### Hallazgos técnicos clave

#### **Arquitectura CI sobre ISU (Escenario 2 - crítico)**

**Flujo técnico identificado:**
```
IBIS genera VEMS → VEMS entra como billing stream en CI →
Contract Account (FI-CA) define billing cycle obligatorio →
CI consolida streams según billing cycle →
ISU invoicing procesa factura final
```

**Implicación:** CI sobre ISU **NO controla calendario facturación**, solo consolida streams. El Contract Account ISU/FI-CA impone billing cycle periódico (mensual, bimestral...) diseñado para utilities.

**Consecuencia GNV/SEI:**
- ✅ **Electricidad funciona:** IBIS genera VEMS mensualmente → billing cycle mensual regular
- ✅ **GNV cíclico funciona:** Billing cycle mensual/bimestral aplicable
- ⚠️ **GNV one-shot:** Requiere billing plan items one-time (no natural, "truco")
- ❌ **SEI incompatible:** Facturas esporádicas sin patrón no tienen billing cycle aplicable

**Solución identificada:** BRIM (Billing and Revenue Innovation Management) permite **CI standalone** con Provider Contract (sin Contract Account ISU), soportando one-time charges nativamente → Escenario 4.

#### **Módulos SAP especializados descubiertos**

Investigación reveló **3 módulos SAP específicos** para gasineras/servicios que resuelven limitaciones ISU:

1. **SAP RFNO (Retail Fuel Network Operations)** - S/4HANA módulo gasineras
   - Diseñado para redes estaciones servicio (COCO, CODO, DODO)
   - Gestión inventario combustible, fleet cards, payment handling, POS integrado
   - **Ventaja vs ISU:** Nativo modelo negocio gasineras (no configuración tramposa)

2. **SAP IS-OIL Downstream con SSR (Service Station Retailing)**
   - Solución Oil & Gas específica downstream (refinación, distribución, retail)
   - SSR para operaciones retail gasineras, billing fuel sales

3. **SAP BRIM (Billing and Revenue Innovation Management)** ⭐ Crítico para SEI
   - Suite facturación compleja (subscription, one-time, usage-based)
   - Provider Contract (CI standalone sin restricciones Contract Account ISU)
   - **Resuelve incompatibilidad SEI:** One-time charges nativos (PROF items)

**Impacto:** Si inversión en SAP es estratégica, debe ser con módulos especializados (RFNO/BRIM), no forzando CI sobre ISU.

### Recomendaciones por contexto

**Si SEI producto crítico + presupuesto disponible:**
→ **ESCENARIO 4** (Sistema especializado RFNO+BRIM)
- Único que resuelve GNV+SEI completos sin configuraciones tramposas
- Requiere validar licensing RFNO/BRIM disponible en S/4HANA Endesa

**Si rapidez crítica + autonomía valorada:**
→ **ESCENARIO 3** (Kintsugi)
- Implementación más rápida (semanas-meses)
- Sin dependencias IT/E4E
- Válido como puente temporal hasta decisión estratégica

**Si E4E estratégico + gestión cobros integrada crítica:**
→ **ESCENARIO 1** (E4E)
- Requiere validar E4E acepta proyecto y viabilidad técnica generación XML
- Resuelve GNV+SEI completos con integración cobros

**EVITAR Escenario 2 (SAP-ISU) si:**
- ❌ SEI es producto crítico (incompatible arquitectónicamente)
- ❌ Inversión SAP como solución largo plazo (usar Escenario 4, no forzar ISU)
- ❌ Experiencia previa ISU gasineras descartada (no repetir mismo error)

### Decisiones pendientes críticas

#### **Decisión estratégica #1: ¿Explorar Escenario 4?**

**Pregunta inmediata para SAP/IT:**
- ¿Endesa tiene licencias RFNO y/o BRIM en S/4HANA actual?
- Si NO: ¿Presupuesto disponible para licensing?

**Impacto decisión:**
- SI licensing viable → Análisis completo Escenario 4 (mismo nivel detalle Esc 1/2/3)
- NO licensing viable → Escenarios 1 o 3 (E4E o Kintsugi)

#### **Decisión estratégica #2: Prioridad SEI**

**Pregunta para dirección:**
- ¿SEI es producto crítico o marginal?

**Impacto decisión:**
- SEI crítico → Descarta Escenario 2, prioriza Escenarios 1/3/4
- SEI marginal → Opción híbrida viable (GNV en SAP, SEI en E4E/Kintsugi)

#### **Decisión táctica #3: Rapidez vs Robustez**

**Contexto:**
- Plazo normativo **confirmado: septiembre 2026** (~7 meses desde feb 2026) — urgencia real

**Impacto decisión:**
- → **Escenario 3 (Kintsugi) como solución puente para sep 2026** — opción más rápida; Escenarios 1/4 no tienen tiempo hábil
- → Escenario 4 como objetivo SAP a largo plazo, en paralelo con la solución puente

### Próximos pasos

#### **Inmediato — prerequisitos que desbloquean todos los escenarios**

1. **Reunión SERES (urgente):** Obtener spec técnica energía + documentación API + confirmar firma electrónica (¿XMLDSig o solo autenticación FTP?) — responsable: SERES
2. **Kick-off Cobros:** Definir workflow gestión estados SERES para GNV/SEI domiciliado (rechazos/aceptaciones/corrección/reenvío) — responsable: Cobros
3. **Pregunta DSI sobre licencias BRIM/RFNO:** ¿S/4HANA actual incluye BRIM/RFNO? ¿Experiencia interna? — responsable: DSI

#### **Escenario 3 — avanzar en paralelo (objetivo sep 2026)**

4. Prototipo generador XML UBL 2.1 (Python leyendo MySQL) — test de viabilidad técnica más directo
5. Formalizar con dirección: cobertura 2 personas clave + horizonte temporal + trigger de migración

#### **Escenario 4 — visibilizar a dirección**

6. Presentar concepto BRIM/RFNO a dirección antes de comprometer inversión en Escenario 2 (CI sobre ISU)
7. Si DSI confirma licencias disponibles → profundizar análisis Escenario 4

#### **Escenario 1 — en espera hasta abril**

8. Obtener valoración formal E4E tras presión del liderazgo (no solo "lo estudiaremos")

### Documentación generada

Estructura actual de `proyecto_facturacion_electronica.md` (restructuración 18 feb 2026):

- **Header:** Plazo normativo sep 2026 visible desde la primera línea
- **§1 Cuadro de mando ejecutivo:** 4 escenarios con semáforo + postura actual + prerequisitos bloqueantes + postura recomendada
- **§2 Contexto:** Obligación normativa + deadline sep 2026
- **§3 GNV y SEI: Dos universos distintos:** Tabla cobertura por escenario
- **§4 Prerequisitos de decisión:** 4 incógnitas transversales con Responsable acción (SERES/Cobros/DSI)
- **§5 Matriz comparativa:** Hallazgos reales por criterio × escenario (fila "Compatibilidad sep 2026" añadida)
- **Escenario 1 (E4E):** Qué es / Ventajas / Limitaciones / 5 hallazgos (Pregunta→Respuesta→Análisis→Implicación) / Señales / Criterio de decisión / Próximos pasos
- **Escenario 2 (SAP-ISU):** Misma estructura
- **Escenario 3 (Kintsugi):** Misma estructura
- **Escenario 4 (BRIM/RFNO):** Placeholder completo — misma estructura con todas las señales "Pendiente de validación" y 5 preguntas concretas a DSI

### Actualizaciones principales

- **2026-02-14:** Hallazgo crítico arquitectura CI sobre ISU (incompatibilidad SEI), actualización Resumen Ejecutivo Escenario 2, descubrimiento módulos especializados SAP (RFNO/BRIM/IS-OIL), propuesta Escenario 4, creación matriz de decisión ejecutiva
- **2026-02-18 (2):** Matiz GNV ventas tarjeta — distinción entre GNV cíclico (factura emitida, en alcance e-invoicing) y ventas directas en gasinera con tarjeta bancaria (apunte contable E4E, sin factura emitida); duda abierta sobre obligación e-reporting DGFiP; "GNV one-shot" retirado como concepto (era impreciso)
- **2026-02-18:** Reestructuración completa del documento — plazo normativo sep 2026 formalizado; nuevo Cuadro de mando ejecutivo con semáforos y postura recomendada; "Incógnitas transversales" elevadas a "Prerequisitos de decisión" con responsables; Escenario 4 pasa de referencia en Escenario 2 a sección independiente con estructura completa; jerarquía de headings corregida; postura recomendada actual definida (Esc 3 como puente + Esc 4 como objetivo estratégico)
