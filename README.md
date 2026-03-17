# Asistente Académico Automatizado (Arquitectura RAG)

Este proyecto es una solución de hiperautomatización diseñada para resolver consultas académicas y logísticas de estudiantes en tiempo real, utilizando Inteligencia Artificial sin riesgo de alucinaciones.

## Tecnologías Utilizadas
* **Orquestación:** n8n
* **LLM (Razonamiento):** Llama 3 (vía Groq API para latencia ultrabaja)
* **Embeddings:** Google Gemini
* **Base de Datos Vectorial:** Pinecone
* **Interfaz de Usuario:** Telegram Bot API

## Descripción del Problema
La gestión de consultas repetitivas sobre aspectos logísticos (fechas de evaluaciones, ponderaciones, etc.) consume un tiempo valioso del cuerpo docente, generando cuellos de botella en la comunicación durante los días sin clases presenciales. 

## La Solución
Se implementó un chatbot con **Arquitectura RAG (Retrieval-Augmented Generation)**. El flujo ingesta el sílabo oficial del curso, lo vectoriza y lo almacena. Cuando un alumno consulta vía Telegram, un agente de IA deduce la intención, busca la información exacta en la base vectorial y responde formulando un mensaje claro, negándose a inventar datos si la información no existe en el documento oficial.

## Arquitectura del Flujo (n8n)
El archivo `Proyecto Final_Cristian_Monsalve.json` contiene el pipeline completo, dividido en dos fases lógicas:
1. **Pipeline ETL Vectorial:** Carga de datos, Text Splitter (Chunking) y almacenamiento (Insert) en Pinecone.
2. **Agente de Recuperación:** Webhook de Telegram, memoria de ventana a corto plazo (Session ID dinámico para concurrencia), y herramientas de búsqueda semántica.

## Cómo usar este repositorio
1. Descarga el archivo `Proyecto Final_Cristian_Monsalve.json`.
2. En tu instancia de [n8n](https://n8n.io/), ve a `Workflows` -> `Import from File` y selecciona el archivo.
3. Configura tus propias credenciales (Groq, Pinecone, Google Gemini y Telegram) en los nodos correspondientes.
