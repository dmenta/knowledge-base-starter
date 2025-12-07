# Registros de Decisiones Arquitectónicas (ADRs)

> 📝 **Nota de Plantilla:** Registrá tus decisiones reales acá. El ejemplo abajo muestra el formato - reemplazalo con tus ADRs reales.

Este documento captura decisiones arquitectónicas y de diseño importantes para el proyecto. Registrar decisiones ayuda a futuras contribuyentes (incluyendo tu yo futuro) a entender por qué las cosas son como son.

---

## ¿Por Qué Documentar Decisiones?

**El contexto se desvanece rápido**
- Lo que pareció obvio en el momento se vuelve misterioso después
- Sin contexto, los cambios se revierten o se repiten

**Las decisiones tienen consecuencias**
- Entender los tradeoffs previene "mejoras" ingenuas que salen mal
- Nuevos miembros del equipo pueden ver el razonamiento detrás de la arquitectura actual

**El aprendizaje se compone**
- Revisar decisiones pasadas revela patrones
- Los errores se vuelven lecciones cuando están documentados

---

## Jerarquía de Decisiones

No todas las decisiones tienen el mismo peso. La jerarquía define cuánta flexibilidad hay para desviarse:

**🔴 CRÍTICAS (Must Follow)**
- Decisiones de seguridad, privacidad, cumplimiento normativo
- Integraciones con terceros que no son reversibles fácilmente
- Decisiones que protegen la estabilidad del dominio
- **Desviación:** Prácticamente nunca, salvo circunstancias extraordinarias documentadas
- **Ejemplo:** "Siempre validar datos de entrada" - no hay excepciones

**🟡 ARQUITECTÓNICAS (Should Follow)**
- Separación de capas, inversión de control
- Patrones de diseño que mejoran mantenibilidad
- **Desviación:** Solo si el caso es excepcional y queda explícitamente documentado
- **Ejemplo:** Repository Pattern - generalmente sí, pero si necesitás una query puntual rápida y lo documentás, puede valer

**🟢 CONTEXTUALES (Consider, But Flexible)**
- Decisiones ligadas a terceros y sus limitaciones
- Trade-offs pragmáticos vs. ideales
- Decisiones que dependen del estado/momento del proyecto
- **Desviación:** Permitida si el contexto lo justifica
- **Ejemplo:** "Usamos librería X para pagos porque integra con nuestro ERP, pero evaluaremos cambiarla si surge mejor opción"

**🔵 APRENDIDAS (Lessons Learned)**
- "Intentamos Y, no funcionó, acá está por qué"
- Sirven para no repetir errores
- Son informativas, no prescriptivas
- **Ejemplo:** "Evitar hacer calls a terceros en el constructor - genera timeouts"

---

## Cuándo Documentar una Decisión

Registrá decisiones que:
- **Afecten arquitectura** - Estructura, capas, componentes mayores
- **Involucren tradeoffs** - Elegiste un enfoque sobre alternativas
- **Sean controvertidas** - El equipo debatió el mejor enfoque
- **Constriñan trabajo futuro** - Decisiones posteriores dependen de esta
- **Podrían sorprender a otros** - "¿Por qué lo hicieron así?"

No documentes:
- Elecciones triviales u obvias
- Decisiones fácilmente reversibles
- Prácticas estándar o patrones

---

## Template de Decisión

Usá este formato para cada decisión:

### [Título de la Decisión] - [Fecha]

**Jerarquía:** 🔴 Crítica / 🟡 Arquitectónica / 🟢 Contextual / 🔵 Aprendida

**Contexto**
¿Qué situación forzó esta decisión? ¿Qué problema estamos resolviendo?

**Decisión**
¿Qué decidimos hacer?

**Alternativas Consideradas**
¿Qué otras opciones evaluamos?
- Opción A: [descripción y por qué la rechazamos]
- Opción B: [descripción y por qué la rechazamos]

**Consecuencias**
¿Cuáles son los resultados positivos y negativos de esta decisión?
- **Beneficios:** ¿Qué ganamos?
- **Trade-offs:** ¿Qué perdemos o qué se vuelve más difícil?
- **Riesgos:** ¿Qué podría salir mal?

**Estado**
Activa | Supersedida por [Decisión #] | Deprecada

---

## Ejemplo de Registro de Decisión

### Usar Repository Pattern para Acceso a Datos - 2024-01-15

**Jerarquía:** 🟡 Arquitectónica

**Contexto**
Necesitamos persistir usuarios, órdenes y productos. El código actual usa queries de base de datos dispersas por toda la lógica de negocio, haciendo el testing difícil y acoplando la lógica de dominio a SQL.

**Decisión**
Implementar Repository pattern para abstraer acceso a datos. Cada objeto de dominio obtiene una interfaz repository (UserRepository, OrderRepository) implementada por repositorios concretos de base de datos.

**Alternativas Consideradas**
- **Active Record:** Los objetos se guardan a sí mismos. Rechazado porque acopla fuertemente la lógica de dominio a la persistencia.
- **SQL directo en todos lados:** Enfoque actual. Rechazado porque hace el testing difícil y viola separación de responsabilidades.
- **ORM sin abstracción:** Usar ORM directamente en lógica de negocio. Rechazado porque sigue acoplando a una librería ORM específica.

**Consecuencias**
- **Beneficios:** La lógica de negocio se vuelve testeable con repositorios mock. Se puede intercambiar bases de datos sin cambiar el código de dominio. Separación clara de responsabilidades.
- **Trade-offs:** Capa de abstracción extra agrega cierta complejidad. Más archivos para mantener.
- **Riesgos:** Sobre-abstracción si los repositorios se vuelven demasiado genéricos. Es necesario mantener interfaces enfocadas.

**Estado**
Activa

---

## Decisiones sobre Terceros

Las integraciones con productos o servicios externos merecen documentación especial:

**Qué Capturar:**
- Qué tercero, por qué lo elegimos
- Qué dependencias trae (técnicas, comerciales, operacionales)
- Cómo mitigamos el acoplamiento (inversión de control, adapters, etc.)
- Qué límites tiene (rate limits, features no disponibles, etc.)
- Cuándo fue cuestionada/evaluada (revisiones periódicas)
- Escenarios de fallback o plan B

**Ejemplo:**

### Proveedor de Pagos (Stripe) - 2024-01-20

**Jerarquía:** 🟡 Arquitectónica

**Contexto**
Necesitamos procesar pagos con tarjeta de crédito. Evaluamos varios proveedores para Argentina.

**Decisión**
Usar Stripe por integración robusta con Argentina, webhooks confiables y buena documentación.

**Mitigación del Acoplamiento:**
- Definir interfaz PaymentProcessor en dominio
- Implementación StripePaymentProcessor en infraestructura
- Dominio no conoce detalles de Stripe (recibe Stripe SDK solo en infraestructura)
- Tests del dominio usan mock PaymentProcessor

**Límites y Riesgos:**
- Rate limit: 100 requests/segundo (mitigado con queue)
- Comisión: 2.9% + $0.30 por transacción
- Disponibilidad: 99.9% SLA
- Riesgo: Si Stripe cae, los pagos se ponen en queue y se reintenta

**Alternativas Consideradas:**
- MercadoPago: Mejor comisión pero peor documentación API
- Decidí Uno: Integración argentina nativa pero menos flexible

**Estado**
Activa - Revisar anualmente

---

## Tus Registros de Decisión

Empezá agregando tus decisiones abajo:

---

### [Tu Primera Decisión] - [Fecha]

**Jerarquía:** [Seleccionar]

**Contexto**
[¿Por qué necesitabas tomar esta decisión?]

**Decisión**
[¿Qué elegiste hacer?]

**Alternativas Consideradas**
- Opción 1: [Descripción y por qué rechazada]

**Consecuencias**
- **Beneficios:**
- **Trade-offs:**
- **Riesgos:**

**Estado**
Activa

---

## Tips para Escribir Buenos ADRs

**Sé conciso** - Apuntá a claridad, no completitud. Una página es ideal.

**Capturá alternativas** - Mostá que consideraste las opciones reflexivamente.

**Enfocate en el "por qué"** - La decisión en sí es visible en el código; explicá el razonamiento.

**Actualizá el estado** - Cuando las decisiones cambian, marcalas como supersedidas en lugar de eliminarlas.

**Escribí poco después de decidir** - Capturá el contexto mientras está fresco.

**Protegé contra experiencias no vividas** - Las reglas rígidas (Críticas y Arquitectónicas) salvan proyectos de errores que requieren años para entender. Respetá la intención detrás de ellas.

---

*Los registros de decisiones son más valiosos cuando se revisan. Revisalos cuando tomes decisiones relacionadas, al onboardear nuevos miembros del equipo, o al evaluar si cambiar de dirección.*
