# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
**Taller 5 - Evaluación de Seguridad con STRIDE aplicada al cliente real Élite Airsoft**

---

## 👥 Integrantes del equipo
- Daniel Felipe Forero
- Brandon Merchan
- Rita Trindade da Cruz

---

## 🧠 Descripción general del trabajo

El presente trabajo tuvo como objetivo aplicar el marco **STRIDE** sobre un proceso crítico del sistema del cliente real **Élite Airsoft**, con el fin de identificar amenazas de seguridad, analizar su posible impacto sobre la operación del negocio y proponer controles de mitigación acordes con su contexto real.

Para desarrollar el taller, el equipo seleccionó como proceso crítico el flujo de **reservas, pagos y consentimiento informado**, ya que en este punto convergen los principales activos sensibles del negocio: datos personales de los clientes, comprobantes de pago, historial de reservas, validación de asistencia y control operativo. A partir de este flujo se construyó la tabla STRIDE del cliente, en la cual se documentaron amenazas, escenarios de ataque, impactos potenciales, controles existentes, mitigaciones propuestas y nivel de riesgo.

El análisis permitió evidenciar que el negocio no enfrenta únicamente riesgos tecnológicos en sentido estricto, sino también riesgos operativos y de seguridad derivados de trabajar con procesos manuales, cuentas personales, evidencia no formalizada y una alta dependencia de un único operador.

---

## 🔧 Proceso de desarrollo

El desarrollo del trabajo comenzó con la selección del proceso más sensible del cliente. Se eligió el flujo compuesto por **WhatsApp, Nequi y Google Forms**, debido a que allí se concentra la mayor parte de la interacción con el cliente y también los principales riesgos de suplantación, alteración de información, pérdida de trazabilidad y exposición de datos personales.

Posteriormente, el equipo identificó los componentes y activos involucrados en ese flujo: cuenta de WhatsApp del operador, conversaciones de reserva, comprobantes de pago por Nequi, formulario de consentimiento informado, hoja de respuestas en Google Sheets, redes sociales del negocio y celular del operador. Sobre esos elementos se aplicó el marco STRIDE para evaluar amenazas de **Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service** y **Elevation of Privilege**.

Finalmente, se consolidó la información en una tabla de análisis de riesgos. Esta tabla permitió no solo clasificar las amenazas, sino también conectarlas con impactos concretos sobre el negocio, como pérdida de ingresos, daño reputacional, exposición de datos personales, problemas legales y parálisis operativa.

---

## 🔐 Proceso crítico analizado

El proceso crítico evaluado corresponde al flujo de atención y formalización de una reserva en Élite Airsoft. Este proceso inicia cuando el cliente conoce el negocio a través de redes sociales y se comunica por WhatsApp para consultar disponibilidad. Después de esto, el operador envía el formulario de consentimiento informado, solicita el pago anticipado por Nequi y confirma manualmente la reserva una vez recibe el comprobante.

Este flujo fue seleccionado porque concentra tres tipos de activos especialmente sensibles. En primer lugar, contiene **datos personales** del cliente, ya que el formulario recoge información de identificación y consentimiento. En segundo lugar, involucra **información financiera básica**, debido a que el pago del anticipo es requisito para confirmar la reserva. En tercer lugar, sostiene la **continuidad operativa del negocio**, porque si este flujo falla, el cliente no puede reservar, pagar ni ser atendido correctamente.

Por esta razón, cualquier vulnerabilidad dentro de este proceso puede traducirse no solo en un incidente de seguridad, sino también en un problema directo de operación, reputación y confianza comercial.

---

## 🧩 Análisis de seguridad con STRIDE

### Spoofing

Dentro del análisis se identificó un riesgo importante de suplantación de identidad asociado a las cuentas de WhatsApp y redes sociales del negocio. Un atacante podría crear perfiles falsos o números similares para hacerse pasar por Élite Airsoft y engañar a clientes, solicitando pagos o enviando información incorrecta sobre reservas. Esta amenaza es especialmente crítica porque el cliente no interactúa con una plataforma formal, sino con canales de mensajería y redes sociales donde la confianza depende mucho de la apariencia del perfil y del número de contacto.

### Tampering

También se identificaron amenazas de alteración de información. Un caso claro es el envío de comprobantes de pago manipulados, por ejemplo capturas editadas para simular una transferencia que en realidad no fue realizada. De igual forma, si la hoja de respuestas del formulario tiene permisos demasiado amplios, existe el riesgo de que se modifique o elimine información del consentimiento informado. En este contexto, la alteración no solo compromete la integridad de los datos, sino que puede dejar al negocio sin respaldo ante una reclamación o incidente.

### Repudiation

El análisis mostró debilidades importantes de repudio. Como gran parte de la operación ocurre en conversaciones de WhatsApp y verificaciones manuales, puede presentarse la situación en la que un cliente niegue haber reservado, haber pagado o haber recibido cierta información, mientras que el negocio tampoco cuenta con una evidencia consolidada, estructurada y fácil de consultar. Esta falta de trazabilidad aumenta los conflictos y debilita la capacidad del negocio para defenderse ante reclamos.

### Information Disclosure

Uno de los riesgos más sensibles detectados fue la exposición de datos personales. El flujo actual maneja información del cliente en formularios, hojas de cálculo, conversaciones privadas y posiblemente en el celular del operador. Si alguno de estos elementos es accedido por terceros no autorizados, se podría producir una divulgación indebida de datos personales, con consecuencias reputacionales y legales. Este riesgo se vuelve más delicado cuando se trata de consentimientos o información asociada a participantes de actividades recreativas.

### Denial of Service

La evaluación también identificó una amenaza clara de denegación del servicio. Actualmente, el proceso depende fuertemente de una sola persona y de un único dispositivo. Si el operador no responde, pierde el celular, sufre un robo o no puede atender durante un período de alta demanda, el flujo de reservas se detiene casi por completo. En este caso, la indisponibilidad no depende necesariamente de un ataque sofisticado, sino de la ausencia de redundancia operativa.

### Elevation of Privilege

Finalmente, se observó un riesgo de elevación de privilegios relacionado con el uso de cuentas personales para actividades del negocio, especialmente en el manejo de pagos. Si otra persona obtiene acceso al celular o a la aplicación utilizada para recibir dinero, podría consultar movimientos, transferir fondos o acceder a información que no debería estar disponible para terceros. La falta de separación entre recursos personales y del negocio amplifica este riesgo.

---

## 🚨 Hallazgos principales del análisis

El análisis STRIDE permitió concluir que las amenazas más relevantes del caso no están aisladas entre sí, sino que se relacionan alrededor de cuatro debilidades estructurales.

La primera es la **falta de formalización del canal oficial del negocio**, lo cual facilita la suplantación y afecta la confianza del cliente. La segunda es la **debilidad en la integridad y trazabilidad del proceso de pago y reserva**, ya que gran parte de la evidencia se conserva en capturas, mensajes y validaciones manuales. La tercera es la **exposición de datos personales sin suficientes controles de acceso**, especialmente en formularios, hojas de cálculo y dispositivos móviles. La cuarta es la **dependencia operativa de una sola persona**, lo cual convierte un problema de disponibilidad en un riesgo crítico para todo el negocio.

En conjunto, estos hallazgos muestran que la seguridad del cliente no depende únicamente de “tener tecnología”, sino de cómo están organizados los accesos, cómo se valida la información y qué tan recuperable es el proceso ante un incidente.

---

## 🛡️ Controles propuestos y priorización del riesgo

A partir de la tabla elaborada por el equipo, se propusieron controles orientados a reducir las amenazas más críticas del proceso. Entre los controles más relevantes se encuentran la adopción de **WhatsApp Business** como canal oficial, la publicación consistente del número auténtico del negocio, la verificación real de pagos en la aplicación y no solo por captura, la restricción de acceso a las respuestas del formulario y la separación entre cuentas personales y medios de pago del negocio.

También se propusieron controles de continuidad operativa, como designar un segundo responsable de respaldo, crear mecanismos de confirmación más formales para las reservas y proteger el dispositivo principal con cifrado, bloqueo remoto y mejores prácticas de acceso.

La priorización del riesgo mostró que las amenazas más urgentes son aquellas que podrían generar exposición de datos personales, fraude en pagos o indisponibilidad del proceso de reservas. Por ello, los controles iniciales deben concentrarse en proteger identidad digital, pagos, datos personales y disponibilidad del servicio.

---

## 🔍 Investigación complementaria

### Tema investigado:
**Buenas prácticas de seguridad para pequeños negocios que operan con canales digitales, datos personales y pagos electrónicos**

### Resumen

La investigación permitió confirmar que el uso de STRIDE resulta apropiado para este caso porque ayuda a identificar amenazas desde la estructura misma del proceso y no solo desde fallas técnicas aisladas. La documentación oficial de Microsoft explica que el threat modeling parte de modelar el sistema, identificar amenazas, proponer mitigaciones y validar los controles, lo cual coincide con la forma en que se desarrolló este taller. En el caso de Élite Airsoft, este enfoque fue útil porque el problema principal no es una única vulnerabilidad técnica, sino la combinación de canales dispersos, procesos manuales y datos sensibles dentro del mismo flujo.

Desde la perspectiva de buenas prácticas para pequeñas empresas, la guía de CISA resalta la importancia de aplicar controles de alto impacto y bajo costo, como autenticación multifactor, copias de seguridad, protección de cuentas críticas, actualización de software y preparación frente a incidentes. Estas recomendaciones se ajustan bien al contexto del cliente, ya que no requiere una infraestructura compleja para mejorar su seguridad, sino fortalecer los puntos donde hoy existe mayor exposición: WhatsApp, formularios, dispositivo móvil y acceso a información sensible.

En el contexto colombiano, la protección de datos personales también es relevante. La Ley 1581 de 2012 establece el marco general para el tratamiento de datos personales y exige que este se realice con autorización previa, expresa e informada del titular. Esto se conecta directamente con el formulario de consentimiento y con la necesidad de limitar el acceso a la información recolectada. Adicionalmente, aunque el negocio no opera con una pasarela de pagos tradicional, los principios de seguridad promovidos por PCI DSS resultan útiles para entender que los procesos de cobro deben tener trazabilidad, controles y menor dependencia de validaciones manuales, ya que de lo contrario se incrementa la exposición a fraude y repudio.

---

## ✅ Conclusiones

La aplicación del marco STRIDE al proceso de reservas, pagos y consentimiento informado de Élite Airsoft permitió identificar que el principal riesgo del cliente no está en una plataforma compleja, sino en la informalidad tecnológica con la que hoy opera un flujo crítico del negocio.

Las amenazas más relevantes se concentran en la suplantación del canal oficial, la alteración de comprobantes o registros, la falta de evidencia sólida para resolver disputas, la exposición de datos personales y la dependencia total de un único operador. Estas amenazas tienen impacto real sobre ingresos, reputación, privacidad y continuidad operativa.

En consecuencia, el análisis demuestra que fortalecer la seguridad del negocio no implica necesariamente una transformación costosa, sino priorizar controles básicos pero estratégicos: formalizar los canales oficiales, mejorar la verificación de pagos, restringir accesos a la información, separar recursos personales de los del negocio y crear mecanismos mínimos de respaldo operativo. Desde la perspectiva del taller, esa es la principal conclusión: en este caso, aplicar STRIDE permitió traducir riesgos abstractos en decisiones concretas de mejora para el cliente real.

---

## 📚 Referencias

[1] Microsoft. *Getting Started - Threat Modeling Tool*.  
https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-getting-started

[2] CISA. *Cyber Guidance for Small Businesses*.  
https://www.cisa.gov/cyber-guidance-small-businesses

[3] Departamento Administrativo de la Función Pública. *Ley 1581 de 2012*.  
https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=49981

[4] PCI Security Standards Council. *PCI Data Security Standard (PCI DSS)*.  
https://www.pcisecuritystandards.org/standards/pci-dss/