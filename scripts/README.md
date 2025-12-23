# Claude Agents Sync Script

Script de sincronización de agentes de Claude para proyectos locales.

## Descripción

Este script permite sincronizar agentes personalizados de Claude desde un repositorio central a cualquier proyecto local. Los agentes se instalan en el directorio `.claude/agents` del proyecto.

## Características

- Interfaz interactiva con colores y emojis
- Selección individual o múltiple de agentes
- Detección automática de agentes disponibles con sus descripciones
- Soporte para instalación desde repositorio local o remoto
- **Repositorio personalizable mediante parámetro o variable de entorno**
- Validación y confirmación antes de instalar
- Resumen detallado de la sincronización
- Comando de ayuda integrado (`-h` o `--help`)

## Uso

### Sintaxis Básica

```bash
./scripts/sync-agents.sh [REPOSITORY_URL]
```

**Opciones:**
- `REPOSITORY_URL`: URL del repositorio de agentes (opcional)
- `-h, --help`: Muestra la ayuda

### Opción 1: Repositorio por Defecto

Usa el repositorio configurado por defecto:

```bash
cd /ruta/a/claude-agents
./scripts/sync-agents.sh
```

### Opción 2: Repositorio Personalizado como Parámetro

Especifica un repositorio diferente directamente:

```bash
# Desde el repositorio de tu empresa
./scripts/sync-agents.sh https://github.com/tu-empresa/company-agents.git

# Desde tu repositorio personal
./scripts/sync-agents.sh https://github.com/tu-usuario/mis-agentes.git

# Desde un repositorio privado (requiere acceso configurado)
./scripts/sync-agents.sh git@github.com:empresa/private-agents.git
```

### Opción 3: Repositorio mediante Variable de Entorno

Configura el repositorio via variable de entorno:

```bash
# Uso temporal
AGENTS_REPO=https://github.com/empresa/agents.git ./scripts/sync-agents.sh

# Configuración permanente en tu shell
export AGENTS_REPO="https://github.com/empresa/company-agents.git"
./scripts/sync-agents.sh
```

### Opción 4: Descarga y Ejecución Remota

Descarga y ejecuta el script desde internet:

```bash
# Con repositorio por defecto
curl -sSL https://raw.githubusercontent.com/juanpaconpa/claude-agents/main/scripts/sync-agents.sh | bash

# Con repositorio personalizado
curl -sSL https://raw.githubusercontent.com/juanpaconpa/claude-agents/main/scripts/sync-agents.sh | bash -s -- https://github.com/empresa/agents.git
```

### Opción 5: Instalación Global

Instala el script globalmente para usarlo desde cualquier proyecto:

```bash
# Clonar el repositorio
git clone https://github.com/juanpaconpa/claude-agents.git ~/.claude-agents

# Crear un alias simple
echo 'alias sync-agents="~/.claude-agents/scripts/sync-agents.sh"' >> ~/.bashrc
source ~/.bashrc

# O crear un alias con repositorio personalizado
echo 'alias sync-company-agents="~/.claude-agents/scripts/sync-agents.sh https://github.com/empresa/agents.git"' >> ~/.bashrc
source ~/.bashrc

# Ahora úsalo desde cualquier proyecto
cd /ruta/a/tu/proyecto
sync-agents
# o
sync-company-agents
```

## Flujo de Trabajo

### 1. Listar Agentes Disponibles

El script muestra todos los agentes disponibles con su descripción:

```
Agentes disponibles:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[1] architect
    Software architecture specialist who analyzes, evaluates...

[2] backend-py
    Backend Python Development Agent specializing in Clean...

[3] qa-backend-py
    QA Backend Python agent...
```

### 2. Seleccionar Agentes

Tienes tres opciones:

- **Opción 1**: Instalar todos los agentes
- **Opción 2**: Selección personalizada (números individuales o rangos)
- **Opción 3**: Salir

### 3. Confirmación

Para selección personalizada, el script pedirá confirmación antes de instalar:

```
Agentes seleccionados: architect backend-py
¿Continuar con la instalación? [s/N]:
```

### 4. Resultado

El script mostrará un resumen de la sincronización:

```
╔═══════════════════════════════════════════════╗
║              Resumen de sincronización        ║
╠═══════════════════════════════════════════════╣
║  Agentes sincronizados: 2
║  Errores:               0
║  Ubicación:             .claude/agents
╚═══════════════════════════════════════════════╝
```

## Ejemplos de Uso

### Instalar todos los agentes

```bash
./scripts/sync-agents.sh
# Selecciona opción [1]
```

### Instalar agentes específicos

```bash
./scripts/sync-agents.sh
# Selecciona opción [2]
# Ingresa: 1 3 (para instalar architect y qa-backend-py)
```

### Instalar rango de agentes

```bash
./scripts/sync-agents.sh
# Selecciona opción [2]
# Ingresa: 1-2 (para instalar architect y backend-py)
```

## Configuración

### Cambiar el repositorio por defecto

Si deseas cambiar el repositorio por defecto permanentemente, edita la variable `DEFAULT_AGENTS_REPO` en el script:

```bash
DEFAULT_AGENTS_REPO="https://github.com/tu-empresa/company-agents.git"
```

### Cambiar el directorio de instalación

Edita la variable `PROJECT_AGENTS_DIR` en el script:

```bash
PROJECT_AGENTS_DIR=".claude/custom-agents"
```

### Configuración para Equipos

Para equipos que trabajan con repositorios de agentes personalizados, se recomienda:

**Opción A: Variable de Entorno Global**
```bash
# En el archivo de configuración del equipo (.bashrc, .zshrc, etc.)
export AGENTS_REPO="https://github.com/empresa/company-claude-agents.git"
```

**Opción B: Alias Personalizado**
```bash
# Crear alias específico para el equipo
alias sync-company-agents="bash /ruta/sync-agents.sh https://github.com/empresa/agents.git"
```

**Opción C: Fork del Repositorio**
```bash
# 1. Hacer fork del repositorio
# 2. Modificar DEFAULT_AGENTS_REPO en el script
# 3. Compartir el fork con el equipo
```

## Estructura de Agentes

Los agentes deben seguir esta estructura en el repositorio:

```
claude-agents/
├── agents/
│   ├── architect.md
│   ├── backend-py.md
│   └── qa-backend-py.md
└── scripts/
    └── sync-agents.sh
```

Cada archivo de agente debe tener un frontmatter YAML con al menos:

```yaml
---
name: agent-name
description: Agent description
model: inherit
color: blue
---

# Agent content...
```

## Requisitos

- Bash 4.0+
- Git
- Permisos de escritura en el proyecto

## Solución de Problemas

### Error: "No se pudo acceder a los agentes"

- Verifica tu conexión a internet
- Verifica que la URL del repositorio sea correcta
- Verifica que tengas git instalado

### Error: "No se encontraron agentes disponibles"

- Verifica que el repositorio tenga una carpeta `agents/`
- Verifica que existan archivos `.md` en la carpeta

### Error al copiar agentes

- Verifica que tengas permisos de escritura en el directorio del proyecto
- Verifica que el directorio `.claude/` sea accesible

## Contribuir

Para agregar nuevos agentes al repositorio:

1. Crea un archivo `.md` en la carpeta `agents/`
2. Incluye el frontmatter YAML con `name`, `description`, `model`, y `color`
3. Escribe la definición del agente
4. Haz commit y push al repositorio

## Licencia

MIT License - Usa, modifica y comparte libremente.