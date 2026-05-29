# Tarea: Comparación de Discursos con Tópicos Globales

## Objetivo

Después de construir el conjunto de tópicos globales del corpus, se debe determinar si cada tópico aparece o no aparece en cada discurso individual.

El objetivo es construir una matriz discurso-tópico que permita analizar la presencia, intensidad y consistencia de los tópicos a lo largo del corpus presidencial.

---

# Entrada

Se debe contar con:

1. Un conjunto de discursos procesados.
2. Un codebook de tópicos globales.
3. Para cada tópico:
   - nombre,
   - descripción,
   - criterios de inclusión,
   - criterios de exclusión,
   - ejemplos representativos.

---

# Salida esperada

Una matriz discurso-tópico.

Ejemplo:

| discurso | T01 | T02 | T03 | T04 |
|---|---|---|---|---|
| D001 | 1 | 0 | 1 | 0 |
| D002 | 1 | 1 | 0 | 0 |
| D003 | 0 | 1 | 1 | 1 |

También se puede construir una matriz con intensidad:

| discurso | T01 | T02 | T03 |
|---|---|---|---|
| D001 | 4 | 0 | 2 |
| D002 | 5 | 3 | 0 |

Donde:

- `0`: no aparece
- `1`: aparece muy débilmente
- `2`: aparece de forma marginal
- `3`: aparece de forma moderada
- `4`: aparece de forma fuerte
- `5`: tópico central del discurso

---

# Estrategias propuestas

## 1. Hard Prompting

Consiste en pedir directamente al LLM que determine si un tópico aparece o no aparece en un discurso.

### Prompt sugerido

Analice el siguiente discurso y determine si el tópico aparece o no aparece.

Tópico:
[nombre del tópico]

Descripción:
[descripción del tópico]

Criterios de inclusión:
[criterios]

Criterios de exclusión:
[criterios]

Discurso:
[texto del discurso]

Responda en formato estructurado:

{
  "topic_code": "T01",
  "appears": true,
  "evidence": "...",
  "justification": "..."
}

## Ventaja

Produce una matriz binaria clara.

## Limitación

Puede ser demasiado rígido para tópicos que aparecen parcialmente o de forma indirecta.

---

## 2. Soft Prompting

Consiste en pedir al LLM que califique qué tanto aparece un tópico en un discurso usando una escala ordinal.

### Prompt sugerido

Analice el siguiente discurso y califique qué tanto aparece el tópico indicado.

Use la siguiente escala:

- 0: no aparece
- 1: aparece muy débilmente
- 2: aparece de forma marginal
- 3: aparece de forma moderada
- 4: aparece de forma fuerte
- 5: es un tópico central del discurso

Tópico:
[nombre del tópico]

Descripción:
[descripción del tópico]

Discurso:
[texto del discurso]

Responda en formato estructurado:

{
  "topic_code": "T01",
  "score": 0,
  "evidence": "...",
  "justification": "..."
}

## Ventaja

Permite medir intensidad temática.

## Limitación

La escala puede ser subjetiva y sensible al prompt.

---

## 3. Comparación mediante embeddings

Consiste en representar semánticamente tanto los tópicos como los discursos usando embeddings.

## Procedimiento

1. Generar una descripción robusta de cada tópico.
2. Calcular el embedding de cada tópico.
3. Dividir cada discurso en párrafos.
4. Calcular el embedding de cada párrafo.
5. Calcular la similitud coseno entre cada tópico y cada párrafo.
6. Para cada discurso y tópico, conservar la mayor similitud encontrada.
7. Definir un umbral para decidir presencia o ausencia del tópico.

## Fórmula general

similitud_tópico_discurso = max(similitud(tópico, párrafo_i))

## Salida esperada

| discurso | tópico | max_similarity | appears |
|---|---|---|---|
| D001 | T01 | 0.82 | 1 |
| D001 | T02 | 0.41 | 0 |

## Ventaja

Permite una medición semántica más sistemática y menos dependiente de una única respuesta generativa.

## Limitación

Requiere definir umbrales de similitud y validar manualmente casos ambiguos.

---

## 4. Combinación de soft prompting y embeddings

Esta estrategia combina razonamiento del LLM con validación semántica mediante embeddings.

## Procedimiento

1. Para cada discurso, pedir al LLM que indique qué aparece de cada tópico.
2. Si el tópico no aparece, debe responder explícitamente: "No aparece".
3. Si aparece, debe generar un resumen breve de cómo aparece el tópico en el discurso.
4. Calcular el embedding de la descripción global del tópico.
5. Calcular el embedding del resumen generado para ese tópico en el discurso.
6. Calcular la similitud entre ambos embeddings.
7. Usar la similitud como medida de consistencia semántica.

## Prompt sugerido

Usando el siguiente codebook, analice el discurso e indique cómo aparece cada tópico.

Si el tópico no aparece, escriba exactamente: "No aparece".

Para cada tópico que sí aparezca, escriba un resumen breve y específico de cómo se manifiesta en el discurso.

Responda en formato estructurado:

{
  "document_id": "D001",
  "topics": [
    {
      "topic_code": "T01",
      "status": "aparece",
      "summary": "..."
    },
    {
      "topic_code": "T02",
      "status": "no aparece",
      "summary": "No aparece"
    }
  ]
}

## Ventaja

Combina interpretación cualitativa con una medida cuantitativa de similitud semántica.

## Limitación

Depende de la calidad del resumen generado por el LLM.

---

# Comparación entre métodos

Se recomienda comparar los resultados de las cuatro estrategias.

## Métricas posibles

- acuerdo entre hard prompting y soft prompting;
- correlación entre soft score y similitud por embeddings;
- porcentaje de coincidencia entre métodos;
- revisión manual de casos en desacuerdo;
- análisis de falsos positivos y falsos negativos.

---

# Producto esperado

El estudiante debe entregar:

1. Matriz discurso-tópico binaria.
2. Matriz discurso-tópico con intensidad.
3. Matriz de similitud por embeddings.
4. Tabla comparativa entre métodos.
5. Análisis de desacuerdos.
6. Recomendación del método final para el trabajo.

---

# Recomendación metodológica

La estrategia más sólida probablemente sea usar:

1. Soft prompting como método principal.
2. Embeddings como validación semántica.
3. Validación humana en casos ambiguos.

Esto permite combinar:
- interpretación semántica,
- trazabilidad,
- cuantificación,
- y revisión humana.
