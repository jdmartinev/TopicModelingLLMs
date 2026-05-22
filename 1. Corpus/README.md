# Corpus

Esta carpeta contiene todos los recursos asociados al corpus de discursos utilizados en el trabajo de investigación.

El objetivo es centralizar:
- los discursos originales,
- las versiones procesadas,
- los metadatos,
- las fuentes de extracción,
- y la documentación asociada al proceso de construcción del corpus.

---

# Objetivo del corpus

El corpus corresponde al conjunto de discursos presidenciales que serán utilizados para realizar:
- inducción temática,
- extracción de tópicos,
- análisis discursivo,
- codificación temática asistida por LLMs.

La calidad y trazabilidad del corpus es fundamental para garantizar:
- reproducibilidad,
- consistencia metodológica,
- y validez del análisis temático.

---

# Estructura sugerida

## raw/

Debe contener los documentos originales extraídos desde las fuentes oficiales.

Ejemplos:
- páginas web oficiales,
- PDFs,
- transcripciones,
- comunicados,
- discursos institucionales.

Estos archivos NO deben modificarse.

---

## processed/

Contendrá versiones preparadas del corpus:
- textos limpios,
- correcciones OCR,
- normalización básica,
- segmentación de discursos largos.

Estas versiones serán utilizadas posteriormente por los modelos de lenguaje.

---

## metadata/

Debe contener archivos tabulares con información asociada a cada discurso.

Ejemplo:

| id | fecha | evento | tipo_discurso | fuente | archivo |
|---|---|---|---|---|---|

Metadatos sugeridos:
- identificador único,
- fecha,
- evento,
- tipo de discurso,
- URL o fuente original,
- nombre del archivo,
- observaciones relevantes.

---

## extraction/

Debe contener:
- scripts de scraping,
- notebooks de extracción,
- procesos automáticos de descarga,
- herramientas utilizadas para construir el corpus.

Esto permitirá reproducir posteriormente el proceso de construcción de datos.

---

# Descripción del proceso de construcción del corpus

El proceso de construcción del corpus debe documentarse cuidadosamente.

## 1. Identificación de fuentes

Se deben identificar las fuentes oficiales donde se encuentran publicados los discursos presidenciales.

Ejemplos:
- Presidencia de la República,
- medios oficiales,
- transcripciones institucionales,
- archivos públicos.

---

## 2. Extracción de discursos

Los discursos deben descargarse y almacenarse inicialmente en la carpeta `raw/`.

Durante esta etapa se recomienda:
- conservar el formato original,
- registrar la fuente,
- registrar la fecha de extracción,
- evitar modificaciones manuales.

---

## 3. Preparación de textos

Posteriormente se realiza:
- limpieza básica,
- eliminación de encabezados repetidos,
- corrección OCR,
- normalización de caracteres,
- segmentación de documentos extensos.

No se recomienda realizar:
- stemming,
- eliminación agresiva de stopwords,
- simplificación semántica.

El objetivo es conservar la estructura lingüística completa para el análisis con LLMs.

---

## 4. Consolidación de metadatos

Cada discurso debe tener información asociada que permita:
- análisis temporal,
- análisis contextual,
- trazabilidad,
- agrupación posterior.

---

# Recomendaciones importantes

- Nunca sobrescribir archivos originales.
- Mantener versiones procesadas separadas.
- Registrar cualquier modificación importante.
- Mantener consistencia en nombres de archivos.
- Conservar trazabilidad completa entre:
  - discurso original,
  - discurso procesado,
  - metadatos,
  - resultados experimentales.

---

# Resultado esperado

El resultado final debe ser un corpus:
- limpio,
- estructurado,
- reproducible,
- trazable,
- y listo para análisis temático asistido por modelos de lenguaje.