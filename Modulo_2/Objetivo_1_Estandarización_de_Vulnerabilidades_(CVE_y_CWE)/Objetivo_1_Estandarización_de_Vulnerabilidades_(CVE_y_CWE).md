**Objetivo 1: Estandarización de Vulnerabilidades (CVE y CWE):**

**CVE (Common Vulnerabilities and Exposures):** Es un diccionario público que asigna un identificador único (como CVE-2021-44228) a cada vulnerabilidad o exposición divulgada en un software o hardware concreto. 



**CWE (Common Weakness Enumeration):** Es una taxonomía o catálogo mantenido por MITRE que clasifica las debilidades subyacentes en la arquitectura, el diseño o el código de un sistema (por ejemplo, CWE-89 para inyección SQL o CWE-79 para Cross-Site Scripting).



**Diferencias:**

**CVE:**

&#x09;**Enfoque:** Una instancia concreta y real en un producto y versión específicos.

&#x09;**Propósito:** Rastrear, evaluar el impacto y parchar sistemas desplegados.

&#x09;**Relación:** Un CVE se mapea a uno o varios CWE que explican por qué ocurrió.

**CWE:**

&#x09;**Enfoque:** La categoría general o causa raíz del fallo de programación o diseño.

&#x09;**Propósito:** Prevenir errores durante el desarrollo y educar a los desarrolladores.

&#x09;**Relación:** Un mismo CWE puede ser el origen de miles de CVE distintos.



**Autoridades de Asignación (CNAs) y Consulta Pública**

**¿Quiénes asignan los CVE?**

Los identificadores son emitidos por las CNAs (CVE Numbering Authorities), organizaciones autorizadas por el Programa CVE (supervisado por MITRE y patrocinado por CISA).


**Herramientas automatizadas de detección:**

**Tenable Nessus:** Escáner de vulnerabilidades de infraestructura y red que audita servidores, sistemas operativos y servicios activos para detectar configuraciones inseguras y parches faltantes asociados a CVEs.

**Qualys VMDR (o Rapid7 InsightVM):** Plataformas empresariales de gestión de vulnerabilidades que realizan escaneos continuos en entornos locales y en la nube, priorizando los CVEs detectados según su riesgo real de explotación.



