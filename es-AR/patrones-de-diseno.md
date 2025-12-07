# Patrones de Diseño: Soluciones Preferidas

> 📝 **Nota de Plantilla:** Reemplazá estos ejemplos con patrones que tu equipo realmente use. Eliminá este archivo si los patrones no son un foco.

Este documento lista patrones de diseño que encontramos útiles y cuándo aplicarlos. Los patrones son herramientas, no reglas—usalos cuando resuelvan un problema real, no porque sean ingeniosos.

---

## Cuándo Usar Patrones

**Sí Usar Patrones Cuando:**
- Reconocés un problema recurrente
- El patrón simplifica la solución
- Los miembros del equipo van a entender el patrón
- El patrón hace que los cambios futuros sean más fáciles

**No Usar Patrones Cuando:**
- Existe una solución más simple
- Estás aplicando patrones por sí mismos
- El problema no coincide con la intención del patrón
- El patrón agrega complejidad innecesaria

---

## Patrones Creacionales

**Factory Method**
- **Cuándo:** Necesitás crear objetos sin especificar la clase exacta
- **Beneficio:** Flexibilidad en la creación de objetos
- **Ejemplo:** Crear diferentes tipos de reportes, notificaciones o parsers

**Builder**
- **Cuándo:** Construir objetos complejos paso a paso
- **Beneficio:** Construcción de objetos clara y legible
- **Ejemplo:** Construir objetos de configuración, queries o datos de prueba

---

## Patrones Estructurales

**Adapter**
- **Cuándo:** Necesitás hacer que interfaces incompatibles trabajen juntas
- **Beneficio:** Integrar librerías de terceros sin cambiar tu código
- **Ejemplo:** Envolver APIs externas, convertir formatos de datos

**Inversión de Control (IoC)**
- **Cuándo:** Siempre—es un principio arquitectónico fundamental
- **Beneficio:** Dominio puro, independiente de infraestructura, altamente testeable
- **Cómo:** Las dependencias fluyen HACIA el dominio, no DESDE él
- **Implementación:** Dependency Injection (DI) - pasar dependencias explícitamente por constructor
- **Ejemplo:** El dominio define interfaces, la infraestructura las implementa y las instancia
- **Nota:** Podés lograr IoC sin containers—simplemente instanciando en la capa de infraestructura
- **Importancia:** Posiblemente el principio más importante para código testeable y mantenible

**Repository**
- **Cuándo:** Necesitás separar acceso a datos de lógica de negocio
- **Beneficio:** La lógica de negocio no sabe sobre bases de datos
- **Ejemplo:** UserRepository, OrderRepository abstraen el almacenamiento de datos

---

## Patrones de Comportamiento

**Strategy**
- **Cuándo:** Necesitás intercambiar algoritmos o comportamientos en runtime
- **Beneficio:** Flexibilidad sin condicionales
- **Ejemplo:** Diferentes algoritmos de ordenamiento, procesadores de pago o reglas de validación

**Template Method**
- **Cuándo:** La estructura del algoritmo permanece igual, pero los pasos varían
- **Beneficio:** Reusar estructura común, personalizar partes específicas
- **Ejemplo:** Pipelines de procesamiento de datos, setup/teardown de tests

**Observer**
- **Cuándo:** Los objetos necesitan reaccionar a cambios en otros objetos
- **Beneficio:** Bajo acoplamiento entre componentes
- **Ejemplo:** Sistemas de eventos, actualizaciones de UI, sistemas de notificación

---

## Patrones que Favorecemos

Listá los patrones que tu equipo usa más frecuentemente y guía específica sobre cómo preferís implementarlos. Ejemplos:

- **Inversión de Control**: Preferir inyección por constructor para dependencias requeridas
- **Repository Pattern**: Mantener repositorios enfocados en una única raíz de agregado
- **Strategy Pattern**: Usar cuando tenés 3+ ramas condicionales haciendo cosas similares
- **Factory Method**: Mejor que constructores complejos o múltiples sobrecargas de constructor

---

## Anti-Patrones a Evitar

**God Objects**
- Clases que saben o hacen demasiado
- **En su lugar:** Dividir en clases enfocadas con responsabilidad única

**Abstracción Prematura**
- Crear patrones antes de necesitarlos
- **En su lugar:** Esperar hasta que veas el patrón emerger naturalmente (Regla de Tres)

**Obsesión por Patrones**
- Usar patrones porque existen, no porque ayuden
- **En su lugar:** Empezar simple, agregar patrones cuando la complejidad lo demande

---

## Aprender Más

Cuando enfrentás un desafío de diseño:
1. Entendé el problema completamente primero
2. Considerá si existe una solución simple
3. Si la complejidad persiste, explorá patrones relevantes
4. Aplicá el patrón, luego refactorizá basado en el uso real
5. Documentá tu decisión en [decisions.md](decisions.md)

---

*Actualizá este archivo a medida que descubrís patrones que funcionan bien para tu equipo y dominio. Eliminá patrones que no agreguen valor. Hacelo tuyo.*
