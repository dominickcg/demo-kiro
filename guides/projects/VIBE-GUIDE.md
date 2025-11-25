# Guía del Proyecto Vibe - Generador de Reportes de Participación Electoral

**Duración:** 15 minutos máximo  
**Objetivo:** Experimentar desarrollo rápido e iterativo con Kiro sin documentación formal

## Introducción (3 minutos)

### ¿Qué es Modo Vibe?

Modo Vibe es desarrollo rápido sin specs, diseño ni documentación formal. Es ideal para:
- ✅ Prototipos rápidos
- ✅ Exploración de ideas
- ✅ Demos y experimentos
- ❌ NO para código de producción
- ❌ NO para proyectos en equipo

### Proyecto: Generador de Reportes de Participación Electoral

Crearemos una herramienta que:
1. Lee datos de mesas electorales desde un archivo CSV
2. Calcula estadísticas de participación
3. Genera un reporte formateado
4. Detecta anomalías (votos > votantes habilitados)

---

## Desarrollo Iterativo (10 minutos)

### Iteración 1: Crear Proyecto Base (2-3 min)

**Prompt para Kiro:**
```
Crea un proyecto TypeScript que lea un archivo CSV con las columnas mesaId, votantesHabilitados, votosEmitidos. 
El archivo está en examples/vibe/turnout-data.csv. 
Usa Node.js y muestra los datos en consola.
```

**Qué esperar:**
- Kiro creará la estructura del proyecto
- Generará código para leer el CSV
- Incluirá package.json con dependencias

**Ejecutar:**
```bash
cd vibe-turnout-report
npm install
node index.js
```

### Iteración 2: Agregar Cálculos (2-3 min)

**Prompt para Kiro:**
```
Agrega cálculo de estadísticas:
- Total de votantes habilitados (suma de todas las mesas)
- Total de votos emitidos (suma de todas las mesas)
- Porcentaje general de participación
Muestra estos totales al final del reporte.
```

**Qué esperar:**
- Kiro agregará funciones de cálculo
- Mostrará totales formateados

**Ejecutar:**
```bash
node index.js
```

### Iteración 3: Mejorar Formato (2-3 min)

**Prompt para Kiro:**
```
Formatea el output como una tabla legible que muestre:
- Encabezado con título del reporte
- Tabla con columnas: Mesa | Habilitados | Votos | Participación %
- Sección de totales al final
Usa caracteres de tabla para que se vea profesional en consola.
```

**Qué esperar:**
- Kiro mejorará el formato visual
- Creará una tabla ASCII bonita

**Ejecutar:**
```bash
node index.js
```

### Iteración 4: Detectar Anomalías (2-3 min)

**Prompt para Kiro:**
```
Agrega detección de anomalías:
- Identifica mesas donde votosEmitidos > votantesHabilitados
- Marca estas mesas con un símbolo de advertencia (⚠️) en la tabla
- Al final del reporte, lista las mesas con anomalías
Si no hay anomalías, muestra "✓ No se detectaron anomalías"
```

**Qué esperar:**
- Kiro agregará validación
- Mostrará advertencias para MESA-005 (tiene 335 votos de 310 habilitados)

**Ejecutar:**
```bash
node index.js
```

---

## Reflexión (2 minutos)

### ✅ Ventajas del Modo Vibe

- **Velocidad:** Proyecto funcional en 10-15 minutos
- **Iteración rápida:** Cambios inmediatos
- **Exploración:** Perfecto para probar ideas
- **Sin overhead:** No necesitas specs ni documentación

### ⚠️ Limitaciones del Modo Vibe

- **Sin tests:** No hay garantías de correctitud
- **Sin documentación:** Difícil de mantener
- **Sin estructura:** Código puede volverse desordenado
- **No escalable:** Problemas en proyectos grandes

### 🎯 Cuándo Usar Modo Vibe

**USA Vibe cuando:**
- Estás explorando una idea nueva
- Necesitas un prototipo rápido
- Estás haciendo una demo
- El código es desechable

**NO uses Vibe cuando:**
- Es código de producción
- Trabajas en equipo
- Necesitas mantenibilidad
- Requieres garantías de correctitud

---

## Siguiente Paso

Ahora que has visto la velocidad del Modo Vibe, pasaremos al **Modo Spec** donde construiremos un proyecto más robusto con:
- Requirements formales
- Diseño estructurado
- Property-based testing
- Documentación completa
- Garantías de correctitud

**Diferencia clave:** Modo Spec toma más tiempo pero produce código profesional y mantenible.

---

## Ejemplo de Output Esperado

```
=== REPORTE DE PARTICIPACIÓN ELECTORAL ===

Mesa         Habilitados    Votos    Participación
─────────────────────────────────────────────────────
MESA-001     300           245      81.67%
MESA-002     280           198      70.71%
MESA-003     320           287      89.69%
MESA-004     290           265      91.38%
MESA-005 ⚠️  310           335      108.06%

TOTALES:
- Votantes Habilitados: 1,500
- Votos Emitidos: 1,330
- Participación General: 88.67%

⚠️ ANOMALÍAS DETECTADAS:
- MESA-005: 335 votos exceden los 310 votantes habilitados
```
