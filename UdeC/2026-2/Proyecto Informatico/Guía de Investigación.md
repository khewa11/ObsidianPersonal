---
tags:
  - proyecto-informatico
  - metodologia-investigacion
  - estado-del-arte
  - literatura-cientifica
  - biobio
  - conectividad-rural
date: 2026-10-05
type: guia-investigacion
---
Soluciones Propuestas
> [[Soluciones Propuestas 1]] y [[Soluciones Propuestas 2 y 3]]

#  Literatura Científica y Evidencia Sectorial

> [!abstract] Propósito Metodológico
> Esta guía sistematiza las fuentes de información y ecuaciones de búsqueda requeridas para respaldar los entregables **E1 (Caso del problema)** y **E4 (Informe final - Capítulos 2 y 4)** del proyecto[cite: 7, 8]. Cumple con la **Proposición 1** (acreditar la magnitud con fuentes verificables) y la **Proposición 3** (sustentar el estado del arte y las ciencias aplicadas de la solución)[cite: 2, 5].

---

## 1. Literatura Científica (Estado del Arte y Ciencias Aplicadas)

### Bases de Datos y Congresos Clave
* **Repositorios académicos:** IEEE Xplore, ACM Digital Library, ScienceDirect (Elsevier) y Google Scholar.
* **Revistas y conferencias del área:** *ACM DEV* (ICT for Development), *IEEE Global Humanitarian Technology Conference (GHTC)*, *IEEE Transactions on Mobile Computing* y *Ad Hoc Networks*.

### Ecuaciones de Búsqueda Booleanas por Solución

| Solución Técnica | Ecuación de Búsqueda Recomendada (Google Scholar / IEEE) | Enfoque Teórico / Ciencias Aplicadas |
| :--- | :--- | :--- |
| **Redes Mesh P2P / BLE** | `("mesh network" OR "opportunistic network") AND ("BLE" OR "Wi-Fi Direct") AND ("emergency" OR "disaster") AND ("epidemic routing" OR "DTN")` | Enrutamiento en grafos dinámicos, difusión epidémica (*Gossip*) y criptografía asimétrica[cite: 5, 17]. |
| **Telemetría LoRa LPWAN** | `("LoRa" OR "LoRaWAN") AND ("rural connectivity" OR "emergency messaging") AND ("Huffman" OR "payload compression")` | Compresión Huffman de paquetes (<50 bytes) y presupuesto de enlace de RF (*Link Budget*)[cite: 5, 17]. |
| **Sincronización Offline-First** | `("CRDT" OR "Conflict-free Replicated Data Types") AND ("offline-first" OR "disconnected operation") AND ("mobile synchronization" OR "eventual consistency")` | Estructuras de datos CRDT (delta-mutación) y consistencia eventual fuerte (*SEC*)[cite: 5, 13]. |
| **Priorización Dinámica (VRP)** | `("Dynamic VRP" OR "vehicle routing problem") AND ("emergency response" OR "ambulance dispatch") AND ("latency" OR "delayed triage")` | Programación lineal entera mixta (MILP), metaheurísticas y despacho estocástico[cite: 5, 17]. |
| **Open-Core SDR / Local Breakout** | `("software-defined radio" OR "SDR") AND ("open-source cellular" OR "Open5GS" OR "Osmocom") AND ("disaster" OR "local breakout" OR "rural")` | Teoría de colas de tráfico telefónico (Erlang-B / Erlang-C) y conmutación SIP/SDP. |
| **Planificación Topográfica (GIS+ITM)** | `("Longley-Rice" OR "Irregular Terrain Model") AND ("facility location problem" OR "antenna placement") AND ("rural wireless mesh")` | Modelamiento ITM de propagación electromagnética y optimización combinatoria de cobertura[cite: 5]. |

> [!tip] Criterio de Selección Académica
> Priorizar *papers* de los últimos 5 años para el estado del arte y citar los artículos seminales que introdujeron las teorías formales base (ej. Shapiro et al. para CRDTs; Longley-Rice para propagación sobre terreno)[cite: 5].

---

## 2. Evidencia Sectorial y Magnitud del Problema (Chile y Biobío)

### A. Organismos Públicos y Datos Verificables
* **SUBTEL (Subsecretaría de Telecomunicaciones - `subtel.gob.cl`):**
  * *Series Estadísticas Trimestrales:* Reclamos por interrupción de servicio e indicadores comunales de brecha de conectividad.
  * *Normativa Técnica de Respaldo Crítico:* Resoluciones exentas sobre exigencias de autonomía y bancos de baterías en antenas.
* **SEC (Superintendencia de Electricidad y Combustibles - `sec.cl`):**
  * *Sanciones e informes técnicos:* Fallas de empresas de telecomunicaciones en labores preventivas y mantenimiento de infraestructura crítica (ej. sanción aplicada en Antuco).
* **SENAPRED (Ex-ONEMI - `senapred.cl`):**
  * *Consolidados de Emergencias Meteorológicas:* Informes de temporales que cuantifican cortes de suministro eléctrico, rutas cortadas y comunidades rurales aisladas.
* **INE / ODEPA:**
  * Datos censales sobre población rural dispersa en comunas cordilleranas (Quilaco, Alto Biobío, Santa Bárbara, Mulchén)[cite: 15].

### B. Prensa Regional (Casos Documentados y Testimonios)
* **Diario Concepción / TVU:**
  * *Noticia base de referencia:* "Incomunicados en la cordillera: advierten severas caídas de telecomunicaciones en zonas rurales de Biobío" (Septiembre 2026)[cite: 15].
  * *Puntos críticos documentados:*
    * Vulnerabilidad en **Quilaco, Hualqui, Mulchén, Antuco y Alto Biobío**[cite: 15].
    * Cortes de servicio que se extienden entre **15 y 30 días** tras temporales de viento y lluvia[cite: 15].
    * Testimonios de vecinos que deben trasladarse en vehículo a carreteras principales o cerros para solicitar ambulancias o realizar trámites[cite: 15].
    * Postura de la **Asociación de Municipios Cordilleranos del Biobío** exigiendo fiscalización y autonomía energética a las antenas[cite: 15].
  * *Ecuación de búsqueda en Google News:*
    ```text
    site:diarioconcepcion.cl ("incomunicados" OR "caídas de telecomunicaciones" OR "falta de señal") ("Quilaco" OR "Antuco" OR "Alto Biobío" OR "Hualqui")
    ```

---

## 3. Integración en la Estructura de Entregables (Guía del Proyecto)

```text
Entregable E1 / Capítulo 2 del Informe Final (E4):
├── 2.1 Identificación y Magnitud del Problema
│   ├── Datos empíricos: Índices de reclamos SUBTEL y sanciones SEC [Fuentes públicas]
│   ├── Escenario territorial: Comunas cordilleranas del Biobío y testimonios [Prensa regional]
│   └── Consecuencias de no abordar: Riesgo vital en emergencias médicas e incendios
├── 2.2 Mapa de Partes Interesadas (Stakeholders)
│   ├── Usuarios directos: Habitantes rurales y comités vecinales
│   ├── Equipos de respuesta: Postas de salud rural, SAMU, Retenes de Carabineros
│   └── Entidades administradoras: Municipios rurales y fiscalizadores (SUBTEL / SEC)
├── 2.3 Insuficiencia de Soluciones Existentes
│   ├── Enlaces satelitales comerciales (inviabilidad económica por vivienda)
│   ├── Radios VHF tradicionales (falta de datos clínicos estructurados/georreferenciados)
│   └── Red celular comercial (vulnerabilidad por falta de respaldo energético)
└── 2.4 Marco Regulatorio y Cumplimiento Normativo
    ├── Ley N° 21.719 (Protección de datos personales en el tránsito de alertas)
    └── Ley N° 20.584 (Resguardo estricto de datos sensibles de salud/triage)