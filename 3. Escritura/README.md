# Guía para escribir la sección metodológica y experimental

## Objetivo

El objetivo inicial del trabajo debe centrarse en construir y documentar correctamente el pipeline experimental para extracción de tópicos utilizando modelos de lenguaje de gran escala (LLMs) sobre discursos presidenciales.

Por ahora, el enfoque debe estar en:
- corpus,
- preparación de datos,
- inducción temática,
- construcción del codebook,
- codificación temática,
- análisis de resultados.

La discusión teórica y política puede fortalecerse posteriormente.

---

# 1. Introducción metodológica

La sección metodológica debe iniciar explicando el enfoque general del trabajo.

Debe dejar claro que:
- no se utiliza topic modeling probabilístico tradicional,
- el enfoque se basa en prompting con LLMs,
- se realiza inducción temática asistida por modelos de lenguaje,
- existe validación humana.

## Ejemplo de redacción

> Este trabajo propone una estrategia de análisis temático asistido por modelos de lenguaje de gran escala para identificar tópicos recurrentes en discursos presidenciales. A diferencia de enfoques tradicionales de topic modeling basados en distribuciones probabilísticas de palabras, la metodología empleada utiliza prompting sobre LLMs para inducir categorías temáticas semánticamente coherentes a nivel de corpus. Posteriormente, estas categorías son consolidadas mediante validación humana y utilizadas para codificar individualmente cada discurso.

---

# 2. Descripción del corpus

Debe explicarse:
- de dónde salen los discursos,
- cuántos discursos existen,
- periodo temporal,
- criterios de inclusión,
- estructura de almacenamiento.

## Qué incluir

- número de discursos,
- rango temporal,
- fuentes oficiales,
- tipo de discursos,
- metadatos disponibles.

## Ejemplo

| id | fecha | evento | tipo_discurso | texto |
|---|---|---|---|---|

---

# 3. Preparación de los datos

Debe describirse claramente el proceso de limpieza y organización.

## Explicar:

- eliminación de encabezados repetidos,
- corrección OCR,
- normalización básica,
- segmentación de documentos largos,
- conservación de puntuación y estructura lingüística.

## Muy importante

Debe justificarse por qué NO se aplicó:
- stemming,
- eliminación de stopwords,
- lematización agresiva.

## Ejemplo de redacción

> Debido a que los modelos de lenguaje modernos aprovechan relaciones semánticas y sintácticas completas, se evitó realizar preprocesamientos agresivos típicos de modelos probabilísticos tradicionales.

---

# 4. Estrategia de inducción temática

Aquí se explica la parte central del trabajo.

Debe aclararse que:
- los tópicos se extraen a nivel de corpus,
- no individualmente por documento,
- el modelo identifica patrones recurrentes globales.

## Explicar:

- uso de prompting,
- análisis global del corpus,
- construcción de taxonomía temática,
- extracción semántica de categorías.

## Ejemplo de prompt

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

# 5. Construcción del codebook

Debe explicarse:
- cómo se consolidaron los tópicos,
- cómo se eliminaron redundancias,
- cómo se definieron categorías finales.

## Incluir tabla

| código | tópico | definición | inclusión | exclusión |
|---|---|---|---|---|

## Explicar:

- refinamiento manual,
- consolidación semántica,
- revisión iterativa.

---

# 6. Codificación temática

Aquí se explica cómo se analiza cada discurso usando el codebook final.

## Explicar:

- asignación de tópicos,
- uso de evidencia textual,
- prohibición de crear nuevos tópicos,
- codificación controlada.

## Prompt sugerido

> Usando exclusivamente el siguiente codebook temático, indique qué tópicos aparecen en el discurso y cite evidencia textual para cada asignación.

---

# 7. Validación humana

Debe explicarse claramente que:
- el LLM no reemplaza al investigador,
- existe revisión manual,
- se corrigen errores semánticos,
- se validan asignaciones.

## Explicar revisión de:

- alucinaciones,
- tópicos ambiguos,
- sobreasignación,
- ausencia de evidencia textual.

---

# 8. Construcción de matrices temáticas

Describir la construcción de:

## Matriz discurso-tópico

| discurso | T01 | T02 | T03 |
|---|---|---|---|

## Matriz temporal

| año | tópico | frecuencia |
|---|---|---|

## Matriz de coocurrencia

| tópico | T01 | T02 |
|---|---|---|

---


# Referencias metodológicas principales

1. Phan et al. *Prompting Large Language Models for Topic Modeling*.

2. Zha et al. *TopicGPT: A Prompt-based Topic Modeling Framework*.

3. Tai et al. *An Examination of the Use of Large Language Models to Support Qualitative Research*.