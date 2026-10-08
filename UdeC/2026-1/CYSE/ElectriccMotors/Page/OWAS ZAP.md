## 🛡️ Vulnerabilidades de Capa de Aplicación (Escaneo Pasivo - OWASP ZAP)

### 1. Content Security Policy (CSP) Header Not Set
* **Nivel de Riesgo:** Medio
* **CWE:** 693
* **Descripción:** El servidor no está configurando la cabecera HTTP `Content-Security-Policy`. Esta política es una capa de seguridad adicional que ayuda a prevenir ataques de inyección de datos y Cross-Site Scripting (XSS), ya que le dice al navegador exactamente desde qué dominios está permitido cargar recursos (scripts, imágenes, estilos).
* **Impacto:** Facilita la ejecución de scripts maliciosos si un atacante logra encontrar un vector de inyección (XSS).
* **Solución:** Configurar el servidor o el proxy reverso para que emita la cabecera CSP definiendo estrictamente los orígenes confiables.
* **Mapeo ISO 27002:** Control 14.2.5 (Principios de construcción de sistemas seguros) y Control 14.1.2 (Aseguramiento de los servicios de aplicación en redes públicas).

### 2. Missing Anti-clickjacking Header (X-Frame-Options)
* **Nivel de Riesgo:** Medio
* **CWE:** 1021
* **Descripción:** La respuesta del servidor no incluye la cabecera `X-Frame-Options` ni la directiva `frame-ancestors` en CSP. 
* **Impacto:** Permite que un atacante incruste la página web dentro de un `<iframe>` invisible en una página maliciosa. Esto puede engañar a un usuario para que haga clic en botones o enlaces de la aplicación original sin darse cuenta (Clickjacking).
* **Solución:** Implementar la cabecera `X-Frame-Options: DENY` o `SAMEORIGIN` para evitar que la página sea renderizada en marcos de terceros.
* **Mapeo ISO 27002:** Control 14.2.5 (Principios de construcción de sistemas seguros).

### 3. Cross-Domain Misconfiguration (CORS Excesivamente Permisivo)
* **Nivel de Riesgo:** Medio
* **CWE:** 264
* **Evidencia:** `Access-Control-Allow-Origin: *`
* **Descripción:** El servidor tiene una política de Intercambio de Recursos de Origen Cruzado (CORS) mal configurada usando el comodín `*`. Esto significa que cualquier dominio de internet tiene permiso para leer las respuestas de las APIs o recursos de este servidor a través del navegador del usuario.
* **Impacto:** Si la aplicación maneja datos sensibles o sesiones autenticadas, un sitio de terceros podría forzar al navegador del usuario a realizar peticiones y leer esa información.
* **Solución:** Restringir la cabecera `Access-Control-Allow-Origin` únicamente a los dominios específicos que necesitan consumir los recursos de la aplicación.
* **Mapeo ISO 27002:** Control 13.1.3 (Segregación en redes) y Control 14.2.5.

### 4. Sub Resource Integrity (SRI) Attribute Missing
* **Nivel de Riesgo:** Bajo/Medio
* **CWE:** 345
* **Evidencia:** Falta el atributo `integrity` en la carga de fuentes/estilos externos (ej. `https://fonts.googleapis.com/...`).
* **Descripción:** La página carga scripts o hojas de estilo (CSS) desde servidores de terceros sin verificar su integridad.
* **Impacto:** Si el servidor de terceros (como un CDN) es comprometido y el archivo original es modificado con código malicioso, la página web del objetivo ejecutará ese código automáticamente.
* **Solución:** Agregar el atributo `integrity` con el hash criptográfico del archivo esperado en las etiquetas `<link>` o `<script>`.
* **Mapeo ISO 27002:** Control 14.1.2 (Aseguramiento de los servicios de aplicación) y Control 15.1.1 (Política de seguridad de la información para las relaciones con proveedores).

### 5. Absence of Anti-CSRF Tokens
* **Nivel de Riesgo:** Bajo (Contextual)
* **CWE:** 352
* **Evidencia:** Formulario apuntando a `action="https://formspree.io/f/mlgabgyb"`.
* **Descripción:** No se encontraron tokens Anti-CSRF en un formulario HTML. Un token Anti-CSRF es un valor aleatorio y único que evita que un atacante fuerce al usuario a enviar solicitudes falsificadas.
* **Impacto:** Un atacante podría crear una página falsa que envíe datos a este formulario sin que el usuario se dé cuenta.
* **Nota Técnica de Auditoría:** Dado que el formulario envía los datos a *Formspree* (un servicio externo de recolección de correos) y no al propio servidor web, el riesgo real es muy bajo, ya que no se están ejecutando cambios de estado críticos en la aplicación (como cambiar una contraseña o hacer una transferencia).
* **Solución:** Implementar tokens sincronizados si el formulario pasa a procesarse localmente.
* **Mapeo ISO 27002:** Control 14.2.5 (Principios de construcción de sistemas seguros).

## 🔬 Metodología de Pruebas y Triaje de Falsos Positivos

Para garantizar la precisión y relevancia de los resultados técnicos presentados en este informe, todos los hallazgos generados por herramientas automatizadas (como el escáner OWASP ZAP) fueron sometidos a un riguroso proceso de validación y triaje manual. Esto asegura que la evaluación de riesgos se base exclusivamente en vulnerabilidades confirmadas dentro del alcance del proyecto (Scope).

### Ejemplo de Triaje y Descarte (Falso Positivo Crítico)

Durante la fase de escaneo pasivo, el sistema de análisis heurístico alertó sobre una potencial filtración de datos críticos:

* **Vulnerabilidad Reportada:** PII Disclosure / Fuga de Información de Identificación Personal (CWE-359).
* **Nivel de Riesgo Asignado por la Herramienta:** Alto.
* **Evidencia Detectada:** Secuencia numérica `4105196173812`, identificada preliminarmente por el escáner como un número de tarjeta de crédito válido (Visa/City Bank) al coincidir con el Algoritmo de validación de Luhn.

**Análisis de Validación Manual:**
Al inspeccionar la solicitud HTTP exacta que detonó la alerta, se procedió a aislar el contexto de la respuesta. Se determinó lo siguiente:
1. **Origen fuera de alcance:** El tráfico interceptado no provenía de la aplicación objetivo (`emdesigner.software`), sino de una solicitud de fondo hacia `firefox.settings.services.mozilla.com`.
2. **Naturaleza de los datos:** El cuerpo de la respuesta contenía datos de telemetría interna del navegador (`mozilla::dom::quota`).
3. **Coincidencia Matemática:** La secuencia numérica identificada correspondía en realidad a una marca de tiempo generada por el sistema y hashes internos que, por mera casualidad matemática, cumplían con la fórmula de Luhn utilizada para validar tarjetas bancarias.

**Conclusión del Triaje:**
El hallazgo fue clasificado categóricamente como un **Falso Positivo**. Fue mitigado en la herramienta excluyendo los dominios de terceros del "Contexto" de ataque y, en consecuencia, ha sido excluido de la matriz de riesgos y del plan de remediación de este reporte.