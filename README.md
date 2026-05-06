# 📝 Quiz App

Aplicación web completamente cliente‑side para crear y realizar exámenes personalizados importando tus propias preguntas en formato JSON.

## ✨ Características

- Importa conjuntos de preguntas desde archivos `.json` o pegando el texto directamente.
- Realiza exámenes con **todas las preguntas** o **solo las falladas**.
- Orden **aleatorio** o **secuencial**.
- Estadísticas por conjunto e historial de resultados.
- Almacena localmente las preguntas falladas y el historial.
- Exporta las preguntas falladas a TXT o JSON.
- Tema **claro u oscuro**.

## 📄 Formato del JSON

El archivo debe contener un **array de objetos**, cada objeto representa una pregunta.

### Campos requeridos

| Campo            | Tipo               | Descripción                                                                 |
|------------------|--------------------|-----------------------------------------------------------------------------|
| `id`             | número             | Identificador único (dentro del conjunto).                                  |
| `question`       | string             | Texto de la pregunta.                                                       |
| `options`        | array de strings   | Lista de respuestas posibles (mínimo 2).                                    |
| `correct_answer` | string             | Debe coincidir **exactamente** con una de las opciones.                     |

### Campo opcional

| Campo         | Tipo   | Descripción                                   |
|---------------|--------|-----------------------------------------------|
| `explanation` | string | Explicación teórica de la respuesta. |

### Ejemplo

```json
[
  {
    "id": 1,
    "question": "¿Cuál es el animal terrestre más rápido?",
    "options": ["León", "Guepardo", "Tigre", "Canguro"],
    "correct_answer": "Guepardo",
    "explanation": "El guepardo alcanza hasta 120 km/h en cortas distancias."
  },
  {
    "id": 2,
    "question": "¿En qué ciudad se encuentra la Torre Eiffel?",
    "options": ["Londres", "Roma", "París", "Madrid"],
    "correct_answer": "París"
  }
]
```

## 🧹 Persistencia
Toda la información (conjuntos, falladas, historial) se guarda automáticamente en el localStorage del navegador. No se pierde al recargar la página.

## 📌 Notas
Al importar, la aplicación genera un nombre automático (“Conjunto 1”, etc.) que puedes cambiar editando el conjunto.

Si usas el campo explanation, se mostrará siempre, pero con un estilo más destacado cuando falles la pregunta.