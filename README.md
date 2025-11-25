# Demo Kiro - Guía Completa de 2 Horas

Esta es una guía completa para aprender a usar Kiro, desde nivel básico hasta intermedio, en máximo 2 horas. La demo está diseñada para entidades de procesos electorales y cubre dos enfoques de desarrollo: **Modo Vibe** (rápido) y **Modo Spec** (estructurado).

## 📋 Contenido de la Demo

### PARTE 1: Modo Vibe (15 minutos)
**Proyecto:** Generador de Reportes de Participación Electoral
- Lee datos de mesas desde archivo CSV
- Genera reporte formateado con estadísticas
- Desarrollo rápido e iterativo
- Sin documentación formal
- Ideal para prototipos

### PARTE 2: Modo Spec (resto del tiempo)
**Proyecto:** Validador de Actas Electorales
- Desarrollo estructurado con requirements y diseño
- Property-based testing para correctitud
- Steering files, agent hooks y MCP servers
- Documentación completa

## 🚀 Cómo Usar Esta Guía

### Para Participantes

1. **Lee el FAQ primero:** [FAQ.md](FAQ.md) - Responde preguntas básicas sobre Kiro

2. **Sigue las guías en orden:**
   - **Parte 1 (15 min):** [VIBE-GUIDE.md](VIBE-GUIDE.md) - Desarrollo rápido
   - **Ejercicio (5 min):** [EARS-GUIDE.md](EARS-GUIDE.md) - Formato de requirements
   - **Parte 2 (~90 min):** [SPEC-GUIDE.md](SPEC-GUIDE.md) - Desarrollo estructurado

3. **Explora características avanzadas:**
   - [STEERING-GUIDE.md](STEERING-GUIDE.md) - Convenciones del proyecto
   - [HOOKS-GUIDE.md](HOOKS-GUIDE.md) - Automatización de tareas
   - [MCP-GUIDE.md](MCP-GUIDE.md) - Extender capacidades
   - [GITHUB-CICD-GUIDE.md](GITHUB-CICD-GUIDE.md) - Integración continua

4. **Profundiza tu conocimiento:**
   - [BEST-PRACTICES.md](BEST-PRACTICES.md) - Optimiza tu uso de Kiro
   - [ADVANCED-FEATURES.md](ADVANCED-FEATURES.md) - Técnicas avanzadas

### Para Instructores

1. **Preparación (antes de la demo):**
   - Revisa todas las guías con anticipación
   - Verifica que tienes Node.js y Kiro instalados
   - Clona el repositorio y familiarízate con la estructura

2. **Durante la demo:**
   - **Minutos 0-15:** Sigue [VIBE-GUIDE.md](VIBE-GUIDE.md)
   - **Minutos 15-20:** Ejercicio con [EARS-GUIDE.md](EARS-GUIDE.md)
   - **Minutos 20-110:** Sigue [SPEC-GUIDE.md](SPEC-GUIDE.md) paso a paso
   - **Minutos 110-120:** Q&A con [FAQ.md](FAQ.md) a mano

3. **Recursos de apoyo:**
   - Usa `.kiro/specs/demo-task-manager/` como referencia
   - Ten las guías de características listas para consulta rápida
   - Prepara ejemplos adicionales si hay tiempo extra

## 📁 Estructura del Repositorio

```
.
├── README.md                          # Este archivo
├── FAQ.md                             # Preguntas frecuentes sobre Kiro
├── LICENSE                            # Licencia del proyecto
│
├── VIBE-GUIDE.md                      # Guía del proyecto Vibe
├── SPEC-GUIDE.md                      # Guía paso a paso del proyecto Spec
├── EARS-GUIDE.md                      # Guía del ejercicio EARS
├── STEERING-GUIDE.md                  # Guía de Steering Files
├── HOOKS-GUIDE.md                     # Guía de Agent Hooks
├── MCP-GUIDE.md                       # Guía de MCP Servers
├── GITHUB-CICD-GUIDE.md               # Guía de GitHub y CI/CD
├── BEST-PRACTICES.md                  # Mejores prácticas de Kiro
├── ADVANCED-FEATURES.md               # Funcionalidades avanzadas de Kiro
│
├── .kiro/
│   └── specs/
│       └── demo-task-manager/
│           ├── requirements.md        # Requirements con formato EARS
│           ├── design.md              # Diseño completo del proyecto
│           └── tasks.md               # Plan de implementación
│
└── examples/
    ├── vibe/
    │   └── turnout-data.csv           # Datos para proyecto Vibe
    └── spec/
        ├── valid-acta.json            # Acta correcta
        ├── invalid-acta.json          # Acta con errores
        └── anomaly-acta.json          # Acta con anomalía
```

## 🎯 Objetivos de Aprendizaje

Al completar esta demo, aprenderás:

- ✅ Diferencia entre Modo Vibe y Modo Spec
- ✅ Cómo crear y usar specs en Kiro
- ✅ Property-based testing con fast-check
- ✅ Configuración de steering files
- ✅ Configuración de agent hooks
- ✅ Configuración de MCP servers
- ✅ Mejores prácticas de uso de Kiro
- ✅ Optimización de consumo de tokens

## 🛠️ Requisitos Previos

- Node.js instalado (v18 o superior)
- Kiro IDE instalado
- Conocimientos básicos de TypeScript
- Terminal/línea de comandos

## ⚡ Inicio Rápido

1. **Clona este repositorio**
   ```bash
   git clone <url-del-repo>
   cd <nombre-del-repo>
   ```

2. **Abre en Kiro**
   ```bash
   kiro .
   ```

3. **Comienza con el FAQ**
   - Lee [FAQ.md](FAQ.md) para familiarizarte con conceptos básicos

4. **Sigue las guías en orden**
   - **Parte 1:** [VIBE-GUIDE.md](VIBE-GUIDE.md) - Proyecto Vibe (15 min)
   - **Ejercicio EARS:** [EARS-GUIDE.md](EARS-GUIDE.md) - Formato de requirements (5 min)
   - **Parte 2:** [SPEC-GUIDE.md](SPEC-GUIDE.md) - Proyecto Spec (~90 min)
   - **Características avanzadas:** Steering, Hooks, MCP (según necesidad)

## 📚 Guías y Recursos

### Guías de Proyectos
- **[VIBE-GUIDE.md](VIBE-GUIDE.md)** - Guía completa del proyecto Vibe (15 min)
- **[SPEC-GUIDE.md](SPEC-GUIDE.md)** - Guía paso a paso del proyecto Spec (~90 min)
- **[EARS-GUIDE.md](EARS-GUIDE.md)** - Ejercicio práctico de formato EARS (5 min)

### Guías de Características
- **[STEERING-GUIDE.md](STEERING-GUIDE.md)** - Configurar steering files (5-10 min)
- **[HOOKS-GUIDE.md](HOOKS-GUIDE.md)** - Configurar agent hooks (5-10 min)
- **[MCP-GUIDE.md](MCP-GUIDE.md)** - Configurar MCP servers (10-15 min)
- **[GITHUB-CICD-GUIDE.md](GITHUB-CICD-GUIDE.md)** - GitHub y CI/CD (10 min)

### Guías de Mejores Prácticas
- **[BEST-PRACTICES.md](BEST-PRACTICES.md)** - Mejores prácticas de uso de Kiro
- **[ADVANCED-FEATURES.md](ADVANCED-FEATURES.md)** - Funcionalidades avanzadas
- **[FAQ.md](FAQ.md)** - Preguntas frecuentes

### Specs del Proyecto
- **Requirements:** `.kiro/specs/demo-task-manager/requirements.md`
- **Design:** `.kiro/specs/demo-task-manager/design.md`
- **Tasks:** `.kiro/specs/demo-task-manager/tasks.md`

## 🤝 Contribuciones

Esta es una guía de demostración. Si encuentras errores o tienes sugerencias de mejora, por favor abre un issue.

## 📝 Licencia

[Especificar licencia aquí]

## 💡 Consejos para la Demo

### Para Modo Vibe (15 min)
- Mantén el ritmo rápido
- No te detengas en detalles
- Muestra la velocidad de iteración

### Para Modo Spec (resto)
- Tómate tiempo para explicar cada concepto
- Ejecuta las tareas una por una
- Muestra los tests ejecutándose
- Demuestra las características avanzadas

### Mejores Prácticas
- Usa #File para dar contexto específico
- Divide tareas complejas en pasos pequeños
- Monitorea el consumo de tokens
- Revisa el FAQ cuando tengas dudas

## 🎓 Después de la Demo

1. Experimenta con tus propios proyectos
2. Prueba crear specs para funcionalidades reales
3. Explora más características de Kiro
4. Comparte tu experiencia con el equipo

---

**¿Preguntas?** Consulta el [FAQ.md](FAQ.md) o abre un issue en este repositorio.
