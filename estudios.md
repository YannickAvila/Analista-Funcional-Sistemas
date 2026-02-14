# Registro de Estudios y Análisis

Visión global de todos los análisis funcionales realizados o en curso.

## Estudios

| # | Nombre | Estado | Archivo | Inicio | Última actualización |
|---|--------|--------|---------|--------|---------------------|
| 1 | Facturación electrónica GNV/SEI — Análisis 4 escenarios + Matriz decisión | **En curso** | [`proyecto_facturacion_electronica.md`](proyecto_facturacion_electronica.md) | 2025 | Feb 2026 |

## Estados posibles

- **En curso** — Análisis activo, con decisiones pendientes
- **En espera** — Análisis pausado, pendiente de inputs externos
- **Completado** — Análisis finalizado con conclusiones/decisión
- **Archivado** — Análisis cerrado sin continuidad

---

## Detalle Estudio #1: Facturación Electrónica GNV/SEI

### Objetivo

Analizar escenarios para implementar facturación electrónica GNV/SEI cumpliendo normativa francesa:
- Generación XML UBL 2.1 conforme especificación SERES
- Comunicación bidireccional con plataforma SERES (PDP - Plataforma de Desmaterialización Partner)
- Gestión estados factura (ENTREGADA/ACEPTADA/RECHAZADA)
- Integración proceso cobros (idealmente)

### Productos en alcance

- **GNV (Gas Natural Vehicular):**
  - GNV cíclico: Abonados con facturación mensual/bimestral regular
  - GNV one-shot: Clientes pago tarjeta (eventos irregulares)
- **SEI (Servicios):**
  - Facturas esporádicas sin periodicidad (instalación, mantenimiento, otros servicios)

### Escenarios analizados

**Matriz de decisión ejecutiva comparando 4 escenarios disponible al inicio del documento.**

#### **Escenario 1: Adaptar E4E**
- **Arquitectura:** Ampliar E4E (registro fiscal actual) para generación XML + comunicación SERES
- **Productos:** ✅ GNV cíclico, ✅ GNV one-shot, ✅ SEI
- **Ventajas:** Infraestructura existente, integración cobros (a validar), sistema corporativo
- **Limitaciones:** Dependencia departamento E4E (apertura, viabilidad técnica), GAP funcional alto (MDG, XML, SERES)
- **Riesgo bloqueante:** E4E rechaza proyecto o plataforma técnica inviable para XML
- **Estado análisis:** ✅ Completo (Resumen Ejecutivo + 34 preguntas dimensionadoras + Análisis Detallado)

#### **Escenario 2: SAP-ISU (CI sobre ISU actual)** ⚠️
- **Arquitectura:** Convergent Invoicing instalado sobre SAP-ISU existente (configuración actual Electricidad)
- **Productos:** ✅ GNV cíclico, ⚠️ GNV one-shot (requiere "trucos"), ❌ **SEI incompatible**
- **HALLAZGO CRÍTICO:** CI sobre ISU hereda restricciones periodicidad de ISU (billing cycle obligatorio). SEI requiere facturas esporádicas sin patrón → **arquitectónicamente incompatible**.
- **Ventajas:** Cobros integrados SAP FI-CA, sistema corporativo robusto, experiencia SAP Electricidad
- **Limitaciones:** SEI inviable, configuración "tramposa" (forzar utilities a gasineras), complejidad alta, dependencia IBIS/Iliade
- **Riesgo bloqueante:** Inversión en arquitectura equivocada (repetir error intento previo ISU gasineras)
- **Recomendación:** ⚠️ **NO RECOMENDADO** - Si SEI crítico o inversión SAP largo plazo → Explorar Escenario 4 con módulos especializados
- **Estado análisis:** ✅ Completo (Resumen Ejecutivo + Sección 2.3 arquitectura CI/ISU + 38 preguntas + Análisis Detallado + Sección 14 hacia Escenario 4)

#### **Escenario 3: Kintsugi (Access/VBA)**
- **Arquitectura:** Mantener proceso actual, Kintsugi añade generación XML + comunicación SERES
- **Productos:** ✅ GNV cíclico, ✅ GNV one-shot, ✅ SEI
- **Ventajas:** Impacto mínimo, rapidez implementación, autonomía funcional completa, datos completos en EVO, coste bajo
- **Limitaciones:** NO resuelve cobros integrados, gestión estados SERES manual, Access punto único fallo, escalabilidad limitada (2GB), mantenibilidad largo plazo
- **Riesgo bloqueante:** Access/VBA no puede generar XML válido, volumetría futura supera capacidad Access
- **Recomendación:** Válido como **puente temporal** si rapidez crítica o como solución definitiva si autonomía prioritaria y cobros manuales aceptables
- **Estado análisis:** ✅ Completo (Resumen Ejecutivo + 42 preguntas dimensionadoras + Análisis Detallado)

#### **Escenario 4: Sistema Especializado SAP (RFNO/BRIM/IS-OIL)** 🆕
- **Arquitectura:** Módulos SAP especializados Oil & Gas / Servicios, independiente de ISU Gas/Electricidad
- **Opciones arquitectura:**
  - 4A: RFNO (Retail Fuel Network Operations) + BRIM (Billing Revenue Innovation Management)
  - 4B: IS-OIL Downstream completo con SSR (Service Station Retailing)
  - 4C: BRIM standalone (solo facturación, sin operaciones gasineras)
- **Productos:** ✅ GNV cíclico, ✅ GNV one-shot, ✅ SEI (BRIM soporta one-time charges nativamente)
- **Ventajas:** Solución definitiva corporativa, SEI viable (BRIM Provider Contract sin restricciones ISU), RFNO diseñado para gasineras (no configuración tramposa), cobros integrados SAP, escalabilidad alta
- **Limitaciones:** Coste licensing alto (RFNO+BRIM), plazo implementación largo (año), complejidad tres mundos SAP coexistentes
- **Riesgo bloqueante:** Licensing prohibitivo, equipo SAP sin capacidad, prioridad roadmap baja
- **Recomendación:** **Solución óptima si SAP estratégico + SEI crítico + presupuesto disponible**
- **Estado análisis:** 🔄 **Debate estratégico abierto** - Sección 14 (Escenario 2) propone arquitectura, preguntas críticas, criterios decisión. Pendiente análisis completo si decisión explorar.

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
- ¿Obligación legal facturación electrónica tiene plazo inminente?

**Impacto decisión:**
- Plazo inminente → Escenario 3 (Kintsugi) como solución rápida, luego migrar
- Sin urgencia → Escenarios 1/4 como soluciones definitivas

### Próximos pasos

#### **Inmediato (próximas 2 semanas)**

1. **Workshop SAP/IT:** Validar disponibilidad RFNO/BRIM en S/4HANA Endesa
2. **Decisión dirección:** Prioridad SEI (crítico vs marginal)
3. **Decisión dirección:** Presupuesto disponible (licensing SAP vs solución departamental)

#### **Si decisión Escenario 1 (E4E)**

4. Workshop departamento E4E (apertura proyecto, viabilidad técnica plataforma)
5. Estudio técnico E4E (capacidad generación XML, librerías disponibles)
6. Identificación sistema Cobros actual (viabilidad integración)

#### **Si decisión Escenario 3 (Kintsugi)**

4. POC técnico Access/VBA (generación XML UBL, validación XSD)
5. Estudio librerías XML disponibles VBA (MSXML 6.0)
6. Definir workflow gestión manual estados SERES

#### **Si decisión Escenario 4 (Especializado)**

4. Estudio licensing RFNO+BRIM (coste, plazo activación)
5. POC técnico BRIM (generación XML UBL, integración SERES)
6. Análisis funcional completo Escenario 4 (estructura similar Esc 1/2/3)
7. Decisión arquitectura (4A: RFNO+BRIM, 4B: IS-OIL, 4C: BRIM standalone)

#### **Común a todos los escenarios**

8. Estudio especificación técnica SERES (glosario UBL 2.1, API/FTP, ambiente pruebas)
9. Análisis GAP datos EVO vs campos obligatorios UBL
10. Identificación sistema Cobros actual (para Escenarios 1/4 con integración)

### Documentación generada

- **Matriz de decisión ejecutiva:** Comparativa 4 escenarios en 19 criterios (inicio documento)
- **Escenario 1:** Resumen ejecutivo + 34 preguntas dimensionadoras + Análisis detallado completo
- **Escenario 2:** Resumen ejecutivo (actualizado con limitaciones) + Sección 2.3 arquitectura CI/ISU + Sección 4 módulos especializados + Sección 14 hacia Escenario 4 + 38 preguntas + Análisis detallado completo
- **Escenario 3:** Resumen ejecutivo + 42 preguntas dimensionadoras + Análisis detallado completo
- **Escenario 4:** Sección 14 (propuesta arquitectura, preguntas críticas, criterios decisión) - Pendiente análisis completo si decisión explorar

**Total preguntas dimensionadoras:** 114 (34+38+42) para estimar esfuerzo antes de comprometerse.

### Actualizaciones principales

- **2026-02-14:** Hallazgo crítico arquitectura CI sobre ISU (incompatibilidad SEI), actualización Resumen Ejecutivo Escenario 2, descubrimiento módulos especializados SAP (RFNO/BRIM/IS-OIL), propuesta Escenario 4, creación matriz de decisión ejecutiva
