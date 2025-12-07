# Guía de Estilo de Código

> 📝 **Nota de Plantilla:** Personalizá este archivo para las convenciones específicas de tu proyecto, o eliminá secciones que no apliquen.

Esta guía define los estándares de codificación y convenciones para nuestro proyecto. La consistencia hace el código más fácil de leer, mantener y colaborar.

---

## Principios Generales

**Claridad Sobre Ingenio**
- Escribí código que sea fácil de entender, no código que alarde
- Si necesita comentarios extensos para explicar, probablemente necesite refactoring
- Elegí soluciones obvias sobre ingeniosas

**El Naming Importa**
- Usá nombres descriptivos que revelen intención
- Funciones y métodos deberían ser verbos: `calcularTotal()`, `validarEntrada()`
- Clases y tipos deberían ser sustantivos: `CuentaDeUsuario`, `ProcesadorDeOrdenes`
- Booleanos deberían leerse como preguntas: `esValido`, `tienePermiso`, `puedeEditar`

**Efectos Secundarios**
- Funciones puras (sin side effects) deberían tener nombres que revelen su intención clara
- Si una función TIENE efectos secundarios, debe estar explícito en el nombre
- Ejemplos:
  - ✅ `calcularTotal()` - sin side effects, devuelve valor
  - ✅ `guardarUsuario()` / `persistirUsuario()` - claro que tiene side effects
  - ❌ `procesarDatos()` - ambiguo, ¿modifica o solo calcula?
  - ❌ `procesarYGuardarDatos()` - evidencia que viola responsabilidad única
- Preferí funciones puras cuando sea posible; orquestá side effects desde niveles superiores

**Mantelo Pequeño**
- Las funciones deberían hacer una cosa bien
- Las clases deberían tener una responsabilidad clara y única
- Los archivos deberían ser cohesivos y enfocados

---

## Organización del Código

**Estructura de Archivo**
- Agrupar funcionalidad relacionada
- Mantener interfaces públicas arriba
- Implementación interna/privada abajo
- Una clase/concepto principal por archivo

**Imports/Dependencias**
- Librería estándar primero
- Librerías de terceros siguiente
- Imports locales del proyecto al final
- Alfabetizar dentro de cada grupo

---

## Formateo

**Indentación**
- Usá indentación consistente (típicamente 2 o 4 espacios, o tabs—elegí uno)
- Sé consistente en todo el proyecto

**Largo de Línea**
- Apuntá a 80-120 caracteres por línea
- Rompé líneas largas en puntos lógicos
- No sacrifiques legibilidad por reglas de largo de línea

**Espacios en Blanco**
- Usá líneas en blanco para separar secciones lógicas
- Agregá espacio alrededor de operadores: `x = a + b` no `x=a+b`
- Una sentencia por línea

---

## Comentarios y Documentación

**Cuándo Comentar**
- Explicá *por qué*, no *qué*
- Documentá decisiones no obvias
- Advertí sobre gotchas o casos extremos
- Proporcioná ejemplos para APIs complejos

**Cuándo NO Comentar**
- No expliques qué el código obviamente hace
- No dejes código comentado (usá control de versiones en su lugar)
- No te disculpes por la calidad del código (arreglalo en su lugar)

**Documentación**
- Las APIs públicas e interfaces necesitan documentación clara
- Incluí descripciones de parámetros y valores de retorno
- Proporcioná ejemplos de uso para funcionalidad compleja

---

## Manejo de Errores

- Falla rápido y fuertemente durante desarrollo
- Proporcioná mensajes de error útiles
- No tragues excepciones silenciosamente
- Validá entrada en los límites

---

## Consideraciones de Testing

- Escribí código testeable (ver [testing.md](testing.md))
- Evitá acoplamiento fuerte a dependencias externas
- Hacé explícitas e inyectables las dependencias
- Mantené los efectos secundarios aislados y obvios

---

## Convenciones de Python

**Lenguaje:** Python 3.x

**Testing:**
- Usá `pytest` como framework de testing
- Usá Approval Tests cuando sea apropiado para snapshot/golden master testing
- Enfocate en testing a nivel unitario
- Naming de archivos de test: `test_*.py` o `*_test.py`
- Una clase de test por clase de producción (típicamente)

**Estructura de Aplicación:**
- Las apps deberían tener una interfaz CLI
- CLI permite testing end-to-end desde línea de comando
- Mantené CLI delgada—delegá al modelo de dominio y servicios

**Estilo de Código:**
- Seguí convenciones PEP 8
- Usá type hints para firmas de funciones
- Preferí explícito sobre implícito
- Usá nombres de variables descriptivos (no abreviados)

**Imports:**
- Librería estándar primero
- Librerías de terceros siguiente
- Imports locales de la aplicación al final
- Alfabetizar dentro de cada grupo

**Ejemplo de Estructura de Test:**
```python
# test_order.py
import pytest
from domain.order import Order

class TestOrder:
    def test_empty_order_has_zero_total(self):
        # Arrange
        order = Order()

        # Act
        total = order.calculate_total()

        # Assert
        assert total == 0
```

---

*Estas son nuestras convenciones para desarrollo en Python. La consistencia en toda la codebase hace la colaboración más fácil.*
