# 📝 Quiz App

Aplicación web completamente cliente‑side para crear y realizar exámenes personalizados importando tus propias preguntas en formato JSON. No requiere instalación ni servidor.

## ✨ Características

- **Importación flexible**: Carga conjuntos de preguntas desde archivos `.json` o pega el JSON directamente.
- **Múltiples conjuntos**: Puedes tener varios conjuntos guardados y elegir cuál usar en cada examen.
- **Modos de examen**: Realiza el examen con todas las preguntas o solo las falladas de ese conjunto.
- **Orden aleatorio o secuencial**: Las preguntas se pueden mostrar desordenadas o en el orden original.
- **Navegación libre**: Salta entre preguntas sin necesidad de comprobar la actual. El progreso se guarda.
- **Mapa de preguntas visual**: Muestra el estado de cada pregunta (correcta, incorrecta, seleccionada, sin contestar) y permite ir directamente a ella.
- **Soporte para respuesta única y múltiple**: La app detecta automáticamente si una pregunta requiere varias respuestas (basándose en el formato de `correct_answer`).
- **Comprobación manual**: Selecciona tus respuestas y pulsa **Comprobar** para ver si son correctas y recibir explicaciones.
- **Explicaciones**: Campo opcional `explanation` que se muestra al comprobar la pregunta, ideal para aprender.
- **Estadísticas e historial**: Resumen global (conjuntos, preguntas, falladas, nota media) y registro de cada examen realizado con puntuación.
- **Gestión de preguntas falladas**: Lista acumulada con contador de veces falladas. Puedes exportarlas a TXT o JSON, o eliminar individuales/todas.
- **Persistencia local**: Todos los datos (conjuntos, falladas, historial, tema) se guardan automáticamente en el `localStorage` del navegador. No se pierden al recargar la página.
- **Tema claro / oscuro**: Alterna entre modos visuales y se recuerda entre sesiones.

## 📄 Formato del JSON

El archivo debe contener un **array de objetos**, donde cada objeto representa una pregunta.

### Campos requeridos

| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id` | número | Identificador único dentro del conjunto. |
| `question` | string | Texto de la pregunta. |
| `options` | array de strings | Lista de respuestas posibles (mínimo 2). |
| `correct_answer` | string | Especifica la(s) respuesta(s) correcta(s) – ver formatos más abajo. |

### Campo opcional

| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `explanation` | string | Explicación teórica que se muestra al comprobar la pregunta. |

### Formatos de `correct_answer`

| Tipo | Ejemplo | Comportamiento |
| :--- | :--- | :--- |
| **Texto exacto** | `"Guepardo"` | Coincide exactamente con una de las opciones. Respuesta única. |
| **Letra individual** | `"A"` | La letra mayúscula corresponde al índice de la opción (A=primera, B=segunda…). |
| **Múltiples letras** | `"A, C"` o `"A and C"` | Varias letras separadas por comas, espacios o la palabra "and". Activa el modo multirrespuesta. El usuario debe marcar todas las opciones indicadas. |

> [!NOTE]
> La aplicación detecta automáticamente si es multirrespuesta cuando `correct_answer` contiene una coma, un punto y coma, o múltiples letras mayúsculas separadas.

## 📋 Ejemplos

### Respuesta única (texto exacto)

```json
[
  {
    "id": 1,
    "question": "¿Cuál es el animal terrestre más rápido?",
    "options": ["León", "Guepardo", "Tigre", "Canguro"],
    "correct_answer": "Guepardo",
    "explanation": "El guepardo alcanza hasta 120 km/h en cortas distancias."
  }
]
```

### Respuesta única (letra)

```json
{
  "id": 2,
  "question": "¿En qué ciudad está la Torre Eiffel?",
  "options": ["Londres", "Roma", "París", "Madrid"],
  "correct_answer": "C"
}
```

### Multirrespuesta

```json
{
  "id": 3,
  "question": "¿Cuáles de los siguientes son lenguajes de programación? (marca 2)",
  "options": ["Python", "HTML", "Java", "CSS"],
  "correct_answer": "A, C",
  "explanation": "Python y Java son lenguajes de programación; HTML y CSS son de marcado."
}
```

## 🚀 Cómo usar la aplicación

1. **Importar un conjunto**: Arrastra un archivo `.json` a la zona de importación, o pega el JSON en el área de texto y pulsa **Importar JSON**. También puedes usar el botón **Cargar ejemplo**.
2. **Ir a la pestaña Examen**: Selecciona el conjunto que quieres practicar.
3. **Configurar el examen**: Elige si quieres todas las preguntas o solo las falladas, y el orden (aleatorio o secuencial).
4. **Realizar el examen**: Responde seleccionando una o varias opciones. Usa el botón **Comprobar** para validar tu respuesta y ver la explicación. Puedes navegar entre preguntas con los botones **Anterior/Siguiente** o haciendo clic en el mapa de preguntas.
5. **Finalizar**: Cuando termines, pulsa **Ver resultados** (o **Finalizar examen**). Se evaluarán automáticamente las preguntas no comprobadas y se mostrará tu puntuación. Los resultados se guardan en el historial.
6. **Revisar falladas**: En la pestaña **Falladas** encontrarás todas las preguntas que has respondido incorrectamente, con la respuesta correcta y tu respuesta errónea. Puedes exportarlas para repasarlas fuera de la app.
7. **Consultar estadísticas**: La pestaña **Stats** muestra el resumen global y el historial de exámenes realizados.

## 🗺️ Mapa de preguntas

Durante el examen aparece un panel con todos los números de pregunta. Los colores indican el estado:

- 🟢 **Verde**: Pregunta comprobada y correcta.
- 🔴 **Rojo**: Pregunta comprobada e incorrecta.
- 🟣 **Morado**: Tiene alguna opción seleccionada pero aún no comprobada.
- ⚪ **Gris**: Sin ninguna respuesta seleccionada.

Haz clic en cualquier número para ir directamente a esa pregunta.

## 🧹 Persistencia de datos

La aplicación guarda automáticamente en `localStorage`:

- Los conjuntos de preguntas importados.
- Las preguntas falladas (con su historial de veces falladas).
- El historial de exámenes.
- El tema elegido (claro/oscuro).

Puedes cerrar el navegador y volver más tarde; todos tus datos seguirán ahí.

## 📌 Notas adicionales

- **Nombres de conjuntos**: Al importar desde texto, la app asigna un nombre genérico (Conjunto 1, Conjunto 2…). Para cambiar el nombre, tendrías que eliminar el conjunto y volver a importar con el nombre deseado (si usas un archivo, el nombre del fichero se usa como nombre del conjunto).
- **Contador de fallos**: Las preguntas falladas acumulan un contador (`failCount`) que se incrementa cada vez que fallas esa pregunta. Puedes verlo en la lista de falladas.
- **Explicaciones**: Si una pregunta tiene `explanation`, se mostrará siempre tras comprobarla, con un estilo especial si la respuesta fue incorrecta.