# Lenguaje de Dominio: Vocabulario del Proyecto

> 📝 **Nota de Plantilla:** Reemplazá los ejemplos con tus términos de dominio reales. Esto se vuelve más valioso a medida que tu proyecto crece.

Este documento define términos y conceptos clave para tu proyecto. Un vocabulario compartido reduce la confusión y hace la comunicación más clara entre miembros del equipo y en el código.

---

## Propósito

El lenguaje del dominio establece:
- **Naming consistente** en código, docs y conversaciones
- **Entendimiento compartido** de conceptos clave
- **Límites claros** entre diferentes partes del sistema
- **Ambigüedad reducida** en requisitos y discusiones

---

## Cómo Usar Este Archivo

1. **Agregá términos conforme emergen** - No intentes definir todo por adelantado
2. **Definilos claramente** - ¿Qué significa este término en *tu* dominio?
3. **Mantené definiciones cortas** - Una o dos oraciones generalmente es suficiente
4. **Usá términos consistentemente** - En código, docs, tests y conversaciones
5. **Actualizá cuando el entendimiento cambie** - Refiná definiciones conforme aprendés

---

## Términos Centrales del Dominio

Define los conceptos clave en tu dominio. Ejemplos:

**Usuario**
Una persona con una cuenta que puede ingresar y acceder al sistema.

**Administrador**
Un usuario con privilegios elevados que puede gestionar otros usuarios y configuraciones del sistema.

**Sesión**
Un período de interacción autenticada entre un usuario y el sistema, típicamente terminando después de timeout o logout.

**Transacción**
Una operación atómica que o bien tiene éxito completamente o falla completamente, manteniendo consistencia de datos.

---

## Conceptos de Negocio

Define términos específicos del negocio. Ejemplos:

**Orden**
Una solicitud del cliente para comprar uno o más productos, incluyendo información de envío y pago.

**Inventario**
La cantidad actual de cada producto disponible para venta.

**Fulfillment**
El proceso de preparar y enviar una orden a un cliente.

---

## Términos Técnicos

Define conceptos técnicos específicos de tu arquitectura. Ejemplos:

**Repository**
Una interfaz para acceder y persistir objetos de dominio, abstrayendo detalles de almacenamiento de datos.

**Service**
Un componente que coordina operaciones de negocio a través de múltiples objetos de dominio.

**Event**
Una notificación de que algo significativo sucedió en el sistema, disparando acciones posteriores.

---

## Lenguaje del Dominio vs. Lenguaje del Usuario

El **lenguaje del dominio** es para el **equipo** (desarrolladores + expertos del negocio). Es preciso, refleja cómo modelamos el problema y guía el diseño del código.

El **lenguaje del usuario** es para la **interfaz**. Es amigable, familiar y optimizado para la comprensión del usuario final.

**Estos son dos lenguajes distintos con propósitos distintos.**

### Ejemplo:

| Contexto | Lenguaje |
|----------|----------|
| **Código (dominio)** | `OrderFulfillmentService.processShipment()` |
| **UI (usuario)** | "Preparando tu envío" |

### Cuándo Adaptarlo:

- Términos de industria que confunden al usuario general
- Conceptos técnicos necesarios internamente pero irrelevantes externamente
- Jerga del negocio que el usuario no maneja
- Siglas o acrónimos específicos del equipo

### La Clave:

El dominio guía el **diseño del código**. La UI se adapta al **usuario**. Esto no es inconsistencia—es claridad arquitectónica: cada lenguaje sirve a su audiencia.

**Ejemplo de confusión evitada:**
- ❌ Mostrar "XOR operation" en la UI (técnico, incomprensible)
- ✅ Mostrar "Combinar modos" o "Diferencia" (claro para el usuario)

---

## Lenguaje Ubicuo

Usá estos términos en todos lados **dentro del equipo**:
- ✅ En código: nombres de clases, funciones, variables
- ✅ En tests: nombres y descripciones
- ✅ En documentación: READMEs, comentarios, guías
- ✅ En conversaciones: discusiones del equipo, requisitos

Cuando el código y las conversaciones usan palabras distintas para el mismo concepto, la confusión es inevitable. Alineá tu lenguaje internamente.

---

## Anti-Glossario: Términos a Evitar

Lista términos vagos o sobrecargados que causan confusión:

**❌ "Procesar"** - Demasiado vago. Usá verbos específicos: validar, calcular, enviar, etc.
**❌ "Manager"** - Generalmente significa que una clase está haciendo demasiado. Sé más específico.
**❌ "Datos"** - ¿Qué tipo de datos? ¿Usuario? ¿Orden? ¿Configuración?
**❌ "Manejar"** - ¿Manejar cómo? ¿Parsear? ¿Validar? ¿Almacenar? Sé explícito.

---

## Entrada de Plantilla

Al agregar nuevos términos, usá este formato:

**[Nombre del Término]**
[Una oración definiéndolo en tu dominio.]
[Opcional: ejemplo de uso o aclaración.]

---

## Empezando

1. Empezá con 5-10 términos centrales de tu dominio
2. Agregá nuevos términos cuando aparezcan en múltiples lugares
3. Actualizá definiciones cuando tu entendimiento evolucione
4. Repasá este archivo cuando onboardeás nuevos miembros del equipo
5. Referencialó durante discusiones de diseño

---

*Este es un documento vivo. A medida que tu proyecto crece y el entendimiento se profundiza, tu lenguaje de dominio evolucionará. Mantelo actualizado y mantelo simple.*
