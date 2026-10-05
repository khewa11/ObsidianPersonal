---
tags:
  - proyecto-informatico
  - ingenieria-software
  - conectividad-rural
  - telecomunicaciones
  - biobio
date: 2026-10-05
type: propuesta-proyecto
---

# Propuestas de Proyecto: Resiliencia de Comunicaciones en Zonas Rurales

> [!abstract] Contexto del Problema
> En sectores rurales y precordilleranos de la Región del Biobío (como Quilaco, Alto Biobío, Hualqui y Antuco), los temporales y cortes de energía provocan la caída de las antenas y redes celulares, dejando a comunidades, postas y retenes completamente incomunicados frente a emergencias médicas o desastres[cite: 16].
> 
> Las propuestas siguientes abordan esta problemática desde la **Ingeniería Civil Informática**, enfocándose en arquitecturas de software, modelamiento matemático y sistemas distribuidos, cumpliendo con los criterios de admisibilidad del curso[cite: 1, 3].

---

## Opción 1: Conmutación Local de Emergencia mediante Telefonía Definida por Software (Local-Breakout / Open-Core)

### 1. Problema Específico
Cuando el enlace troncal (*backhaul* de fibra o satelital) que alimenta la antena de una localidad rural falla, los teléfonos móviles de los usuarios entran en estado "Sin Servicio"[cite: 16]. Esto imposibilita incluso la comunicación interna entre vecinos de un mismo valle, la posta local o el retén de Carabineros[cite: 14, 16].

### 2. Solución Tecnológica (Software)
Desarrollo y orquestación de un núcleo de red móvil local basado en software (*Open-Core SDR* como Open5GS u Osmocom) configurado para operar en modo **Local Breakout**. Al detectar la pérdida de conexión hacia el proveedor nacional, el sistema conmuta a un modo isla autónomo, registrando terminales móviles estándar y permitiendo cursar llamadas de voz sobre IP (VoIP) y mensajería SMS local de emergencia dentro del radio de cobertura comunitaria.

### 3. Aplicación de Ciencias de la Ingeniería y Matemáticas
* **Teoría de Colas y Tráfico Telefónico:** Modelamiento analítico del tráfico de voz mediante los modelos de **Erlang-B** (para estimar probabilidad de bloqueo) y **Erlang-C** (para gestión de colas de espera en llamadas críticas), regulando el algoritmo de control de admisión de la celda[cite: 5].
* **Protocolos de Señalización en Redes:** Implementación de conmutación de paquetes y señalización distribuida bajo estándares SIP (*Session Initiation Protocol*) y SDP sobre arquitecturas contenerizadas[cite: 4, 5].

### 4. Espacio de Soluciones (3 Alternativas Evaluables)
1. **Pila celular 4G/LTE local:** Implementación de núcleo EPC/5G Open5GS con radio definida por software (SDR).
2. **Pila celular ligera 2G/GSM:** Implementación de conmutación con Osmocom sobre hardware embebido de bajo consumo energético.
3. **Red comunitaria Hotspot VoIP:** Portal cautivo Wi-Fi con servidor PBX SIP (Asterisk/Kamailio) para clientes softphone.

### 5. Demostrabilidad en Vivo (Defensa oral E5 - 15 min)
* Simular en vivo la caída del enlace exterior (desconectando el adaptador WAN)[cite: 9].
* Evidenciar la transición automática del servicio a modo isla[cite: 9].
* Ejecutar con éxito una llamada de voz o transmisión de SMS entre dos dispositivos cliente conectados a la celda local[cite: 9].

### 6. Casos Reales e Innovaciones de Referencia
* **Rhizomatica y Telecomunicaciones Indígenas Comunitarias (TIC A.C., México):** Redes de telefonía móvil comunitaria de código abierto en la Sierra de Oaxaca (*Heimerl, K., et al., ACM DEV*).
* **Proyectos Open5GS / Osmocom:** Iniciativas internacionales de telefonía definida por software para rescate y zonas remotas.

---

## Opción 2: Sistema Inteligente de Planificación Topográfica y Optimización de Cobertura para Redes Comunitarias (GIS + ITM)

### 1. Problema Específico
Las municipalidades y comités rurales carecen de herramientas técnicas para planificar enlaces inalámbricos de emergencia a través de valles y cordones montañosos accidentados[cite: 14, 16]. La instalación empírica de antenas genera zonas de sombra y enlaces inviables con pérdidas económicas significativas[cite: 14].

### 2. Solución Tecnológica (Software)
Plataforma computacional de optimización espacial que integra Modelos Digitales de Elevación (DEM satelitales) y algoritmos de propagación electromagnética. El software resuelve el problema de ubicación óptima de nodos repetidores (*Facility Location Problem*), determinando con precisión las coordenadas y alturas mínimas requeridas para garantizar la interconexión entre postas, escuelas y puntos críticos con el menor costo posible.

### 3. Aplicación de Ciencias de la Ingeniería y Matemáticas
* **Modelamiento Electromagnético Computacional:** Implementación del algoritmo **Irregular Terrain Model (ITM / Longley-Rice)** y cómputo de difracción sobre obstáculos topográficos junto al cálculo volumétrico del elipsoide de Fresnel[cite: 5].
* **Optimización Combinatoria:** Formulación matemática del problema de cobertura de conjuntos (*Set Covering / Facility Location Problem*) resuelto mediante metaheurísticas (Algoritmos Genéticos o *Simulated Annealing*) sujetas a restricciones presupuestarias y de relieve[cite: 4, 5].

### 4. Espacio de Soluciones (3 Alternativas Evaluables)
1. **Programación Lineal Entera Mixta (MILP):** Resolución exacta mediante solvers matemáticos (alto requerimiento de cómputo).
2. **Metaheurística Multiobjetivo:** Algoritmo genético (ej. NSGA-II) que pondera cobertura poblacional versus costo de nodos.
3. **Heurística Voraz (Greedy):** Algoritmo aproximado basado en matrices de visibilidad (*Viewshed Analysis*) secuencial.

### 5. Demostrabilidad en Vivo (Defensa oral E5 - 15 min)
* Cargar datos topográficos reales de una comuna del Biobío (ej. cuenca de Quilaco o Alto Biobío)[cite: 9, 16].
* Configurar parámetros de presupuesto y puntos críticos obligatorios (posta, retén)[cite: 9].
* Ejecutar el algoritmo de optimización en vivo y renderizar el mapa interactivo con la ubicación calculada de los nodos y el perfil de elevación del enlace[cite: 9].

### 6. Casos Reales e Innovaciones de Referencia
* **Guifi.net (España):** Plataforma ciudadana que utiliza herramientas computacionales de cálculo de enlaces para estructurar una red libre de más de 35.000 nodos (*Baig, R., et al., Computer Networks*).
* **SPLAT! y Radio Mobile:** Motores científicos consolidados en telecomunicaciones para simulación de radioenlaces sobre modelos de terreno accidentado.