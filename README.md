# Proyecto Weaviate + Ollama + PDF RAG

Esta guía explica cómo conectar Weaviate Cloud con Ollama local para vectorizar y consultar datos extraídos de un PDF.

## Requisitos
- Python 3.13.2
- Weaviate Cloud (URL y API Key)
- Ollama instalado en tu máquina local
- Modelo LLM descargado en Ollama (ejemplo: llama3)

## Instalación de dependencias

```powershell
pip install weaviate-client pypdf requests
```


## Iniciar Ollama y descargar modelo

```powershell
ollama serve
ollama pull llama3
```

## Ejecución de scripts

1. Validar conexión y crear colección:
   ```powershell
   python .\clusteConection.py
   ```
2. Procesar PDF, subir datos y hacer preguntas:
   ```powershell
   python .\main.py
   ```

## Flujo de trabajo
- `clusteConection.py`: Conecta a Weaviate, crea la colección `Viaje` con vectorizador Ollama y cierra la conexión.
- `main.py`: Procesa el PDF, sube los datos a Weaviate, realiza consultas usando Ollama y cierra la conexión.

## Notas
- Modifica el prompt en `main.py` para hacer diferentes preguntas sobre los datos.
- Siempre cierra la conexión con `client.close()` para evitar advertencias.
- Puedes cambiar el modelo en la configuración del vectorizador si lo necesitas.

---


¿Dudas o necesitas adaptar el flujo? ¡Pide ayuda aquí!
