# FitText: Clasificación de comentarios sobre molestias y recuperación en fitness mediante PLN

## 1. Descripción del proyecto

**Nombre del proyecto:** FitText.

**Área de inteligencia artificial:** Procesamiento del Lenguaje Natural (PLN).

**Caso de uso:** clasificación automática de comentarios relacionados con actividad física, molestias mencionadas, fatiga, recuperación, bienestar general y búsqueda de orientación profesional.

### Objetivo general

Evaluar y comparar tres modelos preentrenados de Hugging Face mediante clasificación *zero-shot*, con el propósito de identificar la categoría temática de comentarios relacionados con fitness y analizar el equilibrio entre desempeño, latencia y recursos computacionales.

### Contexto

FitText es un prototipo académico desarrollado con Python, Hugging Face Transformers y Google Colab. Utiliza modelos multilingües preentrenados para clasificar comentarios en español sin realizar entrenamiento adicional.

El sistema tiene fines educativos y experimentales. No realiza diagnósticos médicos, no determina la gravedad de lesiones ni proporciona tratamientos o recomendaciones clínicas.

## 2. Enfoque de inteligencia artificial

- **Tipo de aprendizaje:** transferencia de aprendizaje (*Transfer Learning*).
- **Tarea:** clasificación de texto mediante *zero-shot classification*.
- **Dominio:** Procesamiento del Lenguaje Natural.
- **Arquitectura:** modelos multilingües de inferencia textual (NLI).
- **Entrenamiento adicional:** no se realiza *fine-tuning*.
- **Entorno de prototipado:** Google Colab, preferentemente con GPU NVIDIA T4 cuando esté disponible.

Se utiliza clasificación *zero-shot* para comparar modelos preentrenados sin entrenarlos específicamente con el dataset del proyecto.

## 3. Tecnologías utilizadas

### Lenguaje y entorno

- Python 3.10 o superior, sujeto a compatibilidad con las dependencias instaladas.
- Google Colab.
- GPU NVIDIA T4, si está disponible.

### Librerías principales

- Pandas.
- NumPy.
- Transformers.
- PyTorch.
- Scikit-learn.
- Hugging Face Hub.
- Accelerate.

Las versiones efectivamente utilizadas deben registrarse durante la ejecución del notebook.

## 4. Modelos evaluados

Se comparan los siguientes modelos de clasificación multilingüe *zero-shot*:

1. `MoritzLaurer/mDeBERTa-v3-base-mnli-xnli`
2. `joeddav/xlm-roberta-large-xnli`
3. `MoritzLaurer/DeBERTa-v3-base-mnli-fever-anli`

Los modelos se evalúan utilizando los mismos comentarios, categorías y parámetros de inferencia.

La disponibilidad, la licencia declarada, la revisión del modelo y los requisitos computacionales deben verificarse en sus respectivas tarjetas de Hugging Face antes de utilizar los modelos fuera del contexto académico.

## 5. Categorías de clasificación

Cada comentario se asigna a una de las siguientes cinco categorías:

- `molestia_mencionada`: menciones de dolor o incomodidad durante o después de la actividad física.
- `recuperacion_descanso`: comentarios sobre descanso, recuperación o regreso gradual al ejercicio.
- `fatiga_esfuerzo`: expresiones de cansancio, agotamiento o fatiga asociada al esfuerzo.
- `bienestar_general`: comentarios sobre experiencias cómodas o sensaciones positivas durante la actividad física.
- `consulta_profesional`: intención de buscar orientación de un profesional sanitario.

Estas etiquetas describen el contenido del texto y no constituyen evaluaciones médicas.

## 6. Dataset utilizado

**Archivo:** `data/dataset_fitness_sintetico.csv`

El conjunto contiene 150 comentarios sintéticos en español, distribuidos equitativamente entre las cinco categorías, con 30 ejemplos por categoría.

### Estructura del dataset

| Campo | Descripción |
|---|---|
| `id` | Identificador sintético del registro. |
| `comentario` | Texto que será clasificado. |
| `etiqueta` | Categoría de referencia asignada al comentario. |
| `origen` | Procedencia del registro; en este proyecto, `sintetico`. |
| `split_sugerido` | Campo descriptivo del conjunto de datos. |

Los comentarios se redactaron con fines académicos y no proceden de usuarios reales, redes sociales ni expedientes médicos. Las etiquetas corresponden a las categorías definidas para el ejercicio.

La partición estratificada de evaluación se genera mediante `train_test_split`, con `test_size=0.30` y `random_state=42`. Dado que no se realiza entrenamiento, el conjunto de entrenamiento no se utiliza para ajustar los modelos.

Para evaluar el desempeño en un contexto real sería necesario incorporar datos representativos, verificar su procedencia y licencia, revisar las etiquetas y documentar las medidas de privacidad pertinentes.

## 7. Estructura del proyecto

```text
FitText/
├── README.md
├── requirements.txt
├── data/
│   ├── dataset_fitness_sintetico.csv
│   └── README_dataset.md
├── notebooks/
│   └── fittext_comparacion_modelos.ipynb
├── src/
│   └── evaluacion_modelos.py
├── results/
│   ├── README.md
│   └── metricas_modelos_plantilla.csv
└── docs/
    └── informe_comparativo_fittext.docx
```

Los archivos de métricas definitivas, predicciones y reportes de clasificación se generan al ejecutar el notebook o el script de evaluación.

## 8. Instrucciones de ejecución


1. Abrir Google Colab: https://colab.research.google.com/
2. Cargar `notebooks/fittext_comparacion_modelos.ipynb`.
3. En el menú **Entorno de ejecución → Cambiar tipo de entorno de ejecución**, seleccionar GPU si está disponible.
4. Subir el dataset y configurar su ruta de acceso.
5. Ejecutar las celdas secuencialmente.
6. Esperar a que se descarguen los modelos y finalice la inferencia.
7. Revisar y guardar los archivos generados en `results/`.

La autenticación en Hugging Face Hub es opcional para modelos públicos cuando el acceso anónimo está disponible. Si se necesita un token, debe almacenarse de forma segura y nunca publicarse en el repositorio.


## 9. Métricas de evaluación

Se utilizan las siguientes métricas:

- **Accuracy:** proporción total de predicciones correctas.
- **Precision macro:** promedio de la precisión calculada por categoría.
- **Recall macro:** promedio de la sensibilidad calculada por categoría.
- **F1 macro:** promedio de la media armónica entre precisión y recall por categoría.
- **Latencia total:** tiempo medido para realizar la inferencia sobre el conjunto de evaluación.
- **Latencia media:** tiempo de inferencia dividido entre el número de comentarios evaluados.

El promedio macro permite analizar el rendimiento de las distintas clases con el mismo peso, incluso si en futuras versiones el dataset deja de estar balanceado.

## 10. Resultados y comparación

10. Resultados y comparación

Los resultados experimentales se obtuvieron al ejecutar el pipeline de evaluación en GPU (NVIDIA T4) sobre el conjunto de prueba de 45 textos.

Métricas globales de rendimiento y latencia

Modelo: joeddav/xlm-roberta-large-xnli
Accuracy: 0.6222
Precision Macro: 0.6294
Recall Macro: 0.6222
F1 Macro: 0.6070
Latencia media: 0.0432 segundos por texto
Dispositivo: GPU

Modelo: MoritzLaurer/mDeBERTa-v3-base-mnli-xnli
Accuracy: 0.6222
Precision Macro: 0.6196
Recall Macro: 0.6222
F1 Macro: 0.5894
Latencia media: 0.0181 segundos por texto
Dispositivo: GPU

Modelo: MoritzLaurer/DeBERTa-v3-base-mnli-fever-anli
Accuracy: 0.3556
Precision Macro: 0.4688
Recall Macro: 0.3556
F1 Macro: 0.3234
Latencia media: 0.0188 segundos por texto
Dispositivo: GPU

Archivos generados:

- results/metricas_modelos.csv
- results/predicciones_modelos.csv
- results/classification_reports.txt

Análisis detallado

Rendimiento predictivo: joeddav/xlm-roberta-large-xnli obtuvo el mejor F1 macro general, con un valor de 0.6070, aunque presentó un coste computacional y una latencia mayores, de 0.0432 segundos por texto.

Eficiencia: MoritzLaurer/mDeBERTa-v3-base-mnli-xnli ofreció un equilibrio competitivo entre rendimiento y velocidad, con una latencia media de 0.0181 segundos por texto.

Errores por categoría: Se identificaron dificultades importantes en la clase fatiga_esfuerzo, que obtuvo un F1 de 0.00 en dos de los modelos y de aproximadamente 0.31 en xlm-roberta-large-xnli. Estos resultados se relacionan con las confusiones entre fatiga_esfuerzo y molestia_mencionada.

En la categoría molestia_mencionada, mDeBERTa alcanzó un recall elevado de 0.89, pero una precisión baja de 0.35, lo que indica una cantidad considerable de falsos positivos.

Evaluación de criterios exploratorios

Ninguno de los modelos alcanzó el umbral ideal propuesto, que establece un F1 macro mayor o igual a 0.80 y un recall mayor o igual a 0.90 en las clases críticas.

La comparación integra el rendimiento predictivo, la latencia, los recursos computacionales y el análisis de errores por categoría.


### Criterios propuestos para recomendar un modelo

Como umbrales exploratorios del proyecto, se propone considerar:

- F1 macro igual o superior a 0.80.
- Recall igual o superior a 0.90 en `molestia_mencionada` y `consulta_profesional`.
- Latencia compatible con el entorno de aplicación.
- Licencia verificada y requisitos de recursos aceptables.
- Revisión de los errores de clasificación más importantes.

Estos umbrales son criterios académicos y no estándares clínicos. Deben validarse con datos representativos y revisión humana antes de plantear cualquier uso real.

## 11. Reproducibilidad

Partición estratificada con semilla random_state=42.

Ejecución en entorno controlado de Google Colab utilizando GPU NVIDIA T4.

Archivos exportados en results/ (metricas_modelos.csv, predicciones_modelos.csv y classification_reports.txt).

## 12. Limitaciones y riesgos

Dataset sintético y acotado (150 registros totales, 45 de evaluación).

Ambigüedad semántica entre fatiga_esfuerzo y molestia_mencionada.

Sensibilidad de la clasificación zero-shot a la formulación de las plantillas de hipótesis.

No apto para diagnóstico clínico, triaje médico ni toma de decisiones sobre salud.

## 13. Conclusiones

joeddav/xlm-roberta-large-xnli obtuvo el mejor desempeño predictivo general con un F1 macro de 0.6070, mientras que MoritzLaurer/mDeBERTa-v3-base-mnli-xnli demostró mayor eficiencia temporal con una latencia media de 0.0181 s por texto.

En resumen, estos resultados nos sirven como una excelente prueba de concepto y nos dan claridad sobre qué camino tomar en las siguientes pruebas. Sin embargo, aún no respaldan un despliegue en producción sin antes ampliar el dataset con comentarios reales, corregir las confusiones por clase y validar formalmente las licencias de uso.

## 14. Referencias

- Hugging Face Transformers: https://huggingface.co/docs/transformers/
- Hugging Face Hub y tarjetas de modelos: https://huggingface.co/docs/hub/model-cards
- Scikit-learn, métricas de evaluación: https://scikit-learn.org/stable/modules/model_evaluation.html
- Tarjetas de los tres modelos especificados en la sección 4, consultadas en Hugging Face Hub.
