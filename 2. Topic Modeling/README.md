# Metodología para Extracción de Tópicos con LLMs

## 1. Construcción del corpus

El estudio parte de la construcción de un corpus compuesto por discursos del presidente de Colombia.

Cada documento debe organizarse en una estructura tabular con metadatos asociados.

| id | fecha | evento | tipo_discurso | texto |
|---|---|---|---|---|

Ejemplo:

| id | fecha | evento | tipo_discurso |
|---|---|---|---|
| D001 | 2024-07-20 | Instalación del Congreso | Institucional |
| D002 | 2024-11-15 | COP16 | Internacional |
| D003 | 2025-01-10 | Crisis energética | Coyuntural |

Los metadatos permitirán posteriormente analizar:
- evolución temática,
- cambios discursivos,
- tópicos dominantes por contexto político,
- variaciones temporales.

---

## 2. Preparación de los datos

El corpus debe someterse a un proceso de preparación básica.

Se recomienda:
- eliminar encabezados repetidos,
- corregir errores OCR evidentes,
- normalizar caracteres especiales,
- separar discursos excesivamente largos en fragmentos coherentes,
- conservar puntuación y estructura lingüística.

No se recomienda:
- eliminar stopwords,
- aplicar stemming,
- eliminar contexto sintáctico.

A diferencia de modelos probabilísticos tradicionales, los LLMs utilizan la estructura semántica completa del texto.

---

## 3. Inducción global de tópicos

En lugar de extraer tópicos individualmente por discurso, se propone una estrategia de inducción temática a nivel de corpus.

El corpus completo —o subconjuntos representativos cuando existan limitaciones de longitud— es entregado al modelo de lenguaje para identificar:
- temas recurrentes,
- patrones semánticos,
- categorías temáticas globales,
- relaciones conceptuales entre discursos.

Este enfoque sigue metodologías recientes de:
- prompt-based topic modeling,
- LLM-assisted thematic analysis,
- semantic topic induction.

### Prompt sugerido

> Analice el siguiente conjunto de discursos presidenciales e identifique los principales tópicos recurrentes del corpus. Para cada tópico entregue:
>
> - nombre del tópico,
> - descripción,
> - palabras clave,
> - ejemplos representativos,
> - diferenciación frente a otros tópicos.
>
> Genere únicamente tópicos sustentados recurrentemente en múltiples discursos.

---

## 4. Generación de la taxonomía temática

El modelo debe producir una primera taxonomía temática global.

Ejemplo:

```json
{
  "topics": [
    {
      "topic_name": "Transición energética",
      "description": "Discusión sobre reducción de dependencia fósil y energías renovables.",
      "keywords": ["energía", "transición", "petróleo", "renovables"],
      "example_fragments": ["..."],
      "distinction": "Relacionado con política ambiental, pero enfocado específicamente en energía."
    }
  ]
}
```

# 5. Construcción del codebook temático

A partir de la taxonomía temática generada por el LLM, el investigador debe construir un codebook temático formal que permita estandarizar la codificación de los discursos.

El codebook debe contener:

| código | tópico | definición | criterios de inclusión | criterios de exclusión | ejemplo |
|---|---|---|---|---|---|

Ejemplo:

| código | tópico | definición |
|---|---|---|
| T01 | Transición energética | Discusiones relacionadas con energías renovables, reducción de combustibles fósiles y política energética sostenible. |
| T02 | Reforma agraria | Referencias a redistribución de tierras, campesinado y políticas rurales. |

Los criterios de inclusión y exclusión deben ayudar a reducir ambigüedad entre categorías similares.

Esta etapa permite:
- mejorar la reproducibilidad,
- controlar la interpretación temática,
- consolidar categorías semánticamente coherentes,
- facilitar la validación humana.

---

# 6. Codificación temática de los discursos

Una vez construido el codebook, cada discurso debe analizarse individualmente.

En esta etapa, el objetivo ya no es descubrir nuevos tópicos, sino identificar cuáles de los tópicos globales definidos previamente aparecen en cada documento.

## Prompt sugerido

> Usando exclusivamente el siguiente codebook temático, indique qué tópicos aparecen en el discurso y cite evidencia textual para cada asignación. No genere nuevos tópicos.

---

## Ejemplo de salida esperada

```json
{
  "document_id": "D014",
  "topics_detected": [
    {
      "topic_code": "T01",
      "topic_name": "Transición energética",
      "evidence": "Debemos abandonar progresivamente la dependencia del petróleo..."
    },
    {
      "topic_code": "T03",
      "topic_name": "Justicia social",
      "evidence": "La desigualdad sigue siendo uno de los mayores problemas del país..."
    }
  ]
}
```

# 7. Validación humana

Los resultados producidos por el modelo deben revisarse manualmente.

El investigador debe:
- verificar que exista evidencia textual suficiente,
- eliminar asignaciones incorrectas,
- corregir errores semánticos,
- revisar tópicos ambiguos,
- consolidar categorías redundantes.

Siguiendo la literatura reciente sobre análisis cualitativo asistido por LLMs, el modelo debe entenderse como una herramienta de apoyo al investigador y no como un reemplazo del criterio humano.

La validación humana es especialmente importante debido a:
- posibles alucinaciones,
- sobre-generalización temática,
- sensibilidad al prompt,
- inconsistencias semánticas.

---

# 8. Construcción de matrices de análisis temático

Una vez realizada la codificación temática de todos los discursos, se deben construir matrices estructuradas que permitan analizar la distribución y comportamiento de los tópicos dentro del corpus.

Estas matrices transforman la información cualitativa en una representación organizada para análisis posteriores.

---

## 8.1 Matriz discurso-tópico

La principal estructura corresponde a una matriz binaria o ponderada donde:

- las filas representan discursos,
- las columnas representan tópicos globales,
- cada celda indica presencia, frecuencia o intensidad del tópico en el discurso.

Ejemplo:

| discurso | T01 | T02 | T03 | T04 |
|---|---|---|---|---|
| D001 | 1 | 0 | 1 | 0 |
| D002 | 1 | 1 | 0 | 0 |
| D003 | 0 | 1 | 1 | 1 |

Donde:
- `1` indica presencia del tópico,
- `0` indica ausencia.

Opcionalmente, la matriz puede contener:
- frecuencia de menciones,
- nivel de relevancia,
- score asignado por el LLM,
- validación humana.

---

## Referencias

Referencias principales:

- Pham et al., TopicGPT: A Prompt-based Topic Modeling Framework.
- Phan et al., Prompting Large Language Models for Topic Modeling.
- Tai et al., An Examination of the Use of Large Language Models to Aid Analysis of Textual Data.
