# 🛠️ Taller 5: Evaluación de Seguridad con STRIDE

## 🎯 Objetivo

Analizar los riesgos de seguridad en una parte crítica del sistema usando el marco STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege).

---

taller-05-seguridad-stride/
├── README.md
├── clase/
│   ├── tabla-stride-clase.xlsx
│   └── notas.md
├── entrega/
│   ├── tabla-stride-cliente.xlsx
│   ├── informe.md
│   └── referencias.md
## 🎓 Caso base de referencia: EdukIT (Plataforma de Educación Virtual)

EdukIT es una plataforma de educación en línea que ofrece cursos certificados para estudiantes en América Latina. Administra el acceso a contenido educativo, evaluaciones, interacción con docentes y pagos por suscripción. El sistema gestiona información sensible como historial académico, datos personales, medios de pago y actividad del usuario. Evaluar la seguridad de estos procesos a través de un marco como STRIDE permite anticipar amenazas como suplantación, filtración de datos o accesos no autorizados, y diseñar estrategias de mitigación alineadas con las necesidades de protección de la información educativa.

**Contexto:**
- EdukIT es una plataforma de educación online que permite a estudiantes acceder a cursos, a docentes subir contenidos y a administradores gestionar pagos y certificados.
- El sistema maneja información personal, pagos, calificaciones y control de acceso.

**Elementos sensibles para evaluar:**

- Acceso de estudiantes a cursos y materiales
- Publicación de contenidos por parte de docentes
- Procesamiento de pagos con terceros
- Almacenamiento de datos personales y notas académicas
- Roles: Estudiante, Docente, Administrador

---

## 🧪 Parte 1: Trabajo en Clase

Durante la clase se espera que el equipo:

- Seleccione uno de los flujos críticos del sistema EdukIT.
- Aplique el marco STRIDE sobre ese flujo usando una tabla de análisis de amenazas.
- Identifique vulnerabilidades, impactos posibles y estrategias de mitigación.
- Registre todo en una tabla editable y justifique sus hallazgos.

---

## 🧠 Parte 2: Aplicación al Cliente Real

Después de la clase, el equipo debe:

- Aplicar STRIDE sobre un proceso o componente crítico del sistema del cliente real.
- Elaborar una tabla con amenazas, impactos, controles propuestos y nivel de riesgo.
- Redactar un informe explicando el análisis de seguridad.
- Investigar buenas prácticas de seguridad aplicadas al sector del cliente (educación, salud, logística, etc.).

---

## 📁 Estructura esperada del repositorio

```
taller-05-seguridad-stride/
├── README.md
├── clase/
│   ├── tabla-stride-clase.xlsx
│   └── notas.md
├── entrega/
│   ├── tabla-stride-cliente.xlsx
│   ├── informe.md
│   └── referencias.md
```

---

## 📤 Entregables

- Tabla STRIDE aplicada al sistema del cliente
- Informe técnico de análisis de seguridad
- Referencias de buenas prácticas en ciberseguridad

---

## 📊 Rúbrica de Evaluación

| Criterio                            | Excelente (5)                                                           | Aceptable (3) / Insuficiente (1–2)                      |
|-------------------------------------|--------------------------------------------------------------------------|----------------------------------------------------------|
| Análisis STRIDE (caso base)         | Tabla clara con amenazas reales y mitigación justificada                | Análisis superficial o incompleto                       |
| Aplicación al cliente real          | Adaptación precisa del marco al sistema del cliente                     | Adaptación genérica o sin profundidad técnica           |
| Documentación e interpretación      | Informe bien estructurado con impacto y priorización                    | Informe pobre o sin análisis crítico                    |
| Investigación complementaria        | Buenas prácticas y normativas citadas según el dominio del cliente      | Sin referencias o desconectado del contexto             |

---

## ✅ Licencia

Este taller hace parte del curso de Arquitectura Empresarial - Universidad de La Sabana. Uso académico bajo licencia MIT.
