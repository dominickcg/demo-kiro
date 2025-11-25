# Guía de Agent Hooks

**Duración:** 5-10 minutos  
**Objetivo:** Aprender a configurar agent hooks para automatizar tareas en respuesta a eventos

## ¿Qué son los Agent Hooks?

Los **agent hooks** son automatizaciones que ejecutan acciones cuando ocurren eventos específicos en Kiro. Funcionan como "triggers" que responden a cambios en tu proyecto.

### ¿Para qué sirven?

- **Automatizar tareas repetitivas:** Ejecutar tests, linters, formatters
- **Mantener calidad:** Validar código antes de commits
- **Acelerar feedback:** Ver resultados inmediatamente al guardar
- **Sincronizar recursos:** Actualizar traducciones, regenerar tipos
- **Workflows personalizados:** Crear flujos de trabajo específicos de tu equipo

### Ejemplos de uso

- Ejecutar tests automáticamente al guardar archivos
- Correr linter cuando se modifica código
- Regenerar tipos cuando cambia un schema
- Actualizar traducciones cuando se modifica el archivo base
- Ejecutar build cuando se modifica configuración

---

## Tipos de Eventos (Triggers)

### 1. onFileSave
Se dispara cuando guardas un archivo

**Uso común:**
- Ejecutar tests relacionados
- Formatear código automáticamente
- Validar sintaxis

### 2. onMessage
Se dispara cuando envías un mensaje al agente

**Uso común:**
- Recordatorios de convenciones
- Validaciones antes de generar código
- Contexto adicional automático

### 3. onSessionStart
Se dispara cuando inicias una nueva sesión

**Uso común:**
- Cargar contexto del proyecto
- Verificar dependencias
- Mostrar estado del proyecto

### 4. Manual
Se dispara cuando haces clic en un botón

**Uso común:**
- Tareas bajo demanda (spell-check, refactor)
- Operaciones costosas que no quieres automáticas
- Comandos específicos del proyecto

---

## Cuándo Configurar Agent Hooks

⏰ **Momento ideal:** Después de tener tests implementados

**Flujo recomendado:**
1. Desarrollar funcionalidad básica
2. Escribir tests
3. Configurar hook para ejecutar tests al guardar
4. Continuar desarrollando con feedback automático

**Nota:** No configures hooks antes de tener tests, o se ejecutarán sin hacer nada útil.

---

## Cómo Configurar Agent Hooks

### Método 1: Desde la UI de Kiro (Recomendado)

**Pasos:**

1. **Abrir el panel de Agent Hooks**
   - Busca "Agent Hooks" en el explorador lateral de Kiro
   - O usa el Command Palette: `Ctrl+Shift+P` → "Open Kiro Hook UI"

2. **Crear nuevo hook**
   - Haz clic en "Create New Hook" o botón "+"

3. **Configurar el hook**
   - **Name:** Nombre descriptivo (ej: "Ejecutar tests al guardar")
   - **Trigger:** Selecciona el evento (ej: "onFileSave")
   - **File Pattern:** Patrón de archivos (ej: `**/*.ts`)
   - **Action Type:** "Command" o "Message"
   - **Command/Message:** Lo que se ejecutará (ej: `npm test`)

4. **Guardar y activar**
   - Marca como "Enabled"
   - Guarda la configuración

### Método 2: Desde Command Palette

**Pasos:**

1. Abre Command Palette: `Ctrl+Shift+P` (Windows/Linux) o `Cmd+Shift+P` (Mac)
2. Busca: "Open Kiro Hook UI"
3. Sigue los pasos del Método 1

---

## Ejemplo 1: Ejecutar Tests al Guardar

### Configuración

**Desde la UI de Kiro:**

- **Name:** `Ejecutar tests al guardar`
- **Trigger:** `onFileSave`
- **File Pattern:** `**/*.ts`
- **Action Type:** `Command`
- **Command:** `npm test`
- **Enabled:** ✓

### Comportamiento

1. Modificas cualquier archivo `.ts`
2. Guardas el archivo (`Ctrl+S`)
3. El hook detecta el evento
4. Ejecuta `npm test` automáticamente
5. Ves los resultados en la terminal

### Cuándo es útil

✅ Durante desarrollo activo  
✅ Cuando tienes tests rápidos (< 5 segundos)  
✅ Para detectar errores inmediatamente  

❌ Con tests lentos (> 30 segundos)  
❌ En proyectos muy grandes  
❌ Si prefieres ejecutar tests manualmente  

---

## Ejemplo 2: Recordatorio de Convenciones

### Configuración

**Desde la UI de Kiro:**

- **Name:** `Recordar convenciones TypeScript`
- **Trigger:** `onMessage`
- **Action Type:** `Message`
- **Message:** `Recuerda seguir las convenciones del steering file: interfaces en PascalCase, funciones en camelCase, mensajes en español`
- **Enabled:** ✓

### Comportamiento

1. Envías un mensaje a Kiro
2. El hook se dispara automáticamente
3. Agrega el recordatorio al contexto
4. Kiro genera código siguiendo las convenciones

### Cuándo es útil

✅ Para reforzar convenciones importantes  
✅ En equipos nuevos aprendiendo el proyecto  
✅ Para contexto que siempre debe estar presente  

---

## Ejemplo 3: Formatear Código al Guardar

### Configuración

**Desde la UI de Kiro:**

- **Name:** `Formatear con Prettier`
- **Trigger:** `onFileSave`
- **File Pattern:** `**/*.{ts,js,json}`
- **Action Type:** `Command`
- **Command:** `npx prettier --write`
- **Enabled:** ✓

### Comportamiento

1. Guardas un archivo TypeScript, JavaScript o JSON
2. Prettier formatea el archivo automáticamente
3. El archivo se guarda con formato consistente

---

## Ejemplo 4: Hook Manual para Spell-Check

### Configuración

**Desde la UI de Kiro:**

- **Name:** `Revisar ortografía en README`
- **Trigger:** `Manual`
- **Action Type:** `Message`
- **Message:** `Revisa la ortografía y gramática del archivo README.md y sugiere correcciones`
- **Enabled:** ✓

### Comportamiento

1. Haces clic en el botón del hook en la UI
2. Kiro revisa el README.md
3. Sugiere correcciones de ortografía y gramática

### Cuándo es útil

✅ Para tareas bajo demanda  
✅ Operaciones que no quieres automáticas  
✅ Comandos específicos del proyecto  

---

## Patrones de File Pattern

### Sintaxis de Glob

| Pattern | Descripción | Ejemplo |
|---------|-------------|---------|
| `**/*.ts` | Todos los archivos .ts en cualquier carpeta | `src/parser/acta.ts` |
| `src/**/*.ts` | Archivos .ts solo en src/ | `src/types/acta.ts` |
| `**/*.test.ts` | Solo archivos de test | `tests/parser.test.ts` |
| `**/*.{ts,js}` | Archivos .ts o .js | `src/index.ts`, `utils.js` |
| `src/parser/**` | Cualquier archivo en src/parser/ | `src/parser/acta.ts` |

### Ejemplos Comunes

```
**/*.ts              → Todos los TypeScript
**/*.test.ts         → Solo tests
src/**/*.ts          → TypeScript en src/
**/*.{ts,tsx}        → TypeScript y React
!**/*.test.ts        → Excluir tests (negación)
```

---

## Verificar que el Hook Funciona

### Prueba 1: Modificar y Guardar

1. Abre un archivo que coincida con el pattern
2. Haz un cambio pequeño
3. Guarda el archivo (`Ctrl+S`)
4. Observa la terminal o panel de output

**Resultado esperado:** El comando se ejecuta automáticamente

### Prueba 2: Revisar Logs

1. Abre el panel de Agent Hooks
2. Busca el hook configurado
3. Revisa el historial de ejecuciones
4. Verifica que se disparó correctamente

### Prueba 3: Desactivar y Comparar

1. Desactiva el hook temporalmente
2. Guarda un archivo
3. Observa que no se ejecuta nada
4. Reactiva el hook
5. Guarda de nuevo
6. Confirma que ahora sí se ejecuta

---

## Hooks Avanzados: Combinación con Steering Files

### Workflow Automatizado Completo

**Steering File** → Define convenciones  
**Agent Hook** → Valida que se cumplan  

**Ejemplo:**

1. **Steering file** dice: "Todos los mensajes en español"
2. **Hook onFileSave** ejecuta: Script que verifica mensajes en español
3. Si encuentra mensajes en inglés → Alerta al desarrollador

### Configuración

**Hook:**
- **Name:** `Validar mensajes en español`
- **Trigger:** `onFileSave`
- **File Pattern:** `src/**/*.ts`
- **Command:** `node scripts/validate-messages.js`

**Script (validate-messages.js):**
```javascript
// Script que busca console.log con mensajes en inglés
// y alerta si encuentra alguno
```

---

## Mejores Prácticas

### ✅ Hacer

- Usar hooks para tareas rápidas (< 10 segundos)
- Configurar después de tener tests
- Usar file patterns específicos para evitar ejecuciones innecesarias
- Desactivar hooks temporalmente si molestan durante debugging
- Documentar hooks importantes en el README del proyecto

### ❌ Evitar

- Hooks que ejecutan tareas muy lentas (> 30 segundos)
- Múltiples hooks que hacen lo mismo
- Hooks que modifican archivos sin confirmación
- Hooks en proyectos sin tests (no hay nada que ejecutar)
- Demasiados hooks que ralentizan el workflow

---

## Troubleshooting

### El hook no se ejecuta

**Posibles causas:**
- Hook desactivado (Enabled = false)
- File pattern no coincide con el archivo
- Comando incorrecto o no encontrado
- Error en la configuración del hook

**Solución:**
1. Verifica que el hook está activado
2. Prueba el file pattern con un archivo específico
3. Ejecuta el comando manualmente en la terminal
4. Revisa los logs del hook

### El hook se ejecuta demasiado

**Posibles causas:**
- File pattern demasiado amplio (`**/*`)
- Múltiples hooks con el mismo trigger
- Hook configurado en onMessage sin necesidad

**Solución:**
1. Refina el file pattern para ser más específico
2. Consolida hooks similares
3. Considera usar trigger Manual en lugar de automático

### El comando falla

**Posibles causas:**
- Dependencias no instaladas
- Ruta incorrecta al comando
- Permisos insuficientes

**Solución:**
1. Ejecuta el comando manualmente: `npm test`
2. Verifica que las dependencias están instaladas
3. Usa rutas absolutas si es necesario

---

## Ejemplo de Uso en la Demo

Durante el proyecto Spec, configuramos un hook que:

1. **Trigger:** onFileSave en archivos `**/*.ts`
2. **Action:** Ejecuta `npm test`
3. **Resultado:** Cada vez que guardas código, los tests se ejecutan automáticamente

**Beneficio:** Detectas errores inmediatamente sin tener que ejecutar tests manualmente.

---

## Hooks para Trabajo en Equipo

### Compartir Hooks

Los hooks se pueden compartir con el equipo:

1. Los hooks se guardan en la configuración del workspace
2. Commitea la configuración al repositorio
3. El equipo obtiene los mismos hooks al clonar

### Hooks Recomendados para Equipos

**Hook 1: Tests al guardar**
- Asegura que el código pasa tests antes de commit

**Hook 2: Linter al guardar**
- Mantiene estilo consistente en todo el equipo

**Hook 3: Recordatorio de convenciones**
- Refuerza estándares del proyecto

---

## Recursos Adicionales

- **Documentación oficial:** Consulta la documentación de Kiro sobre hooks
- **Command Palette:** Busca "Kiro Hook" para ver todos los comandos relacionados
- **Comunidad:** Comparte tus hooks útiles con otros desarrolladores

---

## Siguiente Paso

Ahora que entiendes agent hooks, puedes:
1. Configurar hooks para tus proyectos
2. Combinar hooks con steering files para workflows completos
3. Explorar MCP Servers para extender capacidades de Kiro

**Archivo relacionado:** [MCP-GUIDE.md](MCP-GUIDE.md) - Aprende sobre MCP Servers
