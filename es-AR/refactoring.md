# Refactoring: Cuándo y Cómo

Refactorizar es mejorar la estructura del código sin cambiar el comportamiento. Es un acto de cuidado—hacer el código más claro, más mantenible y más fácil de extender.

---

## Cuándo Refactorizar

**Siempre Refactorizar Cuando:**
- Los tests están en verde y ves una mejora
- Acabás de hacer pasar un test y el código puede ser mejor
- Apareció duplicación
- Emergió un nuevo concepto que merece un nombre

**La Regla de la Barra Verde:**
- Solo refactorizá cuando todos los tests estén en verde
- Si los tests están en rojo, primero pongalos en verde
- Si rompés tests mientras refactorizás, deshacé y tomá un paso más chico
- Nunca mezcles refactoring con agregar features

**No Refactorizar Cuando:**
- Los tests están fallando (primero llegá a verde)
- No tenés tests (escribilos primero)
- Estás adivinando necesidades futuras (YAGNI—You Ain't Gonna Need It)

---

## Las Reglas de Oro del Refactoring

**1. Nunca refactorices en rojo—solo en verde**
Los tests deben pasar antes de refactorizar. Si no pasan, primero hacelos pasar.

**2. Commiteá después de cada refactor exitoso**
Cuando los tests están en verde después de refactorizar, commiteá inmediatamente. Esto crea puntos de control de seguridad.

**3. Nunca refactorices y agregues features al mismo tiempo**
Refactorizá O agregá funcionalidad, nunca ambas.

**El Ritmo:**
1. Escribí un test que falle (RED)
2. Hacelo pasar con código simple (GREEN)
3. Refactorizá para mejorar el diseño (REFACTOR)
4. Ejecutá tests para confirmar que siguen en verde
5. Commiteá con un mensaje claro
6. Repetí para el siguiente test

Este ritmo crea seguridad, claridad y progreso continuo.

---

## Patrones Comunes de Refactoring

**Extract Method/Function**
- Rompé funciones grandes en otras más pequeñas y enfocadas
- Dale a cada pieza un nombre descriptivo
- Mejora la legibilidad y reusabilidad

**Rename**
- Actualizá nombres para reflejar el entendimiento actual
- Mejores nombres hacen el código auto-documentado
- No tengas miedo de cambiar nombres a medida que crece el entendimiento

**Extract Class**
- Cuando una clase hace demasiado, dividila
- Cada clase debería tener una responsabilidad clara
- Hace el código más fácil de testear y modificar

**Simplificar Condicionales**
- Extraé condiciones complejas en funciones bien nombradas
- Usá cláusulas de guarda para reducir anidamiento
- Aplaná estructuras profundamente anidadas

**Eliminar Duplicación**
- No te repitas (principio DRY)
- Extraé código repetido en funciones compartidas
- Pero no te obsesiones—algo de duplicación es aceptable si las abstracciones serían forzadas

---

## Proceso Seguro de Refactoring

1. **Verificar barra verde** - Todos los tests deben pasar antes de refactorizar
2. **Hacer un cambio pequeño** - Extraer un método, renombrar una variable, etc.
3. **Ejecutar tests inmediatamente** - Verificar que el comportamiento no cambió
4. **Si verde, commitear** - Preservar este punto de control
5. **Si rojo, deshacer** - Tomar un paso más chico
6. **Repetir** - Mejoras pequeñas, commiteadas frecuentemente

**Cada commit representa:**
- Un estado estable y funcionando
- Una mejora lógica
- Un punto seguro de rollback si es necesario

**Los mensajes de commit deberían describir qué mejoró:**
- "Extraer método calcularDescuento"
- "Renombrar userId a customerId para claridad"
- "Eliminar duplicación en lógica de validación"

---

## Señales de Alarma: Code Smells

Estos patrones sugieren que el código podría beneficiarse de refactoring:

- **Funciones largas** - Difícil de entender qué está pasando
- **Clases grandes** - Intentando hacer demasiado
- **Listas largas de parámetros** - Considerá un objeto o configuración
- **Código duplicado** - Los cambios requieren actualizaciones en múltiples lugares
- **Código muerto** - Funciones o variables sin usar agregan confusión
- **Comentarios explicando qué hace el código** - El código debería ser auto-explicativo
- **Condicionales complejos** - Difícil de rastrear la lógica
- **Acoplamiento fuerte** - Cambios en un lugar fuerzan cambios en otro

---

## Mentalidad de Refactoring

**El Refactoring es Continuo**
- Sucede después de que cada test pasa
- No es una fase separada—es parte del ciclo red-green-refactor
- Refactorings pequeños y frecuentes previenen los grandes y aterradores

**Escuchá al Código**
- El refactoring revela el diseño que quiere emerger
- No fuerces abstracciones—dejá que aparezcan naturalmente
- La duplicación está bien hasta que veas el patrón (Regla de Tres)

**La Disciplina de Commit Crea Seguridad**
- Cada refactor verde se commitea
- Commits pequeños significan rollback fácil
- Commits frecuentes significan nunca perder mucho trabajo
- Mensajes claros significan entender la historia después

**Confiá en Tus Tests**
- Barra verde significa que podés refactorizar sin miedo
- Los tests atrapan errores inmediatamente
- Sin tests, refactorizar es adivinar

---

*Refactorizar hace el trabajo futuro más fácil. Invertí un poco de tiempo ahora para ahorrar mucho tiempo después. Ver [testing.md](testing.md) para asegurar refactoring seguro.*
