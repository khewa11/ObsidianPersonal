Nmap es un escáner de red de código abierto utilizado para el descubrimiento de hosts y la auditoría de seguridad, mapeando los puertos y servicios disponibles. Link: https://nmap.org/

- Command: nmap -p- --open -T4 -v 172.67.157.227
  - Target[172.67.157.227],
  - Status[Host is up, 0.020s latency],
  - 80/tcp[open, http],
  - 443/tcp[open, https],
  - 2052/tcp[open, clearvisn],
  - 2053/tcp[open, knetd],
  - 2082/tcp[open, infowave],
  - 2083/tcp[open, radsec],
  - 2086/tcp[open, gnunet],
  - 2087/tcp[open, eli],
  - 2095/tcp[open, nbx-ser],
  - 2096/tcp[open, nbx-dir],
  - 8080/tcp[open, http-proxy],
  - 8443/tcp[open, https-alt],
  - 8880/tcp[open, cddbp-alt]
### Análisis de Resultados (Nmap) - Factor Cloudflare

* **Hallazgo Principal:** Los puertos expuestos (2052, 2082, 2083, 8443, etc.) y la cabecera HTTP confirman que la IP `172.67.157.227` pertenece a la infraestructura de **Cloudflare**.
* **Impacto Técnico:** La IP corresponde a un proxy reverso / WAF (Web Application Firewall), no al servidor real. Realizar escaneos de Nmap profundos (`-sV -sC`) contra esta IP generará ruido innecesario, será bloqueado y no revelará la infraestructura subyacente.
* **Mapeo ISO 27002:** El uso de un WAF es un hallazgo positivo para el reporte. Evidencia el cumplimiento de controles relacionados con la protección perimetral, gestión de red y mitigación de ataques externos (como DDoS).
* **Acciones a Tomar:**
  * Suspender el escaneo de red directo hacia esta IP.
  * Coordinar con Sebastián para redirigir los esfuerzos hacia la **Capa de Aplicación (Capa 7)** usando herramientas de análisis web (como OWASP ZAP o Burp Suite).
  * (Opcional) Aplicar técnicas de OSINT para intentar descubrir la IP real del servidor (Bypass de Cloudflare).