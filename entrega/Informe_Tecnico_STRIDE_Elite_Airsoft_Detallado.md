# 📄 Informe Técnico Detallado del Taller

## 🔖 Nombre del taller
**Taller 5 - Evaluación de Seguridad con STRIDE aplicada al cliente real Élite Airsoft**

---

## 👥 Integrantes del equipo
- Daniel Felipe Forero
- Brandon Merchan
- Rita Trindade da Cruz

---

## 📆 Fecha
25 de marzo de 2026

---

## 🧠 Resumen ejecutivo

El presente informe documenta un análisis de amenazas con enfoque **STRIDE** aplicado al proceso crítico de **reservas, pagos y consentimiento informado** del cliente real **Élite Airsoft**. El proceso actual depende principalmente de **WhatsApp**, **Nequi**, **Google Forms** y **Google Sheets**, además del dispositivo móvil personal del operador y de los perfiles del negocio en redes sociales. Aunque esta arquitectura es funcional para la operación diaria, introduce una superficie de ataque amplia, heterogénea y poco formalizada.

La matriz consolidada identifica **10 amenazas** distribuidas en las seis categorías de STRIDE, con cobertura completa del modelo. La priorización arroja **5 riesgos críticos** y **5 riesgos altos**, sin hallazgos clasificados como medio o bajo en el estado actual. Esta distribución no implica que el negocio esté “sobretecnificado”, sino lo contrario: refleja que el proceso opera sobre herramientas válidas pero sin suficientes controles de identidad, integridad, trazabilidad, privacidad y continuidad.

Los hallazgos más graves se concentran en cinco frentes: **suplantación del canal oficial**, **fraude por comprobantes manipulados**, **exposición de datos personales**, **uso de cuentas personales para operaciones del negocio** y **dependencia operativa de un único operador**. En conjunto, estas debilidades afectan no solo la seguridad de la información, sino también la reputación comercial, la capacidad de recaudo, la defensa frente a reclamaciones y la continuidad del servicio.

Desde una perspectiva de tratamiento, el informe concluye que Élite Airsoft no requiere inicialmente una plataforma compleja ni una inversión alta en software empresarial; requiere primero una **formalización mínima del flujo**. Los controles con mejor relación costo-beneficio son: institucionalizar el canal oficial en **WhatsApp Business**, verificar pagos contra el movimiento real y no contra capturas, separar medios personales y medios del negocio, endurecer el acceso a formularios y hojas de respuesta, reducir la recolección de datos innecesarios, habilitar mecanismos de respaldo operativo y establecer evidencia mínima de cada reserva. Estas acciones reducen simultáneamente el riesgo técnico, operativo y legal.

---

## 🎯 Objetivo general

Aplicar el marco **STRIDE** sobre un proceso crítico del negocio Élite Airsoft para identificar amenazas, analizar su impacto técnico y operativo, establecer prioridades de tratamiento y proponer controles de mitigación ajustados al contexto real del cliente.

## 🎯 Objetivos específicos

1. Delimitar el proceso crítico de reservas, pagos y consentimiento informado.
2. Identificar activos, flujos de información, dependencias y fronteras de confianza.
3. Clasificar amenazas usando las seis categorías STRIDE.
4. Evaluar impacto, probabilidad y nivel de riesgo de cada hallazgo.
5. Proponer controles técnicos, operativos y administrativos priorizados por urgencia.
6. Relacionar los hallazgos con buenas prácticas oficiales y consideraciones regulatorias aplicables al caso colombiano.

---

## 🏢 Contexto del cliente y del proceso analizado

Élite Airsoft es un negocio que presta servicios recreativos vinculados a actividades de airsoft y atención a clientes mediante canales digitales ligeros. Su operación comercial depende de una secuencia manual y fragmentada:

1. El cliente conoce el negocio por **Instagram/Facebook**.
2. Se comunica por **WhatsApp** para consultar disponibilidad, precios y condiciones.
3. El operador envía o solicita un **formulario de consentimiento informado** mediante **Google Forms**.
4. El cliente realiza el anticipo por **Nequi** y comparte el comprobante por chat.
5. El operador valida el pago manualmente y confirma la reserva.
6. La evidencia queda distribuida entre el chat, la aplicación de pagos, el formulario y la hoja de respuestas.

Desde el punto de vista de seguridad, esta secuencia mezcla activos de naturaleza distinta:
- **Identidad digital del negocio**: número de WhatsApp, perfiles sociales, nombre comercial.
- **Datos personales del cliente**: nombre, identificación y eventualmente información de menores o consentimiento.
- **Evidencias de transacción**: capturas, confirmaciones, historial de mensajes.
- **Capacidad operativa**: disponibilidad del operador y del celular principal.
- **Trazabilidad administrativa**: reservas, cobros, soporte frente a reclamos o auditorías.

La criticidad del proceso radica en que un fallo en cualquiera de estos puntos puede traducirse en pérdida inmediata de ingresos, exposición de datos, conflicto legal o interrupción del servicio.

---

## 🔐 Alcance del análisis

El alcance del taller se concentró en el flujo operativo más expuesto del negocio:

- **Canales incluidos**: WhatsApp, Instagram, Facebook, Nequi, Google Forms, Google Sheets y celular del operador.
- **Activos incluidos**: identidad de canal, conversaciones de reserva, comprobantes de pago, datos del formulario, acceso al dispositivo y evidencia operativa.
- **Tipo de análisis**: identificación de amenazas, evaluación cualitativa del riesgo y propuesta de mitigaciones.
- **Horizonte del análisis**: estado actual del proceso, sin rediseñar una arquitectura empresarial completa ni realizar pruebas de penetración.

### Exclusiones
- No se evaluó infraestructura de red avanzada, servidores propios, APIs ni bases de datos corporativas.
- No se realizó auditoría forense de configuraciones reales en Meta, Google o Nequi.
- No se emitió concepto jurídico vinculante; las referencias normativas se usan como marco de análisis y cumplimiento esperado.

---

## 🧭 Metodología aplicada

El enfoque se basó en la lógica de **threat modeling** promovida por Microsoft: **modelar el sistema, identificar amenazas, proponer mitigaciones y validar el tratamiento**. En el caso de Élite Airsoft, esta metodología se adaptó a un sistema socio-técnico y no exclusivamente a una aplicación software. La adaptación es válida porque el proceso sí posee activos, flujos, actores y fronteras de confianza claramente identificables.

### Fases aplicadas

**1. Delimitación del sistema**  
Se definió el proceso crítico de negocio y se identificaron actores, herramientas, activos y dependencias.

**2. Levantamiento de componentes y flujos**  
Se mapeó el recorrido de la información desde el primer contacto del cliente hasta la confirmación de la reserva.

**3. Identificación de fronteras de confianza**  
Se reconocieron puntos donde cambia el nivel de control:  
- del entorno público de redes al chat privado,  
- del chat al medio de pago,  
- del formulario al almacenamiento de respuestas,  
- del negocio al dispositivo personal del operador.

**4. Clasificación con STRIDE**  
Cada amenaza se clasificó como:
- **Spoofing**
- **Tampering**
- **Repudiation**
- **Information Disclosure**
- **Denial of Service**
- **Elevation of Privilege**

**5. Priorización cualitativa**  
La matriz trabajó con criterios de:
- **Probabilidad**: alta, media o baja.
- **Impacto**: efectos económicos, operativos, reputacionales, legales y de privacidad.
- **Nivel de riesgo**: alto o crítico para el caso analizado.

**6. Definición de mitigaciones**  
Las recomendaciones se ordenaron según urgencia, costo aproximado y facilidad de implementación.

---

## 🧱 Lectura técnica del sistema actual

A nivel lógico, el proceso actual puede representarse así:

```text
[Cliente]
   ↓
[Instagram / Facebook]
   ↓
[WhatsApp del operador]
   ├── envío/recepción de mensajes
   ├── envío de comprobante Nequi
   └── enlace al formulario
        ↓
   [Google Forms]
        ↓
   [Google Sheets / Respuestas]
        ↓
[Validación manual por operador]
        ↓
[Confirmación de reserva]
```

### Principales fronteras de confianza

1. **Canales públicos ↔ canal privado**
   - La identidad del negocio puede ser imitada antes de que el cliente entre en contacto directo.
2. **Cliente ↔ evidencia de pago**
   - El negocio depende de una prueba visual y no de una confirmación transaccional integrada.
3. **Formulario ↔ almacenamiento**
   - El consentimiento viaja por una herramienta legítima, pero su protección depende de la configuración de acceso.
4. **Negocio ↔ dispositivo personal**
   - El operador concentra credenciales, datos, pagos y comunicaciones en un solo equipo.

### Debilidad estructural de la arquitectura actual

La mayor debilidad no es una sola vulnerabilidad técnica, sino la **concentración de funciones críticas en herramientas desacopladas y administradas manualmente**. En términos de seguridad, esto produce:
- escasa trazabilidad,
- controles inconsistentes,
- dificultad para separar lo personal de lo comercial,
- baja auditabilidad,
- ausencia de redundancia.

---

## 📊 Resultados cuantitativos de la matriz

### Distribución por nivel de riesgo

| Nivel | Cantidad | Porcentaje |
|---|---:|---:|
| Crítico | 5 | 50% |
| Alto | 5 | 50% |
| Medio | 0 | 0% |
| Bajo | 0 | 0% |
| **Total** | **10** | **100%** |

### Distribución por categoría STRIDE

| Categoría | Cantidad | Porcentaje |
|---|---:|---:|
| Spoofing | 2 | 20% |
| Tampering | 2 | 20% |
| Repudiation | 2 | 20% |
| Information Disclosure | 2 | 20% |
| Denial of Service | 1 | 10% |
| Elevation of Privilege | 1 | 10% |
| **Total** | **10** | **100%** |

### Lectura ejecutiva del resultado

La cobertura **6/6** de STRIDE confirma que el proceso presenta riesgos distribuidos en todas las dimensiones principales del modelo, no únicamente en confidencialidad o fraude. Esto es relevante porque demuestra que el caso de Élite Airsoft no debe tratarse como un problema aislado de “cuentas inseguras”, sino como un proceso de negocio con debilidades transversales de identidad, integridad, evidencia, privacidad y continuidad.

---

## 🚨 Análisis detallado de amenazas

A continuación se presenta la lectura técnica de cada una de las 10 amenazas priorizadas en la matriz.

### T01 — Suplantación del WhatsApp oficial
- **Activo afectado:** WhatsApp personal del operador
- **Categoría STRIDE:** Spoofing
- **Nivel de riesgo:** Crítico

**Descripción técnica**  
El negocio depende de un número de contacto que el cliente reconoce por contexto, no por un mecanismo robusto de identidad. Esto permite que un atacante cree un número o perfil similar y capture conversaciones, pagos o anticipos simulando ser el negocio legítimo.

**Precondiciones**
- El cliente no tiene un canal inequívoco para validar el número oficial.
- No hay una presencia institucional consistente del contacto auténtico.
- La confirmación del canal depende del reconocimiento visual y de la confianza informal.

**Impacto**
- Fraude directo al cliente.
- Daño reputacional al negocio real.
- Pérdida de confianza en canales digitales.
- Incremento en disputas y reclamaciones.

**Controles existentes**
- Prácticamente inexistentes.
- El canal carece de institucionalización fuerte y de una validación formal.

**Tratamiento recomendado**
- Migrar a **WhatsApp Business** como canal formal del negocio.
- Publicar el número oficial en todos los puntos de contacto del negocio.
- Mantener consistencia del canal en bio, historias destacadas y respuestas automáticas.
- Implementar un texto de validación visible: “Éste es el único número autorizado para reservas”.
- Evaluar mecanismos de verificación de cuenta cuando sean aplicables.

**Comentario técnico**  
Se trata de una amenaza de muy alta prioridad porque explota el punto de entrada del proceso y puede producir daños antes de que exista cualquier otra evidencia transaccional.

---

### T02 — Repudio de reserva o de pago en chat
- **Activo afectado:** conversación de reserva en WhatsApp
- **Categoría STRIDE:** Repudiation
- **Nivel de riesgo:** Alto

**Descripción técnica**  
La reserva y buena parte de la relación comercial se sostienen en conversaciones informales. Aunque el historial del chat existe, no constituye un mecanismo sólido de no repudio. El cliente puede negar haber confirmado una reserva, haber enviado un comprobante válido o haber aceptado condiciones.

**Precondiciones**
- Confirmaciones dispersas en mensajes no estructurados.
- Ausencia de una orden de servicio o confirmación formal.
- Evidencia no archivada ni centralizada.

**Impacto**
- Doble reserva.
- No-show sin base clara para retener anticipo.
- Reclamos difíciles de resolver.
- Debilidad probatoria frente a conflictos.

**Controles existentes**
- Historial del chat.
- Capturas ocasionales.

**Debilidad del control actual**  
El chat preserva comunicación, pero no resuelve por sí mismo la trazabilidad de negocio si la evidencia no se organiza ni se vincula a cada reserva.

**Tratamiento recomendado**
- Generar una confirmación estándar por reserva.
- Asociar cada reserva a un identificador simple.
- Archivar evidencia de pago y consentimiento en una carpeta con estructura por fecha/reserva.
- Enviar confirmación final por un segundo canal o por un mensaje con formato fijo.

**Comentario técnico**  
No es el riesgo más devastador en términos de pérdida masiva, pero sí es un riesgo de fricción crónica que desgasta al negocio y complica el crecimiento.

---

### T03 — Alteración del comprobante de pago
- **Activo afectado:** comprobante de pago compartido por Nequi
- **Categoría STRIDE:** Tampering
- **Nivel de riesgo:** Alto

**Descripción técnica**  
La operación acepta como evidencia inicial una captura enviada por el cliente. En ausencia de verificación transaccional directa, el comprobante puede ser manipulado digitalmente y aun así inducir al operador a confirmar la reserva.

**Precondiciones**
- Validación visual manual.
- Presión operativa por atender rápido.
- Falta de conciliación directa contra la app o contra un identificador oficial de movimiento.

**Impacto**
- Prestación del servicio sin recaudo real.
- Pérdida directa de ingresos.
- Dificultad posterior para demostrar fraude.
- Posible escalamiento si el atacante repite el patrón.

**Controles existentes**
- Revisión visual por el operador.

**Debilidad del control actual**  
El control depende de percepción humana y puede fallar ante capturas editadas, interfaces similares o simples errores de atención.

**Tratamiento recomendado**
- Confirmar el ingreso del dinero contra el movimiento real en la aplicación.
- Solicitar el identificador o referencia de la transacción, no solo una imagen.
- Definir que no existe reserva confirmada hasta verificar el ingreso.
- A mediano plazo, migrar a un flujo con confirmación más automatizada.

**Comentario técnico**  
Es un riesgo clásico de integridad de evidencia. Aunque no involucra una intrusión sofisticada, su explotación es sencilla y de impacto económico inmediato.

---

### T04 — Exposición de datos personales en Google Forms / Sheets
- **Activo afectado:** formulario y hoja de respuestas de consentimiento
- **Categoría STRIDE:** Information Disclosure
- **Nivel de riesgo:** Crítico

**Descripción técnica**  
El proceso recolecta datos personales mediante Google Forms y los deposita en una hoja de respuestas. El riesgo no está en negar que Google utilice HTTPS, sino en que la privacidad real depende de **qué datos se recolectan**, **quién puede verlos**, **cómo se comparten**, **qué configuraciones del formulario están activas** y **qué política se informa al titular**.

**Precondiciones**
- Recolección de datos identificables.
- Posibles permisos amplios en la hoja de respuestas.
- Falta de aviso visible de privacidad y finalidad.
- Potencial presencia de datos de menores o información especialmente sensible para el contexto.

**Impacto**
- Exposición de datos personales.
- Riesgo reputacional.
- Riesgo de reclamación por tratamiento inadecuado.
- Incumplimiento de principios de minimización y seguridad del tratamiento.

**Controles existentes**
- El servicio usa transporte seguro.
- Existe almacenamiento en plataforma reconocida.

**Debilidad del control actual**  
La seguridad del transporte no resuelve por sí misma la seguridad del tratamiento. El problema crítico está en los permisos, la gobernanza del dato y la necesidad real de cada campo solicitado.

**Tratamiento recomendado**
- Minimizar campos y eliminar datos no estrictamente necesarios.
- Incluir aviso de privacidad, finalidad y responsable del tratamiento.
- Restringir el acceso a la hoja de respuestas a muy pocas personas.
- Deshabilitar opciones que expongan resúmenes o faciliten circulación innecesaria.
- Establecer conservación y eliminación periódica de registros.

**Comentario técnico**  
Este hallazgo es crítico porque combina privacidad, evidencia legal y reputación. Además, compromete un punto especialmente sensible si intervienen menores de edad.

---

### T05 — Modificación indebida de respuestas del consentimiento
- **Activo afectado:** hoja de respuestas del consentimiento
- **Categoría STRIDE:** Tampering
- **Nivel de riesgo:** Alto

**Descripción técnica**  
Si la hoja asociada al formulario tiene permisos de edición amplios o mal controlados, un tercero podría modificar, borrar o alterar respuestas. Esto afecta directamente la integridad del consentimiento y puede dejar al negocio sin soporte válido ante un incidente.

**Precondiciones**
- Acceso de edición innecesario.
- Gobernanza débil de permisos.
- Ausencia de exportación o sellado de evidencia.

**Impacto**
- Pérdida de respaldo legal.
- Imposibilidad de demostrar consentimiento.
- Deterioro de la integridad documental.

**Controles existentes**
- Historial de cambios de Google Sheets.

**Debilidad del control actual**  
El historial ayuda a reconstruir eventos, pero no sustituye un control preventivo de acceso ni garantiza respuesta rápida ante una alteración.

**Tratamiento recomendado**
- Principio de mínimo privilegio en permisos.
- Solo una cuenta propietaria con edición.
- Exportación de la evidencia relevante a PDF o repositorio controlado.
- Alertas o revisiones periódicas del historial de cambios.

**Comentario técnico**  
Este riesgo no siempre se materializa con alta frecuencia, pero su impacto jurídico-operativo es serio cuando coincide con accidentes o reclamos.

---

### T06 — Uso de cuenta Nequi personal para el negocio
- **Activo afectado:** cuenta de pagos del operador
- **Categoría STRIDE:** Elevation of Privilege
- **Nivel de riesgo:** Crítico

**Descripción técnica**  
El flujo de cobro usa una cuenta personal para recaudos del negocio. Eso concentra privilegios financieros y visibilidad transaccional en un entorno personal. Si otra persona accede al dispositivo o a la app, obtiene capacidades superiores a las que debería tener sobre fondos e información del negocio.

**Precondiciones**
- Mezcla entre finanzas personales y del negocio.
- Ausencia de segregación de funciones.
- Protección concentrada en el celular principal.

**Impacto**
- Desvío de fondos.
- Confusión contable.
- Dificultad de auditoría.
- Mayor superficie para abuso interno o acceso oportunista.

**Controles existentes**
- Biometría o bloqueo del teléfono.

**Debilidad del control actual**  
La biometría protege el acceso inmediato, pero no resuelve el problema de fondo: la arquitectura operativa es incorrecta porque mezcla identidad personal y flujo financiero empresarial.

**Tratamiento recomendado**
- Separar medio de recaudo del negocio y medio personal.
- Definir una cuenta exclusiva para cobros del negocio.
- Formalizar registro contable y conciliación.
- Proteger el acceso con controles adicionales disponibles en la plataforma y en el dispositivo.

**Comentario técnico**  
La gravedad no depende solo de un atacante externo; también se relaciona con abuso interno, pérdida de control financiero y opacidad administrativa.

---

### T07 — Suplantación de perfiles en redes sociales
- **Activo afectado:** Instagram/Facebook del negocio
- **Categoría STRIDE:** Spoofing
- **Nivel de riesgo:** Alto

**Descripción técnica**  
La imagen del negocio en redes puede ser clonada por terceros que reutilizan fotos, nombre y estilo visual para atraer clientes, ofrecer promociones falsas o redirigir pagos.

**Precondiciones**
- Marca visible pero no suficientemente consolidada.
- Público que confía en la apariencia del perfil.
- Falta de aviso constante sobre el canal oficial.

**Impacto**
- Estafas a clientes potenciales.
- Daño reputacional.
- Aumento de consultas, quejas o denuncias.
- Debilitamiento de la marca.

**Controles existentes**
- Presencia orgánica del negocio.

**Debilidad del control actual**  
La sola existencia de la cuenta legítima no evita la aparición de clones.

**Tratamiento recomendado**
- Publicación reiterada del canal oficial.
- Unificación de nombre, usuario y datos de contacto.
- Monitoreo de menciones y reportes.
- Solicitud de mecanismos de verificación cuando aplique.

**Comentario técnico**  
Este hallazgo complementa T01 y demuestra que la identidad digital del negocio debe gestionarse como un activo crítico.

---

### T08 — Dependencia absoluta del operador único
- **Activo afectado:** continuidad del proceso de reserva
- **Categoría STRIDE:** Denial of Service
- **Nivel de riesgo:** Crítico

**Descripción técnica**  
Toda la operación recae sobre una sola persona y un solo dispositivo. Cualquier indisponibilidad del operador —enfermedad, robo, daño del equipo, desconexión o saturación— interrumpe el flujo completo.

**Precondiciones**
- Sin segundo operador.
- Sin canal alterno de continuidad.
- Sin automatización mínima de autoservicio.

**Impacto**
- Cese temporal de ingresos.
- Pérdida de reservas durante ventanas de alta demanda.
- Mala experiencia del cliente.
- Dependencia operacional extrema.

**Controles existentes**
- Ninguno relevante.

**Tratamiento recomendado**
- Definir un segundo responsable o respaldo.
- Usar capacidades empresariales del canal para atención multiagente cuando sea viable.
- Implementar respuestas automáticas y mensajes de contingencia.
- Introducir un mecanismo alterno de registro de reservas.

**Comentario técnico**  
Este riesgo es crítico porque compromete la disponibilidad del negocio entero. No requiere un ciberataque sofisticado: basta una contingencia cotidiana.

---

### T09 — Exposición de datos por pérdida o robo del celular
- **Activo afectado:** historial de conversaciones y evidencias en el dispositivo
- **Categoría STRIDE:** Information Disclosure
- **Nivel de riesgo:** Crítico

**Descripción técnica**  
El celular del operador funciona como repositorio de chats, comprobantes, datos personales y posiblemente documentos sensibles. La pérdida o robo del dispositivo puede convertirse en una brecha de datos si no existen controles de cifrado, bloqueo remoto y respaldo seguro.

**Precondiciones**
- Concentración de datos en un solo dispositivo.
- Uso intensivo del celular como repositorio principal.
- Ausencia o debilidad de medidas de recuperación/limpieza remota.

**Impacto**
- Brecha masiva de datos personales.
- Exposición de historial comercial.
- Riesgo legal y reputacional.
- Interrupción adicional de la operación.

**Controles existentes**
- Contraseña o huella.

**Debilidad del control actual**  
Un bloqueo básico ayuda, pero no sustituye cifrado, borrado remoto, preparación previa y buenas prácticas de minimización de datos.

**Tratamiento recomendado**
- Asegurar cifrado y bloqueo robusto del dispositivo.
- Verificar que exista capacidad de localización, bloqueo y borrado remoto.
- Reducir el envío de documentos sensibles por chat.
- Respaldar información crítica en entornos controlados.
- Definir procedimiento de respuesta ante pérdida del equipo.

**Comentario técnico**  
Es un hallazgo crítico por la combinación de confidencialidad, continuidad y dependencia del dispositivo.

---

### T10 — Ausencia de registros formales y trazabilidad fiscal/comercial
- **Activo afectado:** proceso general del negocio
- **Categoría STRIDE:** Repudiation
- **Nivel de riesgo:** Alto

**Descripción técnica**  
El negocio carece de registros formales suficientes para demostrar reservas, cobros, servicios prestados y transacciones. Esto incrementa el riesgo ante auditorías, disputas con clientes o necesidades de crecimiento financiero.

**Precondiciones**
- Flujo basado en mensajes y capturas.
- Escasa sistematización contable.
- Emisión no estandarizada de soporte de venta.

**Impacto**
- Dificultad de conciliación.
- Riesgo de sanción o de soporte insuficiente ante requerimientos.
- Imposibilidad de construir historial confiable del negocio.

**Controles existentes**
- Evidencia informal en chats y aplicaciones.

**Debilidad del control actual**  
La evidencia existe, pero no está estructurada como sistema de trazabilidad.

**Tratamiento recomendado**
- Implementar soporte formal por reserva/venta.
- Organizar registro mínimo de servicios prestados y pagos.
- Adoptar herramientas básicas de contabilidad y facturación conforme corresponda.
- Integrar la evidencia comercial con la operativa.

**Comentario técnico**  
Este hallazgo no suele percibirse como “ciberseguridad”, pero sí es una debilidad seria de integridad, no repudio y gobierno del proceso.

---

## 🧨 Hallazgos estructurales del caso

Más allá de los 10 hallazgos puntuales, el caso presenta cinco causas raíz que explican la mayoría de los riesgos:

### 1. Falta de identidad digital formal
El negocio opera en canales válidos, pero sin suficiente institucionalización. Esto favorece la suplantación y dificulta que el cliente valide autenticidad.

### 2. Evidencia distribuida y no gobernada
La información relevante queda fragmentada entre chat, formulario, app de pagos y dispositivo. Esto impide una trazabilidad robusta.

### 3. Mezcla de ámbitos personal y empresarial
El negocio usa medios personales para cobrar, atender y custodiar datos. Esta mezcla amplifica riesgo financiero, operativo y de privacidad.

### 4. Exceso de dependencia del operador
El proceso no es resiliente. Si falla la persona o su dispositivo, falla el negocio.

### 5. Controles reactivos en lugar de preventivos
Los pocos controles actuales sirven para “reconstruir” o improvisar después del problema, no para evitar que ocurra.

---

## 🛡️ Estrategia de tratamiento recomendada

La recomendación no es desplegar una arquitectura costosa de inmediato, sino construir una **línea base de seguridad operacional**.

### Prioridad 1 — Inmediato (0 a 30 días)

| Acción | Riesgos que reduce | Justificación |
|---|---|---|
| Formalizar el canal oficial con WhatsApp Business y unificar el número visible en todas las redes | T01, T07, T08 | Reduce suplantación y mejora continuidad/comunicación |
| Verificar pagos en la app y no solo por captura | T03 | Cierra el principal hueco de integridad del recaudo |
| Restringir acceso a Forms/Sheets y revisar permisos | T04, T05 | Reduce exposición y alteración de consentimientos |
| Activar controles del dispositivo: bloqueo fuerte, cifrado, localización y borrado remoto | T06, T09, T08 | Protege el repositorio principal y mejora respuesta ante pérdida |
| Reducir recolección de datos y añadir aviso de privacidad | T04, T09 | Baja exposición y mejora tratamiento del dato |

### Prioridad 2 — Corto plazo (30 a 60 días)

| Acción | Riesgos que reduce | Justificación |
|---|---|---|
| Separar medio de pago del negocio y medio personal | T06, T10 | Mejora segregación financiera y auditabilidad |
| Crear carpeta/repositorio estructurado por reserva | T02, T05, T10 | Mejora evidencia y trazabilidad |
| Definir respaldo operativo con segundo responsable | T08 | Reduce el punto único de falla humano |
| Establecer formato estándar de confirmación de reserva | T02, T10 | Fortalece no repudio y soporte comercial |

### Prioridad 3 — Mediano plazo (60 a 90 días)

| Acción | Riesgos que reduce | Justificación |
|---|---|---|
| Introducir formulario o flujo de reservas más autogestionado | T02, T08, T10 | Reduce dependencia del chat como único sistema |
| Automatizar parcialmente confirmaciones y consolidación de evidencias | T02, T03, T10 | Eleva trazabilidad y disminuye error humano |
| Integrar contabilidad / facturación básica | T10, T06 | Mejora gobierno del proceso y crecimiento del negocio |

### Prioridad 4 — Evolución posterior (90+ días)

| Acción | Riesgos que reduce | Justificación |
|---|---|---|
| Diseñar un flujo integrado de reservas + pagos + consentimientos | T01–T10 | Reduce fragmentación sistémica |
| Definir política interna de retención de datos y respuesta a incidentes | T04, T09, T10 | Madura el gobierno del dato y la resiliencia |
| Establecer indicadores de seguridad operativa | T03, T08, T10 | Permite seguimiento y mejora continua |

---

## 🔍 Investigación complementaria y alineación con buenas prácticas

### 1. Uso de STRIDE y modelado de amenazas

La documentación oficial de Microsoft describe el threat modeling como un proceso de **crear un diagrama, identificar amenazas, mitigarlas y validar las mitigaciones**. También señala que el enfoque usa **STRIDE** para generar una lista de amenazas previsibles sobre el sistema. Esta lógica encaja con el caso analizado: el sistema de Élite Airsoft no es una aplicación monolítica, pero sí un proceso con componentes, flujos y fronteras de confianza. Por tanto, la aplicación del modelo es metodológicamente coherente.

### 2. Buenas prácticas para pequeñas empresas

La guía de CISA para pequeñas empresas enfatiza controles de alto impacto y relativa facilidad de adopción, como la protección de cuentas, preparación ante incidentes, respaldo y reducción de dependencias críticas. En el caso de Élite Airsoft, estas recomendaciones son especialmente pertinentes porque el negocio depende de pocos activos, pero muy concentrados: un canal, un operador, un dispositivo y una secuencia manual.

### 3. Protección de datos personales en Colombia

La Ley 1581 de 2012 define la autorización como el consentimiento **previo, expreso e informado** del titular y exige aplicar medidas de seguridad para evitar adulteración, pérdida, consulta, uso o acceso no autorizado. Esto incide directamente en el formulario de consentimiento, en la forma de presentar la finalidad del tratamiento y en la necesidad de restringir el acceso a las respuestas.

### 4. Facturación y trazabilidad de ventas

La DIAN indica que, si se es responsable de facturar, se debe hacerlo electrónicamente, salvo las excepciones legales. Más allá de la obligatoriedad puntual según la naturaleza y régimen del negocio, el principio relevante para este análisis es que la trazabilidad comercial no puede descansar indefinidamente en conversaciones de chat y capturas sueltas. El negocio necesita evidencia estructurada de sus servicios y cobros.

### 5. Controles prácticos sobre formularios y dispositivos

Google documenta opciones para limitar respuestas, controlar edición, definir acceso y evitar exposición innecesaria de resúmenes del formulario. Asimismo, Google permite encontrar, asegurar o borrar remotamente un dispositivo Android perdido, siempre que se haya preparado correctamente. Estos controles son directamente accionables en el contexto del operador.

### 6. Seguridad de cuentas y canal empresarial

WhatsApp documenta funciones de seguridad de cuenta y verificación en el contexto empresarial. Aunque la verificación o autenticación no elimina por sí sola la suplantación, sí contribuye a fortalecer la identidad del canal y a disminuir el riesgo de fraude basado en apariencia.

### 7. Estándares de protección de pagos

PCI DSS fue diseñado para entornos donde se almacenan, procesan o transmiten datos de pago. Aunque Élite Airsoft no parece procesar tarjetas directamente en el flujo evaluado, el estándar sigue siendo útil como referencia conceptual: la seguridad del cobro exige controles técnicos y operativos, no simple confianza en evidencia informal.

---

## ⚖️ Consideraciones de cumplimiento y gobierno

### Protección de datos
El negocio debería asumir, como mínimo, las siguientes obligaciones prácticas:
- informar finalidad del tratamiento,
- minimizar la recolección,
- limitar acceso,
- custodiar adecuadamente la información,
- evitar circulación innecesaria de datos por canales informales,
- definir retención y eliminación.

### Gobierno de identidad digital
La identidad digital del negocio debe tratarse como activo. Eso implica:
- un número oficial inequívoco,
- presencia coherente en redes,
- mensajes de validación del canal,
- respuesta ante perfiles clonados.

### Gobierno del recaudo
El proceso de cobro requiere:
- segregación de cuentas,
- verificación real de pago,
- soporte asociado a cada reserva,
- conciliación mínima.

### Continuidad operativa
La continuidad no puede depender solo de disponibilidad personal del dueño. Se requiere:
- respaldo humano,
- respaldo técnico,
- mensajes automáticos,
- contingencia ante pérdida del celular.

---

## 🧩 Arquitectura objetivo mínima recomendada

Sin cambiar por completo la operación del negocio, una arquitectura objetivo mínima podría verse así:

```text
[Cliente]
   ↓
[Instagram / Facebook oficial]
   ↓
[WhatsApp Business oficial]
   ├── mensaje de bienvenida + validación del canal
   ├── enlace al formulario con aviso de privacidad
   └── instrucciones de pago
        ↓
   [Formulario con acceso controlado]
        ↓
   [Hoja de respuestas restringida]
        ↓
[Verificación real del pago en cuenta exclusiva del negocio]
        ↓
[Confirmación estándar de reserva + evidencia archivada]
        ↓
[Repositorio mínimo de soportes / contabilidad básica]
```

Esta arquitectura no elimina todos los riesgos, pero sí reduce radicalmente la informalidad que hoy origina la mayoría de amenazas.

---

## ✅ Conclusiones

1. **El proceso crítico de Élite Airsoft presenta una exposición alta y transversal.**  
   La matriz muestra cobertura completa de STRIDE y una concentración de riesgos en identidad, integridad del cobro, privacidad de datos, trazabilidad y continuidad.

2. **La principal debilidad es sistémica y no puntual.**  
   El negocio no falla por una vulnerabilidad única, sino por operar un flujo crítico sobre herramientas dispersas, cuentas personales y validaciones manuales.

3. **Los riesgos críticos son perfectamente plausibles.**  
   No dependen de atacantes altamente sofisticados; varios pueden materializarse por error humano, abuso oportunista, pérdida del celular o engaño simple al operador o al cliente.

4. **Los quick wins ofrecen una mejora fuerte con baja complejidad.**  
   Formalizar el canal, verificar pagos correctamente, restringir permisos, reducir exposición de datos y preparar el dispositivo del operador produciría una reducción sustancial del riesgo.

5. **La seguridad aquí también es operación, evidencia y gobierno.**  
   En este caso, ciberseguridad no se limita a contraseñas o cifrado; incluye identidad digital, soporte comercial, trazabilidad, protección de datos y continuidad del negocio.

6. **La evolución deseable es hacia un flujo más integrado y menos manual.**  
   No es imprescindible construir una plataforma compleja de inmediato, pero sí avanzar hacia una operación donde reserva, consentimiento, pago y evidencia estén mejor conectados y gobernados.

En síntesis, la aplicación de STRIDE fue útil porque permitió traducir un proceso informal en un mapa claro de amenazas accionables. El caso demuestra que, para pequeños negocios digitales, la mejora de seguridad más importante suele comenzar no con tecnología sofisticada, sino con **controles básicos bien diseñados y correctamente aplicados**.

---

## 📚 Referencias

1. Microsoft. *Getting Started - Microsoft Threat Modeling Tool*. Microsoft Learn.  
   https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-getting-started  
   Fecha de consulta: 25/03/2026.

2. Microsoft. *Threats - Microsoft Threat Modeling Tool*. Microsoft Learn.  
   https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-threats  
   Fecha de consulta: 25/03/2026.

3. CISA. *Cyber Guidance for Small Businesses*. Cybersecurity and Infrastructure Security Agency.  
   https://www.cisa.gov/cyber-guidance-small-businesses  
   Fecha de consulta: 25/03/2026.

4. Departamento Administrativo de la Función Pública. *Ley 1581 de 2012*. Gestor Normativo.  
   https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=49981  
   Fecha de consulta: 25/03/2026.

5. Departamento Administrativo de la Función Pública. *Decreto 1377 de 2013*. Gestor Normativo.  
   https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=53646  
   Fecha de consulta: 25/03/2026.

6. DIAN. *¿Debe facturar electrónicamente?*  
   https://micrositios.dian.gov.co/sistema-de-facturacion-electronica/debes-facturar-electronicamente/  
   Fecha de consulta: 25/03/2026.

7. Google. *Publish & share your form with responders*. Google Docs Editors Help.  
   https://support.google.com/docs/answer/2839588?hl=en  
   Fecha de consulta: 25/03/2026.

8. Google. *Find, secure, or erase a lost Android device*. Google Account Help.  
   https://support.google.com/accounts/answer/6160491?hl=en  
   Fecha de consulta: 25/03/2026.

9. WhatsApp. *About verified business accounts*. WhatsApp Help Center.  
   https://faq.whatsapp.com/794517045178057  
   Fecha de consulta: 25/03/2026.

10. WhatsApp. *How to manage two-step verification settings*. WhatsApp Help Center.  
    https://faq.whatsapp.com/1920866721452534  
    Fecha de consulta: 25/03/2026.

11. PCI Security Standards Council. *PCI Data Security Standard (PCI DSS)*.  
    https://www.pcisecuritystandards.org/standards/pci-dss/  
    Fecha de consulta: 25/03/2026.

12. Élite Airsoft. *Matriz STRIDE del caso analizado y caracterización del proceso crítico*. Documento de trabajo del taller.