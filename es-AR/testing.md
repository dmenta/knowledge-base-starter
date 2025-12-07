# Testing: Desarrollo Test-First

Practicamos desarrollo estricto test-first usando el ciclo red-green-refactor. Los tests no son solo verificación—son herramientas de diseño que revelan cómo el código quiere ser moldeado.

---

## El Ciclo Red-Green-Refactor

**Un Test a la Vez**
Escribimos exactamente un test, lo hacemos pasar, refactorizamos y commiteamos. Luego pasamos al siguiente test. Este ritmo disciplinado crea código de calidad a través de pasos pequeños y verificados.

**🔴 RED - Escribí un Test que Falle**
- Escribí UN test para la siguiente pequeña pieza de comportamiento
- Ejecutalo y miralo fallar (probando que el test funciona)
- El mensaje de fallo debería ser claro y específico
- No escribas el próximo test todavía

**🟢 GREEN - Hacelo Pasar**
- Escribí el código más simple que haga pasar ESTE test
- No te preocupes por la perfección—solo llegá a verde
- Está bien si la implementación es ingenua o incluso hardcodeada
- No anticipes tests futuros—resolvé solo el actual

**🔵 REFACTOR - Mejorá el Diseño**
- Ahora que los tests pasan, mejorá el código
- Escuchá lo que el código te está diciendo
- Eliminá duplicación, clarificá nombres, extraé conceptos
- Ejecutá tests después de cada pequeño refactoring
- Commiteá cuando el refactoring esté completo y los tests en verde

**Repetí** - Escribí el siguiente test. Un test a la vez revela el diseño incrementalmente.

---

## ¿Por Qué Test First?

**Descubrimiento**
- Los tests revelan cómo el código quiere ser moldeado
- Escribir tests primero expone problemas de diseño inmediatamente
- El código emerge de los tests, no al revés
- Los pasos pequeños previenen la sobreingeniería

**Mejor Diseño**
- Te fuerza a pensar en comportamiento antes que en implementación
- Fomenta unidades pequeñas, enfocadas y testeables
- Hace explícitas las dependencias (especialmente con modelo de dominio puro)

**Confianza**
- Cada línea de código tiene un test que la impulsó a existir
- Seguro para refactorizar sin miedo—los tests atrapan errores
- Barra verde significa que el sistema funciona

**Verdad**
- Los tests no mienten—o pasan o fallan
- El ciclo red-green-refactor provee feedback constante
- Siempre sabés dónde estás parado

---

## Qué Testear

**Sí Testear:**
- Comportamiento, no implementación
- Reglas de negocio en el modelo de dominio
- Casos extremos y condiciones de borde
- Interfaces públicas y contratos
- Bugs recientemente arreglados (prevención de regresión)

**No Testear:**
- Detalles de implementación privados (testeá a través de la interfaz pública)
- Código de frameworks o librerías (confiá en que funciona)
- Código trivial de paso directo
- Cómo funciona el código internamente (solo lo que hace)

---

## Escribir Buenos Tests

**Un Comportamiento Por Test**
- Cada test debería verificar una cosa específica
- Claro pasa/falla: o funciona o no funciona
- Nombrá los tests para describir el comportamiento: `test_carrito_vacio_tiene_total_cero()`

**Patrón Arrange-Act-Assert**
```
# Arrange - Configurar datos y condiciones de prueba
carrito = CarritoDeCompras()

# Act - Ejecutar el comportamiento siendo testeado
total = carrito.calcular_total()

# Assert - Verificar el resultado esperado
assert total == 0
```

**Mantené los Tests Simples**
- Los tests deberían ser más fáciles de entender que el código que testean
- Evitá lógica compleja en los tests
- Hacé que las fallas de tests sean obvias y debugueables

---

## Tips de Desarrollo Guiado por Tests

**La Disciplina Crea Libertad**
- Escribí exactamente un test a la vez—resistí escribir múltiples
- Tomá el paso más pequeño posible hacia verde
- Dejá que el test te diga qué código escribir
- Nunca te saltes el paso de refactor (ahí es donde emerge el diseño)
- Commiteá después de cada refactor verde
- Confiá en el proceso—la calidad emerge del ritmo

**Beneficios del Modelo de Dominio Puro**
- La lógica de negocio no tiene dependencias externas
- Los tests corren rápido (sin I/O, sin mocks)
- Los objetos de dominio son fáciles de construir y testear
- Los servicios coordinan; los objetos de dominio contienen lógica

---

## Cuando los Tests Son Difíciles de Escribir

Si testear se siente difícil, tu código podría estar:
- Haciendo demasiado (violando responsabilidad única)
- Muy acoplado a dependencias
- Faltándole interfaces claras
- Mezclando responsabilidades (lógica de negocio con infraestructura)

**Solución:** Refactorizá para hacer el código más testeable. Ver [refactoring.md](refactoring.md).

---

*Testing es una habilidad que mejora con la práctica. Empezá simple, mantené la disciplina con el ciclo red-green-refactor, y dejá que los tests te guíen hacia un mejor diseño.*
