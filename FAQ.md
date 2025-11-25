# FAQ - Preguntas Frecuentes sobre Kiro

Esta guía responde las preguntas más comunes sobre Kiro, desde conceptos básicos hasta optimización avanzada.

## 📑 Tabla de Contenidos

- [Conceptos Básicos](#conceptos-básicos)
- [Funcionalidades](#funcionalidades)
- [Precios y Planes](#precios-y-planes)
- [Tokens y Consumo](#tokens-y-consumo)
- [Sesiones y Contexto](#sesiones-y-contexto)
- [Elección y Cambio de Modelos](#elección-y-cambio-de-modelos)
- [Optimización Avanzada](#optimización-avanzada)

---

## Conceptos Básicos

### ¿Qué es Kiro?

Kiro es un IDE con IA integrada que te ayuda a escribir código de manera más eficiente. Combina un editor de código con un asistente de IA que entiende tu proyecto completo.

### ¿Cuál es la diferencia entre modo Vibe y modo Spec?

- **Modo Vibe:** Desarrollo rápido e iterativo sin documentación formal. Ideal para prototipos y experimentos.
- **Modo Spec:** Desarrollo estructurado con requirements, diseño y plan de implementación. Ideal para proyectos de producción que requieren correctitud y mantenibilidad.

### ¿Qué son los Specs?

Los Specs son documentos estructurados que guían el desarrollo de una funcionalidad. Incluyen:
- **Requirements:** Qué necesitas construir
- **Design:** Cómo lo vas a construir
- **Tasks:** Pasos de implementación

---

## Funcionalidades

### ¿Qué es un Steering File?

Un steering file es un archivo de configuración que proporciona contexto y convenciones a Kiro. Por ejemplo, puedes especificar que uses cierto estilo de código o patrones de diseño específicos.

**Ubicación:** `.kiro/steering/*.md`

**Ejemplo de uso:**
```markdown
# Convenciones de TypeScript

- Usar interfaces en lugar de types
- Nombres en camelCase
- Mensajes de usuario en español
```

### ¿Qué son los Agent Hooks?

Los agent hooks son automatizaciones que ejecutan acciones en respuesta a eventos. Por ejemplo, puedes configurar un hook que ejecute tests automáticamente cada vez que guardas un archivo.

**Ubicación:** `.kiro/hooks/*.json`

**Ejemplo:**
```json
{
  "name": "Ejecutar tests al guardar",
  "trigger": "onFileSave",
  "filePattern": "**/*.ts",
  "action": {
    "type": "command",
    "command": "npm test"
  }
}
```

### ¿Qué es un MCP Server?

MCP (Model Context Protocol) es un protocolo que permite extender las capacidades de Kiro con herramientas externas. Por ejemplo, puedes agregar un servidor que le dé a Kiro acceso a APIs específicas o bases de datos.

**Ubicación:** `.kiro/settings/mcp.json`

### ¿Cómo uso #File y #Folder?

Usa `#File` seguido del nombre del archivo para darle contexto específico a Kiro sobre ese archivo. Usa `#Folder` para darle contexto sobre una carpeta completa.

**Ejemplo:**
```
"Refactoriza la función calculateTurnout en #File src/calculator.ts"
```

Esto ayuda a Kiro a entender mejor tu solicitud sin necesidad de pegar todo el código.

### ¿Qué es #Codebase?

`#Codebase` permite a Kiro buscar en toda tu base de código. Es útil cuando necesitas encontrar dónde se usa una función o patrón específico en todo el proyecto.

**Ejemplo:**
```
"Encuentra todos los lugares donde se usa #Codebase validateActa"
```

### ¿Qué es #Problems?

`#Problems` le da a Kiro acceso a los errores y advertencias que tu IDE está detectando. Esto ayuda a Kiro a entender y solucionar problemas de compilación o linting.

**Ejemplo:**
```
"Ayúdame a resolver #Problems en este archivo"
```

---

## Precios y Planes

### ¿Kiro es gratuito?

Kiro ofrece diferentes planes. Consulta la página oficial de precios para información actualizada sobre planes gratuitos y de pago.

### ¿Qué incluye cada plan?

Los planes varían en:
- Límites de tokens
- Modelos disponibles
- Características avanzadas (steering, hooks, MCP)

Revisa la documentación oficial para detalles específicos.

---

## Tokens y Consumo

### ¿Qué son los tokens?

Los tokens son unidades de medida para el consumo de recursos en Kiro. Cada interacción con la IA consume tokens basándose en la cantidad de texto procesado (tanto input como output).

**Aproximadamente:**
- 1 token ≈ 4 caracteres en inglés
- 1 token ≈ 3-4 caracteres en español

### ¿Cómo puedo ver mi consumo de tokens?

El consumo de tokens se muestra en el chat después de cada respuesta de Kiro. También puedes ver el consumo acumulado en tu panel de usuario.

### ¿Cómo puedo optimizar mi consumo de tokens?

**Mejores prácticas:**

✅ **Sé específico en tus solicitudes**
```
❌ "Mejora este código"
✅ "Refactoriza la función calculateTurnout para usar async/await"
```

✅ **Usa #File en lugar de pegar código completo**
```
❌ [pegar 200 líneas de código]
✅ "Revisa #File src/validator.ts"
```

✅ **Divide tareas grandes en pasos pequeños**
```
❌ "Crea una aplicación completa de validación"
✅ "1. Crea los tipos de datos"
    "2. Implementa el parser"
    "3. Agrega validación"
```

✅ **Evita incluir contexto innecesario**
```
❌ Incluir todo el proyecto cuando solo necesitas ayuda con una función
✅ Usar #File solo en el archivo relevante
```

✅ **Usa steering files para evitar repetir convenciones**
```
❌ Repetir "usa camelCase y mensajes en español" en cada solicitud
✅ Crear un steering file con estas convenciones
```

### ¿Qué consume más tokens?

**Alto consumo:**
- ❌ Incluir archivos grandes con #File
- ❌ Solicitudes muy generales que requieren mucho contexto
- ❌ Generar código muy extenso de una vez
- ❌ Usar #Codebase en proyectos grandes

**Bajo consumo:**
- ✅ Solicitudes específicas y acotadas
- ✅ Usar #File solo en archivos relevantes
- ✅ Dividir tareas en pasos pequeños
- ✅ Usar steering files para contexto persistente

---

## Sesiones y Contexto

### ¿Qué es una sesión en Kiro?

Una sesión es un contexto de conversación activo que mantiene el historial de tu interacción con Kiro. Kiro recuerda lo que has discutido en la sesión actual.

### ¿Cuánto dura una sesión?

Una sesión permanece activa mientras mantengas Kiro abierto. Si cierras Kiro, la sesión se guarda y puedes continuarla después.

### ¿Puedo tener múltiples sesiones?

Sí, puedes crear nuevas sesiones para diferentes tareas o contextos. Esto es útil para mantener conversaciones separadas sobre diferentes aspectos de tu proyecto.

**Ejemplo de uso:**
- Sesión 1: Implementación de feature A
- Sesión 2: Debugging de feature B
- Sesión 3: Refactoring de código legacy

### ¿Kiro recuerda conversaciones anteriores?

Kiro mantiene el historial dentro de una sesión, pero cada sesión nueva comienza sin contexto de sesiones anteriores (a menos que uses specs o steering files que persisten).

---

## Elección y Cambio de Modelos

### ¿Qué modelos de IA puedo usar en Kiro?

Kiro utiliza modelos de Claude (Anthropic). Los modelos disponibles dependen de tu plan e incluyen diferentes versiones de Claude con distintas capacidades.

### ¿Cómo cambio de modelo?

Puedes cambiar de modelo desde:
1. La configuración de Kiro
2. El selector de modelo en la interfaz de chat

Los modelos disponibles varían según tu plan de suscripción.

### ¿Cuál modelo de Claude debo usar?

| Modelo | Mejor para | Características |
|--------|-----------|-----------------|
| **Claude Opus** | Tareas complejas, razonamiento profundo, código crítico | Más capaz, más costoso |
| **Claude Sonnet** | Mayoría de tareas de desarrollo | Balance costo/capacidad |
| **Claude Haiku** | Tareas simples, respuestas rápidas | Más rápido, más económico |

**Recomendaciones:**

- 🎯 **Usa Opus cuando:** Necesitas razonamiento complejo, arquitectura de sistemas, debugging difícil
- 🎯 **Usa Sonnet cuando:** Desarrollo general, refactoring, implementación de features
- 🎯 **Usa Haiku cuando:** Preguntas simples, formateo de código, tareas repetitivas

### ¿Los diferentes modelos de Claude consumen diferentes cantidades de tokens?

Sí, cada modelo de Claude tiene diferentes costos por token:
- **Opus:** Más costoso por token
- **Sonnet:** Costo medio
- **Haiku:** Más económico por token

---

## Optimización Avanzada

### ¿Cuándo debo usar modo Vibe vs modo Spec?

| Situación | Modo Recomendado |
|-----------|------------------|
| Experimentando con ideas | **Vibe** |
| Prototipo rápido | **Vibe** |
| Explorando soluciones | **Vibe** |
| Código de producción | **Spec** |
| Necesitas documentación | **Spec** |
| Requieres garantías de correctitud | **Spec** |
| Trabajo en equipo | **Spec** |

### ¿Qué es property-based testing?

Property-based testing es una técnica donde defines propiedades que deben cumplirse para cualquier entrada válida, y el framework genera automáticamente cientos de casos de prueba aleatorios para verificar esas propiedades.

**Ejemplo:**
```typescript
// En lugar de:
test("suma de 2 + 3 es 5", () => {
  expect(suma(2, 3)).toBe(5);
});

// Property-based testing:
test("suma es conmutativa", () => {
  fc.assert(fc.property(
    fc.integer(), fc.integer(),
    (a, b) => suma(a, b) === suma(b, a)
  ));
});
// Esto prueba con cientos de pares de números aleatorios
```

### ¿Cómo divido tareas complejas?

**❌ Mal enfoque:**
```
"Crea una aplicación completa de validación de actas electorales"
```

**✅ Buen enfoque:**
```
1. "Crea los tipos de datos (Acta, VoteTally, ValidationResult)"
2. "Implementa la función de parseo de archivos JSON"
3. "Agrega validación de suma de votos"
4. "Agrega validación de votos negativos"
5. "Escribe property tests para validación"
```

**Beneficios:**
- ✅ Menor consumo de tokens por solicitud
- ✅ Más fácil de revisar y corregir
- ✅ Mejor control del proceso
- ✅ Resultados más precisos

### ¿Cuándo debo usar steering files?

Usa steering files cuando:

✅ **Tienes convenciones de código específicas**
```markdown
- Usar interfaces en lugar de types
- Nombres en camelCase
- Mensajes en español
```

✅ **Quieres que Kiro recuerde patrones de diseño**
```markdown
- Usar patrón Repository para acceso a datos
- Usar patrón Strategy para validaciones
```

✅ **Necesitas referencias a documentación externa**
```markdown
- Seguir guía de estilo de TypeScript
- Usar convenciones de la empresa
```

✅ **Trabajas en equipo y quieres consistencia**
```markdown
- Todos los desarrolladores usan las mismas convenciones
- El código generado es consistente
```

### ¿Cómo aprovecho mejor los specs?

**Proceso recomendado:**

1. **Requirements claros y específicos**
   - Usa formato EARS
   - Define acceptance criteria medibles
   - Incluye glossary de términos

2. **Design detallado**
   - Define arquitectura modular
   - Especifica interfaces claras
   - Define correctness properties para testing

3. **Tasks incrementales**
   - Divide en pasos pequeños
   - Cada task referencia requirements
   - Incluye checkpoints para verificación

4. **Ejecución controlada**
   - Ejecuta tareas una por una
   - Revisa resultados antes de continuar
   - Ajusta el plan según necesidad

---

## 💡 Consejos Rápidos

### Para Principiantes
1. Empieza con modo Vibe para familiarizarte
2. Lee el FAQ completo
3. Practica con proyectos pequeños
4. Usa #File para dar contexto

### Para Usuarios Intermedios
1. Aprende a crear specs
2. Experimenta con steering files
3. Configura agent hooks básicos
4. Monitorea tu consumo de tokens

### Para Usuarios Avanzados
1. Domina property-based testing
2. Configura MCP servers
3. Optimiza consumo de tokens
4. Crea workflows personalizados

---

## 🆘 ¿Necesitas Más Ayuda?

- 📖 Revisa la documentación oficial de Kiro
- 💬 Únete a la comunidad de Kiro
- 🐛 Reporta issues en GitHub
- 📧 Contacta soporte técnico

---

## 📚 Recursos Relacionados

- **[VIBE-GUIDE.md](VIBE-GUIDE.md)** - Guía del proyecto Vibe
- **[SPEC-GUIDE.md](SPEC-GUIDE.md)** - Guía del proyecto Spec
- **[EARS-GUIDE.md](EARS-GUIDE.md)** - Formato EARS de requirements
- **[STEERING-GUIDE.md](STEERING-GUIDE.md)** - Configurar steering files
- **[HOOKS-GUIDE.md](HOOKS-GUIDE.md)** - Configurar agent hooks
- **[MCP-GUIDE.md](MCP-GUIDE.md)** - Configurar MCP servers
- **[BEST-PRACTICES.md](BEST-PRACTICES.md)** - Mejores prácticas
- **[ADVANCED-FEATURES.md](ADVANCED-FEATURES.md)** - Funcionalidades avanzadas

---

**Última actualización:** Noviembre 2024
