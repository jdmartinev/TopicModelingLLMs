# Metodología para Extracción de Tópicos con LLMs

## 1. Definición del corpus

Construir una base de discursos en formato tabular:

| id | fecha | evento | tipo_discurso | texto |
|---|---|---|---|---|

Ejemplo:

| id | fecha | evento | tipo_discurso |
|---|---|---|---|
| D001 | 2024-07-20 | Instalación del Congreso | Institucional |
| D002 | 2024-11-15 | COP16 | Internacional |
| D003 | 2025-01-10 | Crisis energética | Coyuntural |

Cada discurso debe incluir metadatos mínimos:
- fecha,
- evento,
- tipo de discurso,
- fuente,
- texto completo.

Estos metadatos permitirán posteriormente analizar:
- evolución temática,
- tópicos por contexto político,
- cambios discursivos temporales,
- diferencias entre tipos de intervención.

---

## 2. Preprocesamiento de los textos

No se recomienda realizar un preprocesamiento agresivo como en enfoques tradicionales tipo LDA.

Se recomienda únicamente:
- eliminar encabezados repetidos,
- corregir errores OCR evidentes,
- separar discursos extremadamente largos en fragmentos coherentes,
- conservar puntuación y estructura lingüística,
- evitar eliminar stopwords automáticamente.

Esto es importante porque los LLMs aprovechan el contexto semántico y sintáctico completo.

---

## 3. Diseño del prompt base

El prompt debe orientarse a extracción temática y no a resumen.

Ejemplo:

> Analiza el siguiente discurso e identifica los principales tópicos tratados. Para cada tópico entrega:
> - nombre breve,
> - descripción,
> - evidencia textual corta,
> - justificación semántica.
>
> No inventes información que no esté presente en el texto.

---

## 4. Extracción de tópicos por documento

Para cada discurso, el estudiante debe solicitar al LLM una salida estructurada.

Ejemplo:

```json
{
  "document_id": "...",
  "topics": [
    {
      "topic_label": "...",
      "description": "...",
      "evidence": "...",
      "confidence": "alta/media/baja"
    }
  ]
}
```

---

Este enfoque sigue metodologías recientes de prompt-based topic modeling, donde el LLM induce tópicos latentes directamente desde el texto.

## Referencias principales
- Phan et al. Prompting Large Language Models for Topic Modeling
- Zha et al. TopicGPT: A Prompt-based Topic Modeling Framework