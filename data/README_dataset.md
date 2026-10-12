# Dataset de comentarios fitness (sintético)

## Origen
Los 150 comentarios se redactaron de forma sintética para este ejercicio. No proceden de personas reales, redes sociales, pacientes ni historiales médicos. No contienen datos personales. El dataset es un conjunto didáctico y **no demuestra generalización a conversaciones reales**.

## Campos
- `id`: identificador sintético único.
- `comentario`: texto en español.
- `etiqueta`: clase de referencia creada por el autor del dataset.
- `origen`: siempre `sintetico`, para evitar confundirlos con datos observados.
- `split_sugerido`: valor descriptivo; el notebook hace una partición estratificada reproducible.

## Etiquetas
- `molestia_mencionada`: el comentario menciona dolor o incomodidad, sin atribuir causa ni diagnóstico.
- `recuperacion_descanso`: descanso, recuperación o regreso gradual.
- `fatiga_esfuerzo`: cansancio o esfuerzo percibido.
- `bienestar_general`: experiencia positiva o cómoda.
- `consulta_profesional`: intención de buscar orientación profesional.

## Uso y limitaciones
El conjunto está balanceado (30 ejemplos por clase) y sirve para verificar el flujo de evaluación. Al ser sintético, puede favorecer patrones lingüísticos artificiales. Para un uso real, reemplazar o complementar con datos públicos/licenciados, revisar manualmente etiquetas y documentar consentimiento y privacidad. No usar el clasificador para diagnóstico, ni recomendaciones médicas.
