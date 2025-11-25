# Funcionalidades Avanzadas de Kiro

Esta guía cubre características avanzadas de Kiro para usuarios que ya dominan lo básico y quieren aprovechar al máximo la herramienta en proyectos complejos.

---

## 1. Gestión de Sesiones Múltiples

### ¿Qué son las Sesiones?

Una **sesión** es un contexto de conversación independiente con Kiro. Cada sesión mantiene su propio historial y contexto.

### Cuándo Usar Múltiples Sesiones

**Escenario 1: Diferentes Aspectos del Proyecto**
- Sesión 1: Frontend (React components)
- Sesión 2: Backend (API endpoints)
- Sesión 3: Database (schemas y migrations)
- Sesión 4: Tests

**Ventajas:**
- ✅ Contexto enfocado en cada sesión
- ✅ Menos tokens por sesión
- ✅ Más fácil encontrar conversaciones específicas
- ✅ Evita confusión entre diferentes contextos

**Escenario 2: Experimentación vs Producción**
- Sesión 1: Experimentar con diferentes enfoques
- Sesión 2: Implementación final del enfoque elegido

**Ventajas:**
- ✅ Puedes explorar sin contaminar la sesión principal
- ✅ Fácil descartar experimentos fallidos
- ✅ Mantener limpia la sesión de producción

**Escenario 3: Diferentes Features**
- Sesión 1: Feature A (validación de actas)
- Sesión 2: Feature B (generación de reportes)
- Sesión 3: Feature C (exportación a PDF)

**Ventajas:**
- ✅ Historial organizado por feature
- ✅ Fácil retomar trabajo en una feature específica
- ✅ Contexto relevante para cada feature

### Cómo Crear y Gestionar Sesiones

**Crear nueva sesión:**
1. Haz clic en el botón "+" en el panel de sesiones
2. O usa Command Palette: `Ctrl+Shift+P` → "New Chat Session"

**Cambiar entre sesiones:**
1. Haz clic en la sesión deseada en el panel lateral
2. O usa `Ctrl+Tab` para navegar entre sesiones recientes

**Renombrar sesión:**
1. Haz clic derecho en la sesión
2. Selecciona "Rename"
3. Dale un nombre descriptivo (ej: "Backend API", "Frontend Components")

**Eliminar sesión:**
1. Haz clic derecho en la sesión
2. Selecciona "Delete"
3. Confirma la eliminación

### Mejores Prácticas con Sesiones

**✅ Hacer:**
- Nombrar sesiones descriptivamente
- Crear sesión nueva para contextos diferentes
- Cerrar sesiones que ya no necesitas
- Usar sesiones para organizar trabajo por feature

**❌ Evitar:**
- Una sola sesión gigante para todo
- Sesiones sin nombre claro
- Acumular muchas sesiones sin organizar
- Mezclar contextos diferentes en una sesión

---

## 2. Técnicas Avanzadas de #Codebase

### Búsquedas Básicas vs Avanzadas

**Búsqueda básica:**
```
Usando #Codebase busca ActaValidator
```

**Búsqueda avanzada con contexto:**
```
Usando #Codebase busca todos los lugares donde se validan actas 
y muestra cómo se manejan los errores en cada caso
```

### Patrones de Búsqueda Efectivos

#### Patrón 1: Buscar Implementaciones

```
Usando #Codebase busca todas las implementaciones de la interface Validator
```

**Útil para:**
- Entender patrones de diseño en el proyecto
- Encontrar ejemplos de implementación
- Verificar consistencia

#### Patrón 2: Buscar Uso de APIs

```
Usando #Codebase busca todos los lugares donde se usa fs.readFile 
y muestra cómo se maneja el manejo de errores
```

**Útil para:**
- Auditar uso de APIs
- Encontrar patrones de error handling
- Refactorizar uso de APIs

#### Patrón 3: Buscar Patrones de Código

```
Usando #Codebase busca todos los archivos que usan el patrón repository
```

**Útil para:**
- Entender arquitectura del proyecto
- Encontrar ejemplos de patrones
- Mantener consistencia arquitectónica

#### Patrón 4: Buscar Dependencias

```
Usando #Codebase busca qué módulos dependen de ActaParser
```

**Útil para:**
- Entender impacto de cambios
- Planear refactorings
- Analizar acoplamiento

### Búsquedas Complejas

**Combinar múltiples criterios:**
```
Usando #Codebase busca funciones que:
1. Usen async/await
2. Manejen errores con try/catch
3. Retornen ValidationResult
```

**Búsqueda con contexto de negocio:**
```
Usando #Codebase busca toda la lógica relacionada con 
validación de consistencia de votos en actas electorales
```

### Optimizar Búsquedas en #Codebase

**✅ Búsquedas efectivas:**
- Específicas: "busca ActaValidator" vs "busca validadores"
- Con contexto: "busca y muestra cómo se usa"
- Enfocadas: Un concepto a la vez

**❌ Búsquedas ineficientes:**
- Muy amplias: "busca todo sobre validación"
- Múltiples conceptos: "busca validators, parsers, y formatters"
- Sin contexto: "busca código"

---

## 3. Combinación de Steering Files + Hooks para Automatización Completa

### Workflow Automatizado: Ejemplo Completo

**Objetivo:** Mantener código consistente y validado automáticamente

#### Paso 1: Steering File Define Convenciones

**Archivo:** `.kiro/steering/typescript-conventions.md`

```markdown
# Convenciones TypeScript

## Validaciones
- Todas las funciones de validación deben retornar ValidationResult
- Mensajes de error en español
- Usar métodos privados para validaciones individuales

## Tests
- Cada validación debe tener property test
- Mínimo 100 iteraciones por property test
- Usar fast-check para generadores
```

#### Paso 2: Hook Valida Convenciones

**Hook:** "Validar convenciones al guardar"
- **Trigger:** onFileSave
- **Pattern:** `src/**/*.ts`
- **Command:** `npm run lint && npm test`

#### Paso 3: Workflow Completo

1. Desarrollador escribe código
2. Kiro genera código siguiendo steering file
3. Desarrollador guarda archivo
4. Hook ejecuta lint + tests automáticamente
5. Si falla, desarrollador ve errores inmediatamente
6. Si pasa, código está listo

**Resultado:** Código consistente y validado sin intervención manual.

### Ejemplos de Workflows Automatizados

#### Workflow 1: Validación de Mensajes

**Steering file:**
```markdown
Todos los mensajes de usuario deben estar en español
```

**Hook:**
```
Command: node scripts/validate-spanish-messages.js
```

**Script:**
```javascript
// Busca console.log, throw new Error, etc.
// Verifica que los mensajes están en español
// Falla si encuentra mensajes en inglés
```

#### Workflow 2: Actualización de Tipos

**Steering file:**
```markdown
Cuando se modifica schema.json, regenerar tipos TypeScript
```

**Hook:**
```
Trigger: onFileSave
Pattern: schema.json
Command: npm run generate-types
```

#### Workflow 3: Sincronización de Traducciones

**Steering file:**
```markdown
Mantener archivos de traducción sincronizados
```

**Hook:**
```
Trigger: onFileSave
Pattern: i18n/es.json
Command: node scripts/sync-translations.js
```

### Mejores Prácticas para Workflows

**✅ Hacer:**
- Documentar workflows en README
- Mantener scripts de validación simples
- Hacer que hooks sean rápidos (< 5 segundos)
- Permitir desactivar hooks temporalmente

**❌ Evitar:**
- Workflows muy complejos
- Hooks que modifican archivos sin confirmación
- Dependencias circulares entre hooks
- Hooks que siempre fallan

---

## 4. Trabajo en Equipo con Kiro

### Compartir Specs

**Qué compartir:**
- `.kiro/specs/` - Requirements, design, tasks
- `.kiro/steering/` - Convenciones del proyecto
- `.kiro/settings/mcp.json` - Configuración de MCP (sin credenciales)

**Cómo compartir:**
```bash
# Commitear al repositorio
git add .kiro/
git commit -m "Add project specs and conventions"
git push
```

**Beneficios:**
- ✅ Todo el equipo sigue las mismas convenciones
- ✅ Specs sirven como documentación
- ✅ Nuevos miembros se ponen al día rápido
- ✅ Consistencia en todo el proyecto

### Compartir Configuraciones

**Archivo:** `.kiro/settings/workspace.json`

```json
{
  "preferredModel": "claude-sonnet",
  "autoSave": true,
  "formatting": {
    "tabSize": 2,
    "useTabs": false
  }
}
```

**Commitear al repo:** El equipo obtiene la misma configuración.

### Compartir Hooks

Los hooks configurados en el workspace se comparten automáticamente:

1. Configura hooks útiles para el equipo
2. Commitea la configuración
3. El equipo obtiene los mismos hooks al clonar

**Hooks recomendados para equipos:**
- Ejecutar tests al guardar
- Validar mensajes en español
- Ejecutar linter
- Verificar convenciones

### Convenciones de Equipo

**Crear guía de equipo:**

**Archivo:** `.kiro/steering/team-conventions.md`

```markdown
# Convenciones del Equipo

## Sesiones
- Nombrar sesiones con formato: [Feature] - [Descripción]
- Ejemplo: "Auth - Implementar login"

## Commits
- Usar conventional commits
- Ejecutar tests antes de commit

## Specs
- Actualizar specs cuando cambien requirements
- Revisar design antes de implementar

## Code Review
- Usar Kiro para generar código
- Revisar código generado antes de commit
- Pedir a Kiro que explique código complejo
```

### Onboarding de Nuevos Miembros

**Checklist para nuevos miembros:**

1. **Clonar repositorio**
   ```bash
   git clone [repo]
   cd [proyecto]
   ```

2. **Instalar dependencias**
   ```bash
   npm install
   ```

3. **Revisar specs**
   - Leer `.kiro/specs/*/requirements.md`
   - Leer `.kiro/specs/*/design.md`

4. **Revisar convenciones**
   - Leer `.kiro/steering/*.md`

5. **Configurar Kiro**
   - Verificar que hooks están activos
   - Verificar que MCP servers se conectan

6. **Primer tarea**
   - Abrir `.kiro/specs/*/tasks.md`
   - Elegir tarea no asignada
   - Ejecutar con Kiro

**Tiempo estimado:** 30 minutos para estar productivo.

---

## 5. Tips de Optimización Avanzada de Tokens

### Técnica 1: Reutilizar Contexto

**En lugar de:**
```
Sesión 1: Crea ActaParser [incluye todo el contexto]
Sesión 2: Crea ActaValidator [incluye todo el contexto de nuevo]
```

**Mejor:**
```
Sesión 1: Crea tipos base (Acta, ValidationResult)
Sesión 2: Crea ActaParser usando #File types.ts
Sesión 3: Crea ActaValidator usando #File types.ts
```

**Ahorro:** No repites el contexto de tipos en cada sesión.

### Técnica 2: Specs como Documentación

**En lugar de:**
```
Cada prompt: "Recuerda que los mensajes deben estar en español, 
usar interfaces en PascalCase, ..."
```

**Mejor:**
```
Steering file: Define convenciones una vez
Cada prompt: Kiro usa automáticamente las convenciones
```

**Ahorro:** No repites convenciones en cada prompt.

### Técnica 3: Sesiones Enfocadas

**En lugar de:**
```
Una sesión con todo el historial del proyecto (miles de tokens)
```

**Mejor:**
```
Sesión específica para la tarea actual (solo contexto relevante)
```

**Ahorro:** Solo incluyes contexto necesario.

### Técnica 4: Incremental Development

**En lugar de:**
```
Prompt: Crea todo el sistema de validación completo
```

**Mejor:**
```
Prompt 1: Crea interface ValidationResult
Prompt 2: Crea método validateSumConsistency
Prompt 3: Crea método validateNoNegativeVotes
Prompt 4: Integra métodos en validate()
```

**Ahorro:** Cada prompt es más pequeño y enfocado.

### Técnica 5: Usar Referencias

**En lugar de:**
```
Prompt: Crea ActaValidator [describe toda la lógica]
```

**Mejor:**
```
Prompt: Usando #File design.md, implementa ActaValidator según el diseño
```

**Ahorro:** El design ya tiene toda la información.

---

## 6. Comparación: Modo Vibe vs Modo Spec

### Cuándo Usar Cada Modo

| Aspecto | Modo Vibe | Modo Spec |
|---------|-----------|-----------|
| **Velocidad inicial** | ⚡ Muy rápido | 🐢 Más lento (setup) |
| **Documentación** | ❌ Mínima | ✅ Completa |
| **Correctitud** | ⚠️ No garantizada | ✅ Property tests |
| **Mantenibilidad** | ⚠️ Difícil | ✅ Fácil |
| **Escalabilidad** | ❌ Limitada | ✅ Excelente |
| **Trabajo en equipo** | ⚠️ Complicado | ✅ Estructurado |
| **Refactoring** | ❌ Difícil | ✅ Guiado por specs |
| **Onboarding** | ⚠️ Lento | ✅ Rápido (specs) |

### Decisión Rápida

**Usa Vibe si:**
- ✅ Prototipo rápido
- ✅ Script de una sola vez
- ✅ Experimento personal
- ✅ Aprendiendo algo nuevo
- ✅ Proyecto < 500 líneas

**Usa Spec si:**
- ✅ Proyecto de producción
- ✅ Trabajo en equipo
- ✅ Código crítico
- ✅ Proyecto > 1000 líneas
- ✅ Necesitas documentación
- ✅ Requieres correctitud garantizada

### Transición de Vibe a Spec

**Escenario:** Empezaste en Vibe, ahora necesitas Spec

**Pasos:**

1. **Crear requirements basados en código existente**
   ```
   Usando #Folder src/
   
   Crea un requirements.md que documente la funcionalidad actual
   ```

2. **Crear design basado en arquitectura actual**
   ```
   Usando #Folder src/
   
   Crea un design.md que documente la arquitectura actual
   ```

3. **Crear tasks para mejoras futuras**
   ```
   Usando requirements.md y design.md
   
   Crea tasks.md con mejoras pendientes
   ```

4. **Agregar tests**
   ```
   Implementa property tests según las correctness properties del design
   ```

**Resultado:** Proyecto Vibe convertido a Spec con documentación completa.

---

## 7. Casos de Uso Avanzados

### Caso 1: Migración de Código Legacy

**Objetivo:** Modernizar código antiguo

**Estrategia:**
1. Crear spec que documente funcionalidad actual
2. Crear design con arquitectura moderna
3. Implementar nueva versión siguiendo spec
4. Migrar gradualmente con tests

**Prompts:**
```
Usando #File legacy-validator.js

Crea requirements.md que documente qué hace este código
```

```
Usando requirements.md

Crea design.md con arquitectura moderna en TypeScript
```

### Caso 2: Integración de Múltiples Servicios

**Objetivo:** Integrar varios servicios externos

**Estrategia:**
1. Configurar MCP servers para cada servicio
2. Crear steering file con patrones de integración
3. Usar sesiones separadas para cada integración
4. Consolidar en sesión principal

**Ejemplo:**
- Sesión 1: Integración con base de datos (MCP postgres)
- Sesión 2: Integración con API externa (MCP fetch)
- Sesión 3: Integración con filesystem (MCP filesystem)
- Sesión 4: Orquestar todas las integraciones

### Caso 3: Refactoring Masivo

**Objetivo:** Refactorizar arquitectura completa

**Estrategia:**
1. Documentar arquitectura actual con #Codebase
2. Crear design con nueva arquitectura
3. Crear tasks de migración incremental
4. Ejecutar tasks con tests en cada paso

**Prompts:**
```
Usando #Codebase

Documenta la arquitectura actual del proyecto
```

```
Crea design.md con nueva arquitectura basada en [patrón]
```

```
Crea tasks.md con pasos de migración incremental
```

---

## Recursos Adicionales

- **BEST-PRACTICES.md:** Mejores prácticas básicas
- **SPEC-GUIDE.md:** Guía completa de modo Spec
- **STEERING-GUIDE.md:** Configurar convenciones
- **HOOKS-GUIDE.md:** Automatizar workflows
- **MCP-GUIDE.md:** Extender capacidades

---

## Conclusión

Las funcionalidades avanzadas de Kiro te permiten:

- ✅ Gestionar proyectos complejos con múltiples sesiones
- ✅ Buscar y entender código con #Codebase avanzado
- ✅ Automatizar workflows con steering + hooks
- ✅ Colaborar efectivamente en equipo
- ✅ Optimizar consumo de tokens
- ✅ Elegir el modo apropiado (Vibe vs Spec)

**Recuerda:** Estas técnicas se aprenden con práctica. Empieza con lo básico y gradualmente incorpora técnicas avanzadas según las necesites.
