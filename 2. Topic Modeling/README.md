# Topic Modeling

Esta carpeta contiene las actividades relacionadas con la construcción, validación y aplicación de un esquema de tópicos para el análisis de discursos presidenciales utilizando modelos de lenguaje de gran escala (LLMs).

El trabajo se desarrollará de forma incremental mediante etapas sucesivas. Cada etapa tendrá una tarea específica, un documento metodológico asociado y unos entregables esperados.

---

# Objetivo general

Construir una metodología reproducible para:

1. Identificar los principales tópicos presentes en el corpus de discursos presidenciales.
2. Construir una taxonomía temática global.
3. Validar los tópicos obtenidos.
4. Determinar la presencia o ausencia de dichos tópicos en cada discurso.
5. Analizar la evolución temporal y discursiva de los temas identificados.

La metodología propuesta se inspira en trabajos recientes sobre:

- Prompt-based Topic Modeling.
- TopicGPT.
- Análisis temático asistido por LLMs.
- Construcción de codebooks para análisis cualitativo.

---

# Etapas del proyecto

## Etapa 1 — Extracción de tópicos

**Asignada:** Viernes 22

### Objetivo

Identificar los tópicos globales presentes en el conjunto completo de discursos.

A diferencia de enfoques tradicionales donde los tópicos se extraen individualmente por documento, en este proyecto se propone realizar una inducción temática a nivel de corpus.

### Documento asociado

`Topic_Extraction_Methodology.md`

### Actividades

- Preparar el corpus.
- Definir la estrategia de prompting.
- Extraer tópicos globales.
- Consolidar tópicos similares.
- Construir una taxonomía temática inicial.
- Construir un primer codebook.

### Entregables

- Lista de tópicos globales.
- Descripción de cada tópico.
- Evidencia textual representativa.
- Primera versión del codebook.

---

## Etapa 2 — Codificación temática de discursos

**Asignada:** Viernes 29

### Objetivo

Determinar cuáles de los tópicos globales aparecen en cada discurso individual.

El objetivo es construir una matriz discurso-tópico que permita analizar posteriormente:

- frecuencia temática,
- evolución temporal,
- coocurrencias,
- prioridades discursivas.

### Documento asociado

`Topic_Coding_Methods.md`

### Estrategias propuestas

#### 1. Hard Prompting

Determinar si un tópico aparece o no aparece en un discurso.

Resultado esperado:

- matriz binaria discurso-tópico.

---

#### 2. Soft Prompting

Determinar qué tan presente está un tópico en un discurso utilizando una escala ordinal.

Resultado esperado:

- matriz de intensidad temática.

---

#### 3. Embeddings

Representar semánticamente:

- tópicos,
- párrafos,
- discursos.

Y calcular similitud entre ambos espacios.

Resultado esperado:

- matriz de similitud temática.

---

#### 4. Estrategia híbrida

Combinar:

- razonamiento del LLM,
- resúmenes temáticos,
- validación mediante embeddings.

Resultado esperado:

- asignaciones temáticas con soporte semántico adicional.

---

### Entregables

- Implementación de las estrategias propuestas.
- Matrices discurso-tópico.
- Comparación entre métodos.
- Análisis de concordancia.
- Recomendación del método final para el trabajo.

---

# Próximas etapas

Las siguientes etapas serán definidas conforme avance el proyecto, pero probablemente incluirán:

## Etapa 3

Análisis temporal de tópicos.

## Etapa 4

Análisis de coocurrencia temática.

## Etapa 5

Visualización y análisis discursivo.

## Etapa 6

Redacción y consolidación de resultados.

---

# Recomendaciones

Durante todas las etapas se recomienda:

- documentar prompts,
- almacenar resultados intermedios,
- registrar cambios en el codebook,
- mantener trazabilidad experimental,
- documentar decisiones metodológicas.

Todo resultado debe poder reproducirse posteriormente a partir del corpus, los prompts y la configuración experimental utilizada.
