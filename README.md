# Claude Agents Repository

Repositorio centralizado de agentes personalizados para Claude Code. Facilita la instalación y sincronización de agentes especializados en diferentes proyectos de desarrollo.

## Descripción

Este repositorio proporciona una colección de agentes de Claude especializados y un script de sincronización que permite instalarlos fácilmente en cualquier proyecto local. Los agentes están diseñados para tareas específicas de desarrollo, desde arquitectura de software hasta testing y QA.

## Agentes Disponibles

### 1. Architect Agent (`architect.md`)
**Especialista en Arquitectura de Software**

Agente enfocado en análisis, evaluación y recomendación de soluciones arquitectónicas sin escribir código de implementación.

**Capacidades:**
- Análisis profundo de arquitectura de proyectos
- Evaluación de patrones de diseño (Clean Architecture, Hexagonal, etc.)
- Recomendaciones de arquitectura con pros/cons
- Planificación detallada de desarrollo por fases
- Generación de diagramas (Mermaid)
- Estimaciones de tiempo y recursos
- Documentación técnica completa (ADRs)

**Cuándo usar:**
- Diseño de nuevas funcionalidades
- Refactorización de sistemas existentes
- Evaluación de opciones técnicas
- Planificación de proyectos
- Documentación de arquitectura

### 2. Backend Python Agent (`backend-py.md`)
**Desarrollo Backend Python con Clean Architecture**

Agente especializado en desarrollo backend Python usando Clean Architecture y Hexagonal Architecture (Ports & Adapters).

**Stack Tecnológico:**
- FastAPI 0.68.2+
- SQLAlchemy 2.0+ (PostgreSQL)
- MongoEngine (MongoDB)
- Alembic 1.14.0+
- Python 3.11+

**Capacidades:**
- Implementación de Clean Architecture/Hexagonal Architecture
- Desarrollo de APIs REST con FastAPI
- Gestión de bases de datos (PostgreSQL, MongoDB)
- Migraciones con Alembic
- Aplicación de principios SOLID
- Patrones de diseño (Repository, Interactor, DTO)
- Seguridad y autenticación (JWT, OAuth 2.0)
- Optimización de queries y performance

**Cuándo usar:**
- Desarrollo de APIs REST
- Implementación de casos de uso (Interactors)
- Creación de repositorios y adaptadores
- Migraciones de base de datos
- Refactorización hacia arquitectura limpia

### 3. QA Backend Python Agent (`qa-backend-py.md`)
**Testing y QA para Backend Python**

Agente especializado en testing, QA y chaos engineering para sistemas backend Python.

**Capacidades:**
- Testing unitario con Pytest
- Testing de integración
- Testing end-to-end
- Chaos engineering
- Cobertura de código (>90% objetivo)
- Testing de performance
- Testing de seguridad
- Generación de fixtures y mocks
- Análisis de código estático

**Cuándo usar:**
- Escribir tests unitarios e integración
- Aumentar cobertura de código
- Implementar chaos engineering
- Validar seguridad del código
- Testing de performance

## Instalación

### Método 1: Script de Sincronización (Recomendado)

El método más fácil y rápido para instalar agentes:

```bash
# Clonar el repositorio
git clone https://github.com/juanpaconpa/claude-agents.git
cd claude-agents

# Ejecutar el script de sincronización
./scripts/sync-agents.sh
```

### Método 2: Instalación Remota

Instalar sin clonar el repositorio:

```bash
# Instalar con repositorio por defecto
curl -sSL https://raw.githubusercontent.com/juanpaconpa/claude-agents/main/scripts/sync-agents.sh | bash

# Instalar con repositorio personalizado
curl -sSL https://raw.githubusercontent.com/juanpaconpa/claude-agents/main/scripts/sync-agents.sh | bash -s -- https://github.com/tu-empresa/agents.git
```

### Método 3: Instalación Global

Para usar en cualquier proyecto:

```bash
# Clonar en directorio home
git clone https://github.com/juanpaconpa/claude-agents.git ~/.claude-agents

# Crear alias
echo 'alias sync-agents="~/.claude-agents/scripts/sync-agents.sh"' >> ~/.bashrc
source ~/.bashrc

# Usar desde cualquier proyecto
cd /tu/proyecto
sync-agents
```

### Método 4: Manual

Copiar manualmente los agentes:

```bash
# Crear directorio de agentes
mkdir -p .claude/agents

# Copiar agentes deseados
cp claude-agents/agents/architect.md .claude/agents/
cp claude-agents/agents/backend-py.md .claude/agents/
cp claude-agents/agents/qa-backend-py.md .claude/agents/
```

## Uso del Script de Sincronización

### Sintaxis

```bash
./scripts/sync-agents.sh [REPOSITORY_URL]
```

### Opciones

- `REPOSITORY_URL`: URL del repositorio de agentes (opcional)
- `-h, --help`: Muestra la ayuda

### Ejemplos

**Uso básico:**
```bash
./scripts/sync-agents.sh
```

**Con repositorio personalizado:**
```bash
# Como parámetro
./scripts/sync-agents.sh https://github.com/empresa/company-agents.git

# Como variable de entorno
AGENTS_REPO=https://github.com/empresa/agents.git ./scripts/sync-agents.sh

# Exportar variable (permanente)
export AGENTS_REPO="https://github.com/empresa/agents.git"
./scripts/sync-agents.sh
```

**Selección de agentes:**
- **Opción 1**: Instalar todos los agentes
- **Opción 2**: Selección personalizada (números individuales: `1 3` o rangos: `1-3`)
- **Opción 3**: Salir

### Flujo de Trabajo

1. El script muestra todos los agentes disponibles con sus descripciones
2. Seleccionas qué agentes instalar
3. Confirmas la instalación (en modo personalizado)
4. Los agentes se copian a `.claude/agents/`
5. Se muestra un resumen de la sincronización

## Estructura del Proyecto

```
claude-agents/
├── .gitignore
├── .idea/                      # IntelliJ IDEA config
├── README.md                   # Este archivo
├── agents/                     # Agentes de Claude
│   ├── architect.md           # Agente de arquitectura
│   ├── backend-py.md          # Agente de backend Python
│   └── qa-backend-py.md       # Agente de QA/testing
└── scripts/                    # Scripts de utilidad
    ├── sync-agents.sh         # Script de sincronización
    ├── README.md              # Documentación del script
    └── QUICKSTART.md          # Guía rápida
```

## Configuración para Equipos

### Opción A: Variable de Entorno Global

Configurar para todo el equipo en sus archivos de shell:

```bash
# En .bashrc, .zshrc, etc.
export AGENTS_REPO="https://github.com/empresa/company-claude-agents.git"
```

### Opción B: Alias Personalizado

Crear un alias específico para el equipo:

```bash
alias sync-company-agents="~/.claude-agents/scripts/sync-agents.sh https://github.com/empresa/agents.git"
```

### Opción C: Fork del Repositorio

1. Hacer fork de este repositorio
2. Modificar `DEFAULT_AGENTS_REPO` en `scripts/sync-agents.sh`
3. Agregar/modificar agentes según necesidades del equipo
4. Compartir el fork con el equipo

## Uso de los Agentes

Una vez instalados, los agentes están disponibles en Claude Code:

### En Claude Code CLI

```bash
# Los agentes están automáticamente disponibles
# Claude Code los carga desde .claude/agents/
```

### Invocar un Agente

Los agentes se invocan basándose en el contexto de tu solicitud. Por ejemplo:

- **Architect**: "Analiza la arquitectura de este proyecto y recomienda cómo agregar autenticación"
- **Backend-Py**: "Implementa un interactor para crear usuarios siguiendo Clean Architecture"
- **QA**: "Escribe tests unitarios para este interactor con >90% de cobertura"

## Crear Nuevos Agentes

### Estructura de un Agente

Cada agente es un archivo Markdown con frontmatter YAML:

```markdown
---
name: agent-name
description: Brief description of the agent
model: inherit
color: blue
---

# Agent Title

Your agent prompt here...
```

### Campos del Frontmatter

- `name`: Identificador único del agente (kebab-case)
- `description`: Descripción breve (1 línea)
- `model`: Modelo a usar (`inherit`, `sonnet`, `opus`, `haiku`)
- `color`: Color para la UI (`blue`, `green`, `yellow`, `red`, `purple`, `cyan`)

### Ejemplo

```markdown
---
name: frontend-react
description: React frontend development agent specializing in TypeScript and modern React patterns
model: inherit
color: cyan
---

# Frontend React Agent

You are a specialized React frontend development agent...
```

## Contribuir

### Agregar un Nuevo Agente

1. Fork este repositorio
2. Crea un nuevo archivo en `agents/` siguiendo la estructura
3. Prueba el agente localmente
4. Crea un Pull Request con descripción detallada

### Mejorar un Agente Existente

1. Fork el repositorio
2. Modifica el agente en `agents/`
3. Documenta los cambios
4. Crea un Pull Request

### Reportar Issues

Si encuentras problemas:

1. Verifica que no exista un issue similar
2. Crea un nuevo issue con:
   - Descripción clara del problema
   - Pasos para reproducir
   - Comportamiento esperado vs actual
   - Logs relevantes

## Casos de Uso

### Startup con Clean Architecture

```bash
# Instalar agentes de arquitectura y backend
./scripts/sync-agents.sh
# Selecciona: 2 → Ingresa: 1 2

# Usar el agente de arquitectura
"Analiza este proyecto y recomienda la mejor forma de implementar un sistema de autenticación"

# Usar el agente de backend
"Implementa el sistema de autenticación siguiendo las recomendaciones del arquitecto"
```

### Empresa con Repositorio Privado

```bash
# Configurar repo privado de la empresa
export AGENTS_REPO="git@github.com:empresa/private-agents.git"

# Instalar agentes de empresa
sync-agents

# Los agentes personalizados ahora están disponibles
```

### Freelancer con Múltiples Clientes

```bash
# Cliente A
alias sync-agents-clienta="sync-agents https://github.com/clienta/agents.git"

# Cliente B
alias sync-agents-clientb="sync-agents https://github.com/clientb/agents.git"

# Cambiar entre proyectos fácilmente
cd ~/projects/clienta && sync-agents-clienta
cd ~/projects/clientb && sync-agents-clientb
```

## Actualización de Agentes

Para actualizar agentes a la última versión:

```bash
# Ejecutar nuevamente el script
./scripts/sync-agents.sh

# Seleccionar los agentes a actualizar
# Los archivos existentes serán sobrescritos
```

## Requisitos

- Git
- Bash 4.0+
- Claude Code CLI
- Permisos de escritura en el proyecto

## Solución de Problemas

### Los agentes no aparecen en Claude Code

1. Verifica que los archivos estén en `.claude/agents/`
2. Reinicia Claude Code
3. Verifica que los archivos tengan el formato correcto

### Error al clonar repositorio

1. Verifica tu conexión a internet
2. Verifica que tengas acceso al repositorio
3. Para repos privados, configura SSH o tokens de acceso

### Agentes no se sincronizan

1. Verifica que la carpeta `agents/` exista en el repo
2. Verifica que los archivos `.md` estén presentes
3. Ejecuta con `bash -x` para debug: `bash -x scripts/sync-agents.sh`

## Recursos

- [Documentación del Script](./scripts/README.md) - Documentación completa del script de sincronización
- [Guía Rápida](./scripts/QUICKSTART.md) - Inicio rápido
- [Claude Code Documentation](https://docs.anthropic.com/claude/docs) - Documentación oficial de Claude

## Licencia

MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Autor

Desarrollado por Juan Pablo Contreras

## Contribuidores

¡Las contribuciones son bienvenidas! Gracias a todos los que han contribuido a este proyecto.

---

**¿Preguntas o sugerencias?** Abre un issue o contacta al equipo.

**¿Te gustó este proyecto?** Dale una estrella en GitHub.