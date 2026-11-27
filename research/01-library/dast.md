# DAST
## What is
Dynamic application security testing (DAST) testing method used to identify vulnerabilities and misconfigurations in web applications, APIs and, more recently, mobile apps in running environments. black box testing.
### Tools
ZAP

link: https://www.ibm.com/think/topics/dynamic-application-security-testing

### ZAP

Las 4 GitHub Actions Oficiales de ZAP y qué hace cada una


GitHub Action Oficial	Qué hace según los Docs Oficiales	¿Lanza ataques activos?	Uso ideal en CI/CD
zaproxy/action-baseline
	Ejecuta el spider tradicional (y opcionalmente Ajax spider) durante 1 minuto por defecto y aplica únicamente reglas de escaneo pasivo (cabeceras HTTP, cookies inseguras, fugas de información).	No (100% pasivo y rápido).	Pull Requests, commits y hasta entornos de producción sin riesgo de romper datos.
zaproxy/action-full-scan
	Ejecuta el spider sin límite de tiempo por defecto, un Ajax spider opcional y luego lanza un escaneo activo completo (ataques reales: SQLi, XSS, path traversal, etc.) contra la aplicación.	Sí (ataques activos intrusivos).	Entornos de Staging / QA o ejecuciones nocturnas (cron), nunca en producción.
zaproxy/action-api-scan
	Importa una definición de API (OpenAPI/Swagger, SOAP o GraphQL desde URL o archivo local) y ejecuta pruebas pasivas y activas optimizadas para endpoints de API.	Sí (ataques activos sobre los endpoints).	Microservicios y APIs REST/GraphQL en entornos de pruebas.
zaproxy/action-af
	Ejecuta un plan YAML personalizado del ZAP Automation Framework (plan:), permitiendo controlar autenticación compleja, contextos, scripts y reportes múltiples (incluyendo SARIF, JSON, HTML).	Configurable según el plan YAML.	Flujos avanzados que requieren login/autenticación o exportar SARIF nativo.

https://github.com/zaproxy/action-full-scan