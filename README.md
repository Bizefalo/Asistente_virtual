# 🚀 Weaviable - Sistema RAG con Weaviate y Ollama

Un sistema RAG (Retrieval-Augmented Generation) completo que permite procesar documentos PDF, almacenarlos en una base de datos vectorial y realizar consultas inteligentes usando modelos de lenguaje locales.

[![Python](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Docker](https://img.shields.io/badge/docker-required-blue.svg)](https://www.docker.com/)
[![Ollama](https://img.shields.io/badge/ollama-local--llm-green.svg)](https://ollama.ai/)
[![Weaviate](https://img.shields.io/badge/weaviate-vector--db-orange.svg)](https://weaviate.io/)

## 📋 Tabla de Contenidos

- [🌟 Características](#-características)
- [🏗️ Arquitectura](#️-arquitectura)
- [📋 Requisitos](#-requisitos)
- [⚡ Instalación Rápida](#-instalación-rápida)
- [🚀 Uso](#-uso)
- [📁 Estructura del Proyecto](#-estructura-del-proyecto)
- [💡 Ejemplos de Consultas](#-ejemplos-de-consultas)
- [🔧 Troubleshooting](#-troubleshooting)
- [📖 Documentación Completa](#-documentación-completa)

## 🌟 Características

- 📖 **Procesamiento de PDFs** - Extrae y procesa documentos automáticamente
- 🧠 **Embeddings locales** - Genera vectores usando Ollama (sin APIs externas)
- 💾 **Base de datos vectorial** - Almacena conocimiento en Weaviate local
- 🔍 **Búsqueda híbrida** - Combina búsqueda vectorial y por texto
- 💬 **Chat interactivo** - Interfaz de terminal para consultas naturales
- 🐳 **Fácil deployment** - Todo containerizado con Docker

## 🏗️ Arquitectura

```
PDF → Chunks → Embeddings → Weaviate → Consultas → Ollama → Respuestas
```

| Componente | Tecnología | Puerto |
|------------|------------|--------|
| **Vector DB** | Weaviate | 8080 |
| **LLM Local** | Ollama | 11434 |
| **Embeddings** | llama3.1 | - |
| **Chat** | Python CLI | - |

## 📋 Requisitos

- **Python** 3.11+
- **Docker Desktop** (para Weaviate)
- **Ollama** (para LLMs locales)
- **8GB RAM** mínimo

## ⚡ Instalación Rápida

### 1. Instalar dependencias Python
```bash
pip install weaviate-client==4.16.10 pypdf requests
```

### 2. Instalar Ollama
```bash
# Descargar desde: https://ollama.ai/download
ollama pull llama3.1
ollama pull gemma3:1b
```

### 3. Iniciar servicios
```bash
# Terminal 1: Ollama
ollama serve

# Terminal 2: Weaviate (Docker)
docker-compose up -d
```

### 4. Procesar datos
```bash
python main.py
```

### 5. ¡Usar el chat interactivo!
```bash
python chat_interactivo.py
```

**¡Ahora puedes hacer preguntas como:**
- `"Recomiéndame un viaje familiar con rating alto"`
- `"¿Qué destinos son mejores para aventura?"`
- `"Busco algo romántico para mi pareja"`
- `"¿Cuál es el viaje con mejor rating?"`

## 🚀 Uso

### 💬 Chat Interactivo (¡Recomendado!)
```bash
python chat_interactivo.py
```

**Una vez iniciado el chat, puedes hacer consultas como:**

#### Consultas por Tipo de Viaje:
```
🔍 Tu pregunta: "Busco un viaje romántico"
🔍 Tu pregunta: "¿Qué aventuras hay disponibles?"
🔍 Tu pregunta: "Recomiéndame algo familiar"
```

#### Consultas por Rating/Calidad:
```
🔍 Tu pregunta: "¿Cuál es el viaje con mejor rating?"
🔍 Tu pregunta: "Muéstrame opciones con rating mayor a 4"
🔍 Tu pregunta: "¿Qué destino tiene las mejores calificaciones?"
```

#### Consultas por Características:
```
🔍 Tu pregunta: "¿Qué viajes duran más de una semana?"
🔍 Tu pregunta: "Busco algo que se pueda hacer en auto"
🔍 Tu pregunta: "¿Cuáles son los destinos más populares?"
```

**💡 Tip:** Escribe `"salir"` para terminar el chat.

### Uso Programático
```python
from clusteConection import get_weaviate_client
from rag_query import query_rag

client = get_weaviate_client()
respuesta = query_rag(client, "¿Cuál es el mejor destino?")
print(respuesta)
```

## 📁 Estructura del Proyecto

```
Weaviable/
├── 🎮 chat_interactivo.py        # ⭐ Interfaz principal (¡Úsalo para hacer preguntas!)
├── 🔧 main.py                    # Procesamiento inicial de datos
├── 🔌 clusteConection.py         # Conexión a Weaviate local (sin autenticación)
├── 📄 pdfs.py                    # Procesamiento PDF
├── 🧠 embeddings.py              # Generación embeddings con Ollama
├── 📤 subir_chunks.py            # Carga de datos vectoriales
├── 🔍 rag_query.py               # Sistema de consultas RAG
├── 🐳 docker-compose.yml         # Configuración Weaviate local
└── 📚 docs/                      # Documentación completa
```

## 🎯 Flujo de Uso para Estudiantes

### Primera vez (Setup completo):
```bash
# 1. Instalar dependencias
pip install weaviate-client==4.16.10 pypdf requests

# 2. Descargar Ollama y modelos
ollama pull llama3.1

# 3. Iniciar servicios (en terminales separados)
ollama serve
docker-compose up -d

# 4. Procesar datos inicial
python main.py

# 5. ¡Empezar a hacer preguntas!
python chat_interactivo.py
```

### Uso normal (servicios ya configurados):
```bash
# 1. Iniciar servicios
ollama serve
docker-compose up -d

# 2. ¡Chat directo!
python chat_interactivo.py
```

## 💡 Ejemplos de Consultas

### Por Tipo de Viaje
```
"Busco un viaje romántico"
"¿Qué aventuras hay disponibles?"
"Recomiéndame algo familiar"
```

### Por Rating/Calidad
```
"¿Cuál es el viaje con mejor rating?"
"Muéstrame opciones con rating mayor a 4"
"¿Qué destino tiene las mejores calificaciones?"
```

### Por Características
```
"¿Qué viajes duran más de una semana?"
"Busco algo que se pueda hacer en auto"
"¿Cuáles son los destinos más populares?"
```

## 🔧 Troubleshooting

### ❌ Error "Connection refused"
```bash
# Verificar servicios
docker-compose ps
ollama list

# Reiniciar
docker-compose restart
```

### ❌ "No se encontraron documentos"
```bash
# Diagnosticar
python diagnostico.py

# Recargar datos
python limpiar_datos.py
python main.py
```

### ❌ Error de modelo Ollama
```bash
# Verificar modelos
ollama list

# Descargar si falta
ollama pull llama3.1
```

## 📊 Performance

| Métrica | Valor |
|---------|-------|
| **Tiempo de respuesta** | ~10-30 segundos |
| **Procesamiento PDF** | ~30 seg/MB |
| **Dimensiones embedding** | 4096 |
| **Precisión búsqueda** | ~85-90% |

## 📖 Documentación Completa

- 📚 [**Guía Completa para Estudiantes**](GUIA_COMPLETA_ESTUDIANTES.md) - Tutorial paso a paso completo
- 🔄 [**Guía de Reinicio**](GUIA_REINICIO.md) - Cómo reiniciar el sistema
- 🏗️ [**Estructura del Proyecto**](ESTRUCTURA_PROYECTO.md) - Arquitectura detallada

## 🚀 Quick Start para Estudiantes

### 🎯 **¿Primera vez? (Setup completo)**
```bash
ollama serve → docker-compose up -d → python main.py → python chat_interactivo.py
```

### ⚡ **¿Ya tienes datos? (Uso normal)**
```bash
ollama serve → docker-compose up -d → python chat_interactivo.py
```

### 🆘 **¿Problemas?**
```bash
python diagnostico.py
```

### 💬 **Una vez en el chat, prueba preguntas como:**
- `"Recomiéndame un viaje familiar"`
- `"¿Cuál tiene el mejor rating?"`
- `"Busco aventuras en montaña"`
- `"¿Qué destinos duran una semana?"`

## 🤝 Contribuir

1. Fork el repo
2. Crea tu branch (`git checkout -b feature/nueva-funcionalidad`)
3. Commit (`git commit -m 'Agrega nueva funcionalidad'`)
4. Push (`git push origin feature/nueva-funcionalidad`)
5. Abre un Pull Request

## 📝 Changelog

### v1.0.0 (2025-09-25)
- ✅ Sistema RAG completo
- ✅ Chat interactivo
- ✅ Búsqueda híbrida
- ✅ Docker local
- ✅ Guías completas

## 🙏 Créditos

- [Weaviate](https://weaviate.io/) - Vector database
- [Ollama](https://ollama.ai/) - Local LLMs
- [PyPDF](https://pypdf.readthedocs.io/) - PDF processing

## 📄 Licencia

MIT License - ver [LICENSE](LICENSE) para detalles.

---

<div align="center">

**⭐ ¿Te gusta el proyecto? ¡Dale una estrella!**

[🐛 Reportar Bug](https://github.com/tu-usuario/weaviable/issues) • [✨ Pedir Feature](https://github.com/tu-usuario/weaviable/issues) • [📖 Documentación](docs/)

**Hecho con ❤️ usando Python, Weaviate y Ollama**

</div>

