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

1. **Lee el FAQ primero:** [FAQ.md](guides/FAQ.md) - Responde preguntas básicas sobre Kiro

2. **Sigue las guías en orden:**
   - **Parte 1 (15 min):** [VIBE-GUIDE.md](guides/projects/VIBE-GUIDE.md) - Desarrollo rápido
   - **Ejercicio (5 min):** [EARS-GUIDE.md](guides/projects/EARS-GUIDE.md) - Formato de requirements
   - **Parte 2 (~90 min):** [SPEC-GUIDE.md](guides/projects/SPEC-GUIDE.md) - Desarrollo estructurado

3. **Explora características avanzadas:**
   - [STEERING-GUIDE.md](guides/features/STEERING-GUIDE.md) - Convenciones del proyecto
   - [HOOKS-GUIDE.md](guides/features/HOOKS-GUIDE.md) - Automatización de tareas
   - [MCP-GUIDE.md](guides/features/MCP-GUIDE.md) - Extender capacidades
   - [GITHUB-CICD-GUIDE.md](guides/features/GITHUB-CICD-GUIDE.md) - Integración continua

4. **Profundiza tu conocimiento:**
   - [BEST-PRACTICES.md](guides/best-practices/BEST-PRACTICES.md) - Optimiza tu uso de Kiro
   - [ADVANCED-FEATURES.md](guides/best-practices/ADVANCED-FEATURES.md) - Técnicas avanzadas

## 📁 Estructura del Repositorio

```
.
├── README.md                          # Este archivo (guía principal)
├── LICENSE                            # Licencia del proyecto
├── .gitignore                         # Archivos ignorados por Git
│
├── guides/                            # Todas las guías organizadas
│   ├── DEMO-GUIDE.md                  # Guía maestra con timeline completo
│   ├── FAQ.md                         # Preguntas frecuentes
│   │
│   ├── projects/                      # Guías de proyectos
│   │   ├── VIBE-GUIDE.md              # Proyecto Vibe (15 min)
│   │   ├── SPEC-GUIDE.md              # Proyecto Spec (~90 min)
│   │   └── EARS-GUIDE.md              # Ejercicio EARS (5 min)
│   │
│   ├── features/                      # Guías de características
│   │   ├── STEERING-GUIDE.md          # Steering Files
│   │   ├── HOOKS-GUIDE.md             # Agent Hooks
│   │   ├── MCP-GUIDE.md               # MCP Servers
│   │   └── GITHUB-CICD-GUIDE.md       # GitHub y CI/CD
│   │
│   └── best-practices/                # Mejores prácticas
│       ├── BEST-PRACTICES.md          # Mejores prácticas de Kiro
│       └── ADVANCED-FEATURES.md       # Funcionalidades avanzadas
│
└── examples/                          # Archivos de ejemplo
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

- **Kiro IDE instalado** - [Descargar Kiro](https://kiro.ai)
- **Conocimientos básicos de TypeScript** (opcional pero recomendado)
- **Git instalado** (para clonar el repositorio)

**Nota:** Node.js y TypeScript se configurarán con ayuda de Kiro durante la demo. Las guías incluyen instrucciones sobre cómo pedirle a Kiro que configure el entorno.

## ⚡ Inicio Rápido

1. **Clona este repositorio**
   ```bash
   git clone https://github.com/dominickcg/demo-kiro.git
   cd demo-kiro
   ```

2. **Abre en Kiro**
   - Abre Kiro IDE
   - File → Open Folder
   - Selecciona la carpeta `demo-kiro`

3. **Comienza con el FAQ**
   - Lee [FAQ.md](guides/FAQ.md) para familiarizarte con conceptos básicos

4. **Sigue las guías en orden**
   - **Parte 1:** [VIBE-GUIDE.md](guides/projects/VIBE-GUIDE.md) - Proyecto Vibe (15 min)
   - **Ejercicio EARS:** [EARS-GUIDE.md](guides/projects/EARS-GUIDE.md) - Formato de requirements (5 min)
   - **Parte 2:** [SPEC-GUIDE.md](guides/projects/SPEC-GUIDE.md) - Proyecto Spec (~90 min)
   - **Características avanzadas:** Steering, Hooks, MCP (según necesidad)

## 📚 Guías y Recursos

### 🎯 Guía Maestra
- **[DEMO-GUIDE.md](guides/DEMO-GUIDE.md)** - Timeline completo de 2 horas paso a paso

### 📖 Guías de Proyectos
- **[VIBE-GUIDE.md](guides/projects/VIBE-GUIDE.md)** - Guía completa del proyecto Vibe (15 min)
- **[SPEC-GUIDE.md](guides/projects/SPEC-GUIDE.md)** - Guía paso a paso del proyecto Spec (~90 min)
- **[EARS-GUIDE.md](guides/projects/EARS-GUIDE.md)** - Ejercicio práctico de formato EARS (5 min)

### ⚙️ Guías de Características
- **[STEERING-GUIDE.md](guides/features/STEERING-GUIDE.md)** - Configurar steering files (5-10 min)
- **[HOOKS-GUIDE.md](guides/features/HOOKS-GUIDE.md)** - Configurar agent hooks (5-10 min)
- **[MCP-GUIDE.md](guides/features/MCP-GUIDE.md)** - Configurar MCP servers (10-15 min)
- **[GITHUB-CICD-GUIDE.md](guides/features/GITHUB-CICD-GUIDE.md)** - GitHub y CI/CD (10 min)

### 💡 Guías de Mejores Prácticas
- **[BEST-PRACTICES.md](guides/best-practices/BEST-PRACTICES.md)** - Mejores prácticas de uso de Kiro
- **[ADVANCED-FEATURES.md](guides/best-practices/ADVANCED-FEATURES.md)** - Funcionalidades avanzadas

### ❓ Preguntas Frecuentes
- **[FAQ.md](guides/FAQ.md)** - Respuestas a preguntas comunes sobre Kiro

## 🤝 Contribuciones

Esta es una guía de demostración. Si encuentras errores o tienes sugerencias de mejora, por favor abre un issue.

## 📝 Licencia

[Especificar licencia aquí]

## 💡 Consejos para Aprovechar la Demo

### Modo Vibe (15 min)
- Enfócate en la velocidad de desarrollo
- Observa cómo iterar rápidamente
- Nota la diferencia con desarrollo tradicional

### Modo Spec (resto)
- Tómate tiempo para entender cada concepto
- Ejecuta las tareas una por una
- Observa cómo los tests validan el código
- Experimenta con las características avanzadas

### Mejores Prácticas
- Usa #File para dar contexto específico a Kiro
- Divide tareas complejas en pasos pequeños
- Monitorea el consumo de tokens en el chat
- Consulta el FAQ cuando tengas dudas

## 🎓 Después de la Demo

1. **Experimenta:** Aplica lo aprendido en tus propios proyectos
2. **Practica:** Crea specs para funcionalidades reales
3. **Explora:** Descubre más características avanzadas de Kiro
4. **Comparte:** Enseña a tu equipo lo que aprendiste

---

**¿Preguntas?** Consulta el [FAQ.md](guides/FAQ.md) o abre un issue en este repositorio.
