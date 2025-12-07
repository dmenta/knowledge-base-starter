# Filosofía de Desarrollo

> 📝 **Nota de Plantilla:** Personalizá esto para reflejar los valores y prácticas reales de tu equipo.

Este documento captura nuestras creencias y valores centrales sobre el desarrollo de software. Estos principios guían nuestras decisiones y moldean cómo abordamos los problemas.

---

## Valores Centrales

**Claridad Ante Todo**
- El código se lee mucho más de lo que se escribe
- Escribí para la próxima persona (a menudo tu yo futuro)
- La claridad es un acto de amabilidad hacia tus colaboradores
- Las soluciones simples suelen ser mejores que las ingeniosas

**La Calidad es Incremental**
- El código perfecto no existe, pero el código mejor sí
- Las pequeñas mejoras se componen con el tiempo
- Dejá el código más limpio de lo que lo encontraste
- Progreso sobre perfección

**Entender Antes de Construir**
- No empieces a codificar hasta que entiendas el problema
- Hacé preguntas cuando los requisitos no estén claros
- Explorá el dominio antes de saltar a las soluciones
- A veces el mejor código es el código que no escribís

---

## Cómo Construimos Software

**Test-First, Siempre**
- Cada feature empieza con un test que falla
- Un test a la vez—enfocate, implementá, refactorizá
- Los tests revelan el diseño; no luches contra ellos
- Red-green-refactor es nuestro ritmo (ver [testing.md](testing.md))

**Trabajá en Pasos Pequeños**
- Escribí un test, hacelo pasar, refactorizá, commiteá
- Nunca refactorices en rojo—primero llegá a verde
- Commiteá después de cada refactor exitoso
- Los pasos pequeños hacen que los problemas sean más fáciles de debuguear

**Dejá que el Diseño Emerja**
- No diseñes todo por adelantado
- Escribí el test, escribí el código más simple, refactorizá para revelar patrones
- El diseño emerge a través del paso de refactorización
- Confiá en el proceso—la sobreingeniería viene de saltarse pasos

**Diseño Orientado al Dominio**
- Modelá el dominio del negocio en código
- Usá el lenguaje del dominio en todos lados (ver [domain-language.md](domain-language.md))
- Las reglas de negocio viven en objetos de dominio
- Mantené las preocupaciones de infraestructura en los bordes

---

## Principios de Diseño

**Modelo de Dominio Puro (DDD)**
- Las reglas de negocio pertenecen a los objetos de dominio, no a los servicios
- Los objetos de dominio no tienen dependencias de infraestructura
- Mantené el núcleo puro—sin bases de datos, sin HTTP, sin frameworks
- Los servicios coordinan; los objetos de dominio deciden
- El modelo de dominio retorna valores o lanza excepciones de dominio
- Esto hace que testear sea trivial y el razonamiento claro

**Separación de Responsabilidades**
- Capa de dominio: lógica de negocio pura, sin dependencias externas
- Capa de servicio: coordinación, orquestación y protección de límites
- Capa de infraestructura: bases de datos, APIs, sistemas externos
- Excepciones en los límites de servicios (validar entrada, atrapar excepciones de dominio)
- Límites claros hacen que testear y cambiar sea fácil

**Claridad**
- Hacé obvias las dependencias y relaciones
- El comportamiento implícito genera confusión
- Preferí verboso y claro sobre conciso e ingenioso

**Testeabilidad**
- Si es difícil de testear, probablemente esté mal diseñado
- Modelo de dominio puro = testeo fácil, sin necesidad de mocks
- Los tests guían hacia una mejor arquitectura

---

## Lo Que Valoramos

**Comportamiento Sobre Implementación**
- Lo que el código hace importa más que el cómo
- Testeá comportamiento, no detalles de implementación
- La implementación puede cambiar; el comportamiento debería permanecer estable
- Enfocate en contratos e interfaces, no en internos

**Descubrimiento Sobre Planificación**
- Los tests revelan lo que el código necesita ser
- El refactoring revela la abstracción correcta
- Los pasos pequeños revelan el camino a seguir
- Confiá en la emergencia sobre el diseño anticipado

**Disciplina Sobre Improvisación**
- Red-green-refactor: sin atajos
- Un test a la vez: resistí la urgencia de saltarte pasos
- Commiteá después de refactorizar: preservá el progreso
- El ritmo produce calidad

**Claridad de Dominio**
- Usá el lenguaje del dominio del negocio
- Reglas de negocio en objetos de dominio, no dispersas en servicios
- El modelo de dominio puro hace todo más fácil
- El código debería leerse como habla el experto del dominio

**Filosofía de Manejo de Errores**
- Los objetos de dominio lanzan excepciones por reglas de negocio violadas
- Los servicios atrapan y manejan excepciones en los límites
- No dejes que las excepciones se filtren a través de las capas arquitectónicas
- Hacé que los mensajes de error sean útiles para debuguear

---

## Nuestro Compromiso

Nos esforzamos por:
- Construir sistemas que sean fáciles de entender y cambiar
- Tomar decisiones reflexivas y documentarlas (ver [decisions.md](decisions.md))
- Testear nuestras suposiciones y verificar nuestro trabajo
- Aprender continuamente y actualizar nuestras prácticas
- Colaborar con respeto y curiosidad

Reconocemos:
- No todo el código será perfecto
- A veces el pragmatismo supera al principio
- La deuda técnica sucede—gestionala conscientemente
- El contexto importa—adaptá los principios a la situación

---

*Estos son ideales a los que aspirar, no reglas rígidas. Usá juicio, adaptate al contexto, y siempre priorizá entregar valor.*
