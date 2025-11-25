# Guía de MCP Servers

**Duración:** 10-15 minutos  
**Objetivo:** Aprender a configurar y usar MCP Servers para extender las capacidades de Kiro

## ¿Qué es MCP?

**MCP (Model Context Protocol)** es un protocolo estándar que permite a Kiro conectarse con herramientas y servicios externos. Piensa en MCP como "plugins" que le dan a Kiro nuevas capacidades.

### ¿Para qué sirve?

- **Acceso a sistemas externos:** Bases de datos, APIs, servicios cloud
- **Herramientas especializadas:** Análisis de código, búsqueda avanzada, procesamiento de datos
- **Integración con servicios:** GitHub, Slack, Jira, etc.
- **Capacidades personalizadas:** Crear tus propias herramientas para Kiro

### Ejemplos de uso

- Leer/escribir archivos del sistema con permisos específicos
- Consultar bases de datos directamente
- Buscar en documentación externa
- Interactuar con APIs de terceros
- Ejecutar análisis de código especializado

---

## Conceptos Clave

### MCP Server
Un programa que expone herramientas (tools) que Kiro puede usar. Cada servidor puede ofrecer múltiples herramientas.

### MCP Tool
Una función específica que Kiro puede invocar. Por ejemplo: `read_file`, `search_database`, `analyze_code`.

### MCP Client
Kiro actúa como cliente MCP, conectándose a servidores y usando sus herramientas.

---

## Cuándo Configurar MCP Servers

⏰ **Momento ideal:** Al final del proyecto, cuando necesitas capacidades avanzadas

**Flujo recomendado:**
1. Desarrollar funcionalidad básica
2. Identificar necesidades de integración externa
3. Configurar MCP server apropiado
4. Usar las nuevas capacidades

**Nota:** MCP es una característica avanzada. No es necesaria para proyectos básicos.

---

## Servidores MCP Disponibles

### Servidores Oficiales

| Servidor | Descripción | Herramientas |
|----------|-------------|--------------|
| `filesystem` | Acceso al sistema de archivos | read_file, write_file, list_directory |
| `github` | Integración con GitHub | create_issue, search_repos, get_pr |
| `postgres` | Consultas a PostgreSQL | query, list_tables, describe_table |
| `sqlite` | Consultas a SQLite | query, list_tables |
| `fetch` | Peticiones HTTP | get, post, put, delete |
| `aws-docs` | Documentación de AWS | search_docs, get_service_info |

### Servidores de la Comunidad

Hay muchos servidores creados por la comunidad. Busca en:
- GitHub: `mcp-server-*`
- Documentación oficial de MCP
- Comunidad de Kiro

---

## Configuración de MCP Servers

### Ubicación del Archivo de Configuración

**Workspace (proyecto específico):**
```
.kiro/settings/mcp.json
```

**User (global, todos los proyectos):**
```
~/.kiro/settings/mcp.json
```

**Precedencia:** User < Workspace1 < Workspace2 (el último sobrescribe)

### Estructura del Archivo mcp.json

```json
{
  "mcpServers": {
    "nombre-del-servidor": {
      "command": "comando-para-ejecutar",
      "args": ["argumentos", "del", "comando"],
      "env": {
        "VARIABLE_ENTORNO": "valor"
      },
      "disabled": false,
      "autoApprove": ["herramienta1", "herramienta2"]
    }
  }
}
```

---

## Ejemplo 1: Servidor Filesystem

### Configuración

**Crear archivo:** `.kiro/settings/mcp.json`

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "uvx",
      "args": ["mcp-server-filesystem"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      },
      "disabled": false,
      "autoApprove": ["read_file", "list_directory"]
    }
  }
}
```

### Instalación de uvx

MCP servers suelen ejecutarse con `uvx`, que requiere `uv` (gestor de paquetes Python).

**Instalar uv:**

**Windows:**
```bash
pip install uv
```

**macOS/Linux:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Verificar instalación:**
```bash
uv --version
uvx --version
```

**Nota:** `uvx` descarga y ejecuta el servidor automáticamente. No necesitas instalar el servidor por separado.

### Herramientas Disponibles

Una vez configurado, Kiro puede usar:

- `read_file` - Leer contenido de archivos
- `write_file` - Escribir en archivos
- `list_directory` - Listar contenido de carpetas
- `create_directory` - Crear carpetas
- `move_file` - Mover/renombrar archivos
- `delete_file` - Eliminar archivos

### Uso en Kiro

**Prompt:**
```
Usando las herramientas MCP, lista todos los archivos JSON en la carpeta examples/spec/
```

**Kiro usará:** `list_directory` del servidor filesystem

**Prompt:**
```
Lee el contenido del archivo examples/spec/valid-acta.json usando MCP
```

**Kiro usará:** `read_file` del servidor filesystem

---

## Ejemplo 2: Servidor AWS Documentation

### Configuración

**Agregar a:** `.kiro/settings/mcp.json`

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "uvx",
      "args": ["mcp-server-filesystem"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      },
      "disabled": false,
      "autoApprove": ["read_file", "list_directory"]
    },
    "aws-docs": {
      "command": "uvx",
      "args": ["awslabs.aws-documentation-mcp-server@latest"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

### Herramientas Disponibles

- `search_docs` - Buscar en documentación de AWS
- `get_service_info` - Obtener información de servicios AWS

### Uso en Kiro

**Prompt:**
```
Usando MCP, busca información sobre AWS Lambda en la documentación oficial
```

**Kiro usará:** `search_docs` del servidor aws-docs

---

## Auto-Approve: Aprobación Automática

### ¿Qué es autoApprove?

Por defecto, Kiro pide confirmación antes de usar herramientas MCP. Con `autoApprove`, puedes especificar herramientas que se ejecuten sin confirmación.

### Configuración

```json
{
  "autoApprove": ["read_file", "list_directory"]
}
```

### Cuándo usar

✅ **Usar autoApprove para:**
- Operaciones de solo lectura (read_file, list_directory)
- Herramientas que usas frecuentemente
- Operaciones seguras sin efectos secundarios

❌ **NO usar autoApprove para:**
- Operaciones de escritura (write_file, delete_file)
- Operaciones destructivas
- Herramientas que modifican datos externos
- Operaciones con efectos secundarios importantes

---

## Verificar Conexión de MCP Servers

### Método 1: Panel de MCP Servers

1. Abre el panel de MCP Servers en Kiro
2. Busca tu servidor en la lista
3. Verifica el estado: ✓ Conectado o ✗ Error

### Método 2: Command Palette

1. Abre Command Palette: `Ctrl+Shift+P`
2. Busca: "MCP"
3. Selecciona: "View MCP Servers"
4. Revisa el estado de cada servidor

### Método 3: Probar una Herramienta

**Prompt:**
```
Lista las herramientas MCP disponibles
```

Kiro mostrará todos los servidores conectados y sus herramientas.

---

## Reconectar Servidores

### Cuándo reconectar

- Después de cambiar la configuración en mcp.json
- Si un servidor muestra error
- Después de instalar/actualizar un servidor

### Cómo reconectar

**Opción 1: Desde el panel**
1. Abre el panel de MCP Servers
2. Haz clic en el botón de reconectar junto al servidor

**Opción 2: Desde Command Palette**
1. `Ctrl+Shift+P` → "Reconnect MCP Servers"

**Opción 3: Reiniciar Kiro**
- Los servidores se reconectan automáticamente al iniciar Kiro

---

## Troubleshooting

### El servidor no se conecta

**Posibles causas:**
- `uv` o `uvx` no instalados
- Comando incorrecto en la configuración
- Servidor no existe o nombre incorrecto
- Error en la sintaxis del JSON

**Solución:**
1. Verifica que `uvx --version` funciona
2. Revisa la sintaxis del mcp.json (usa un validador JSON)
3. Verifica el nombre del servidor en la documentación oficial
4. Revisa los logs del servidor en el panel de MCP

### Las herramientas no aparecen

**Posibles causas:**
- Servidor desconectado
- Servidor deshabilitado (disabled: true)
- Error al iniciar el servidor

**Solución:**
1. Verifica que disabled: false
2. Reconecta el servidor
3. Revisa los logs para errores específicos

### Kiro no usa las herramientas MCP

**Posibles causas:**
- Prompt no es claro sobre usar MCP
- Herramienta no apropiada para la tarea
- Kiro prefiere usar capacidades nativas

**Solución:**
1. Sé explícito: "Usando herramientas MCP, ..."
2. Verifica que la herramienta existe
3. Pregunta: "¿Qué herramientas MCP tienes disponibles?"

---

## Ejemplo de Uso en la Demo

Durante el proyecto Spec, configuramos MCP filesystem para:

1. **Listar archivos de ejemplo:**
   ```
   Usando MCP, lista los archivos en examples/spec/
   ```

2. **Leer actas de ejemplo:**
   ```
   Usando MCP, lee el contenido de examples/spec/valid-acta.json
   ```

3. **Verificar estructura:**
   ```
   Usando MCP, lista la estructura completa del proyecto
   ```

**Beneficio:** Kiro puede explorar el sistema de archivos de forma más flexible.

---

## MCP Servers Avanzados

### Crear tu Propio MCP Server

Puedes crear servidores MCP personalizados usando:
- Python con `fastmcp`
- TypeScript con `@modelcontextprotocol/sdk`
- Otros lenguajes con implementaciones de MCP

**Ejemplo básico (Python):**
```python
from fastmcp import FastMCP

mcp = FastMCP("mi-servidor")

@mcp.tool()
def mi_herramienta(parametro: str) -> str:
    """Descripción de mi herramienta"""
    return f"Resultado: {parametro}"

if __name__ == "__main__":
    mcp.run()
```

### Configurar Servidor Personalizado

```json
{
  "mcpServers": {
    "mi-servidor": {
      "command": "python",
      "args": ["path/to/mi-servidor.py"],
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

---

## Configuración Multi-Workspace

### Escenario

Tienes múltiples proyectos con diferentes necesidades de MCP.

### Solución

**User config (~/.kiro/settings/mcp.json):**
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "uvx",
      "args": ["mcp-server-filesystem"],
      "disabled": false,
      "autoApprove": ["read_file", "list_directory"]
    }
  }
}
```

**Workspace config (.kiro/settings/mcp.json):**
```json
{
  "mcpServers": {
    "postgres": {
      "command": "uvx",
      "args": ["mcp-server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://localhost/mydb"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

**Resultado:** El workspace tiene acceso a filesystem (user) + postgres (workspace)

---

## Mejores Prácticas

### ✅ Hacer

- Configurar MCP cuando realmente lo necesites
- Usar autoApprove solo para operaciones seguras
- Documentar servidores MCP en el README del proyecto
- Probar herramientas MCP antes de usarlas en producción
- Mantener configuración de MCP en control de versiones

### ❌ Evitar

- Configurar muchos servidores que no usas
- autoApprove en operaciones destructivas
- Credenciales en texto plano en mcp.json (usa variables de entorno)
- Servidores MCP de fuentes no confiables
- Depender de MCP para funcionalidad básica

---

## Seguridad

### Consideraciones

- **Permisos:** MCP servers tienen acceso según lo que permitas
- **Credenciales:** Usa variables de entorno, no texto plano
- **Fuentes confiables:** Solo usa servidores de fuentes verificadas
- **Auto-approve:** Úsalo con precaución

### Ejemplo Seguro

```json
{
  "mcpServers": {
    "database": {
      "command": "uvx",
      "args": ["mcp-server-postgres"],
      "env": {
        "DATABASE_URL": "${DATABASE_URL}"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Define `DATABASE_URL` en tu entorno, no en el archivo.

---

## Recursos Adicionales

- **Documentación oficial de MCP:** https://modelcontextprotocol.io
- **Repositorio de servidores:** Busca `mcp-server-*` en GitHub
- **Crear servidores:** Documentación de `fastmcp` y `@modelcontextprotocol/sdk`
- **Comunidad:** Foros y Discord de Kiro

---

## Siguiente Paso

Ahora que entiendes MCP Servers, puedes:
1. Configurar servidores para tus necesidades específicas
2. Explorar servidores de la comunidad
3. Crear tus propios servidores MCP personalizados
4. Integrar Kiro con tus herramientas y servicios

**Archivos relacionados:**
- `BEST-PRACTICES.md` - Mejores prácticas de uso de Kiro
- `ADVANCED-FEATURES.md` - Características avanzadas de Kiro
