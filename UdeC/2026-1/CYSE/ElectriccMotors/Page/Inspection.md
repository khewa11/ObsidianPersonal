 WhatWeb es una herramienta de identificación de sitios web que ayuda a descubrir tecnologías, servicios y plataformas utilizadas en un servidor web. Link: https://github.com/urbanadventurer/WhatWeb.git
- Command: whatweb https://emdesigner.software/
	- https://emdesigner.software/ [200 OK] 
	- CloudFlare, 
	- Country[RESERVED][ZZ], 
	- Frame, 
	- HTML5, 
	- HTTPServer[cloudflare], 
	- IP[172.67.157.227], 
	- PoweredBy[peer-reviewed],
	- Script, 
	- Title[e-Machine Designer — Electric Machine Design Software (EMDS)], UncommonHeaders[x-content-type-options,report-to,nel,access-control-allow-origin,referrer-policy,link,cf-cache-status,cf-ray,alt-svc]

### Nivel 4 de Agresividad (Heavy)
El nivel 4 es el modo más exhaustivo y ruidoso de WhatWeb. A diferencia de los niveles inferiores, este nivel ejecuta pruebas agresivas de **todos** los plugins disponibles contra **todas** las URLs del objetivo, sin importar si hubo coincidencias previas. Esto implica realizar una gran cantidad de peticiones HTTP, lo que lo hace ideal para una inspección profunda pero aumenta el riesgo de ser bloqueado por sistemas de seguridad (IDS/WAF).