# Reporte de Benchmark y Respuestas: LLMOps Lab 1

Este documento detalla las respuestas completas obtenidas por cada modelo cuantizado frente a los prompts de prueba, acompañadas de sus métricas de rendimiento.

---

## Prueba 1: qwen2.5:1.5b-instruct-q4_K_M

- **Categoría de Prompt:** Corto (Definición)
- **Métricas:** `TTFT: 1318.94 ms` | `Velocidad: 7.92 TPS` | `Tokens: 417` | `Tiempo Total: 53.98 s`

### Prompt Enviado:
> Explica en exactamente 3 viñetas qué es la cuantización en modelos de lenguaje.

### Respuesta Generada:
```text
La cuantización en modelos de lenguaje es un concepto fundamental en la representación de la información en redes de neuronas y, en particular, en los modelos de lenguaje como el Transformer. Aquí te explico en tres viñetas:

1. **Representación de la información**: La cuantización implica la transformación de la información original en un espacio de representación más reducido. En modelos de lenguaje, esto se refleja en la reducción de la cantidad de características o tokens que se utilizan para representar el texto. En lugar de manejar todos los posibles caracteres del alfabeto (como en el caso de modelos tradicionales), estos modelos utilizan una representación más simple, generalmente una secuencia de números enteros (tokens) que representan palabras o subsecuencias de palabras.

2. **Reducción de la complejidad**: La cuantización reduce la complejidad del modelo, lo que puede ser beneficioso en términos de rendimiento y eficiencia. En modelos de lenguaje, esto se traduce en una menor cantidad de parámetros y una menor cantidad de operaciones necesarias para realizar cálculos. Esto puede llevar a una mejora en la velocidad de entrenamiento y la capacidad de la red para procesar grandes cantidades de texto.

3. **Interpretación y comprensión**: La cuantización también tiene implicaciones para la interpretación y comprensión del modelo. Al trabajar con números enteros en lugar de caracteres, los modelos pueden ser más eficientes en términos de memoria y procesamiento. Además, la cuantización puede ayudar a reducir la confusión que puede surgir al trabajar con texto en su forma original, especialmente en modelos que deben procesar texto en varias lenguas o dialectos. Esto puede mejorar la precisión y la eficacia del modelo en tareas de traducción o comprensión de lenguaje natural.
```

---

## Prueba 2: qwen2.5:1.5b-instruct-q4_K_M

- **Categoría de Prompt:** Medio (Razonamiento)
- **Métricas:** `TTFT: 2781.1 ms` | `Velocidad: 7.58 TPS` | `Tokens: 434` | `Tiempo Total: 60.05 s`

### Prompt Enviado:
> Tengo un servidor con 16 GB de RAM y sin GPU. Quiero desplegar un asistente interno para 5 empleados. ¿Qué arquitectura y tamaño de modelo me recomiendas y por qué?

### Respuesta Generada:
```text
Para un asistente interno para 5 empleados en un servidor con 16 GB de RAM y sin GPU, la arquitectura y tamaño de modelo que recomendaría son:

1. **Modelo de Conversación Simple (Simple Conversational Model, SSM)**: Este modelo es ideal para aplicaciones de asistente interno donde la conversación es más simple y directa. Es más rápido y consume menos recursos que modelos más complejos.

2. **Tamaño de Modelo Medio (Medium-sized Model, MS)**: Este tamaño de modelo es adecuado para aplicaciones de asistente interno donde la conversación puede ser más compleja y requiere más recursos. 

3. **Tamaño de Modelo Medio Alto (Medium-sized Model, MS-A)**: Este tamaño de modelo es más grande y puede ser más adecuado para aplicaciones donde la conversación puede ser más compleja y requiere más recursos. 

4. **Tamaño de Modelo Grande (Large Model, LM)**: Este tamaño de modelo es el más grande y puede ser más adecuado para aplicaciones donde la conversación puede ser muy compleja y requiere mucho más recursos.

Por qué estas recomendaciones:

- **SSM**: Es más rápido y consume menos recursos, lo que es ideal para un servidor con 16 GB de RAM.
- **MS**: Es más rápido que SSM pero consume más recursos, lo que puede ser más adecuado para un servidor con 16 GB de RAM.
- **MS-A**: Es más grande que MS pero consume más recursos, lo que puede ser más adecuado para un servidor con 16 GB de RAM.
- **LM**: Es el tamaño de modelo más grande y consume más recursos, lo que puede ser más adecuado para un servidor con 16 GB de RAM.

Recuerda que la elección del tamaño de modelo y la arquitectura dependerá de la complejidad de la conversación que se pretende manejar y del rendimiento que se puede permitir en el servidor.
```

---

## Prueba 3: qwen2.5:1.5b-instruct-q4_K_M

- **Categoría de Prompt:** Largo (Generación de Código)
- **Métricas:** `TTFT: 2002.73 ms` | `Velocidad: 7.66 TPS` | `Tokens: 616` | `Tiempo Total: 82.47 s`

### Prompt Enviado:
> Escribe una función en Python bien documentada que implemente búsqueda binaria sobre una lista ordenada, incluyendo manejo de excepciones y 3 casos de prueba.

### Respuesta Generada:
```text
Aquí tienes una función en Python que implementa la búsqueda binaria sobre una lista ordenada. Esta función está bien documentada y incluye manejo de excepciones y tres casos de prueba:

```python
def binary_search(arr, target):
    """
    Realiza una búsqueda binaria en una lista ordenada para encontrar el índice del elemento 'target'.
    
    Parámetros:
    arr (list): Una lista ordenada de elementos.
    target: El elemento a buscar en la lista.
    
    Retorna:
    int: El índice del elemento 'target' en la lista, o -1 si no se encuentra.
    
    Excepciones:
    ValueError: Si la lista no está ordenada o si el elemento 'target' no está en la lista.
    """
    # Verificar si la lista está ordenada
    if not arr or arr != sorted(arr):
        raise ValueError("La lista no está ordenada o el elemento no está en la lista.")
    
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
            
    raise ValueError("El elemento no está en la lista.")
    
# Casos de prueba
try:
    lista = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    print(binary_search(lista, 5))  # Debería imprimir 4
    print(binary_search(lista, 11))  # Debería imprimir ValueError
except ValueError as e:
    print(e)
```

### Explicación:
- **Función**: `binary_search` recibe una lista `arr` ordenada y un `target` a buscar.
- **Verificación de ordenación**: La función primero verifica si la lista está ordenada y si el `target` está en la lista. Si no, lanza una excepción de tipo `ValueError`.
- **Búsqueda binaria**: Utiliza un algoritmo de búsqueda binaria para encontrar el índice del `target` en la lista. Si encuentra el `target`, devuelve su índice. Si no lo encuentra, devuelve `-1`.
- **Excepciones**: La función maneja la excepción `ValueError` en caso de que la lista no esté ordenada o si el `target` no está en la lista.
- **Casos de prueba**: Se incluyen dos casos de prueba: un éxito y un error. El éxito se verifica con un `target` que está en la lista, y el error se verifica con un `target` que no está en la lista.

Este código es práctico y bien documentado, lo que facilita su comprensión y uso en diferentes contextos.
```

---

## Prueba 4: qwen2.5:1.5b-instruct-q8_0

- **Categoría de Prompt:** Corto (Definición)
- **Métricas:** `TTFT: 2168.39 ms` | `Velocidad: 4.2 TPS` | `Tokens: 294` | `Tiempo Total: 72.21 s`

### Prompt Enviado:
> Explica en exactamente 3 viñetas qué es la cuantización en modelos de lenguaje.

### Respuesta Generada:
```text
1. **Definición y Concepto**: La cuantización en modelos de lenguaje es un proceso que reduce la cantidad de información original en un texto o frase a una representación más simple y compacta. En términos técnicos, se refiere a la transformación de un texto en un conjunto de números o representaciones numéricas que pueden ser procesadas y manipuladas por un sistema de inteligencia artificial.

2. **Aplicaciones y Beneficios**: Esta técnica es utilizada en diversos campos, incluyendo la traducción automática, el procesamiento de lenguaje natural y la generación de texto. Su principal beneficio es la reducción de la cantidad de recursos necesarios para la computación, lo que puede mejorar la eficiencia y la velocidad de procesamiento. Además, permite la representación de textos en un formato más amigable para el procesamiento por computadora.

3. **Efectos y Limitaciones**: La cuantización puede tener efectos tanto positivos como negativos. Por un lado, puede mejorar la eficiencia y la velocidad de procesamiento de los modelos de lenguaje. Por otro lado, puede resultar en una pérdida de información, lo que puede afectar la calidad del texto generado o traducido. Además, la precisión de la cuantización depende del método utilizado y puede ser difícil de controlar completamente.
```

---

## Prueba 5: qwen2.5:1.5b-instruct-q8_0

- **Categoría de Prompt:** Medio (Razonamiento)
- **Métricas:** `TTFT: 4936.52 ms` | `Velocidad: 4.25 TPS` | `Tokens: 674` | `Tiempo Total: 163.6 s`

### Prompt Enviado:
> Tengo un servidor con 16 GB de RAM y sin GPU. Quiero desplegar un asistente interno para 5 empleados. ¿Qué arquitectura y tamaño de modelo me recomiendas y por qué?

### Respuesta Generada:
```text
Para un asistente interno para 5 empleados con un servidor de 16 GB de RAM, aquí te recomendaría una arquitectura y tamaño de modelo:

1. Arquitectura:
   - Servidor de 16 GB de RAM: Es suficiente para manejar la carga de trabajo de un asistente interno.
   - CPU: Un procesador de 64-bit con al menos 2 núcleos y 4 threads sería adecuado. Por ejemplo, un Intel Core i7 o un AMD Ryzen 5.
   - Memoria RAM: 8 GB o más sería ideal para manejar la carga de trabajo de un asistente interno.

2. Tamaño de modelo:
   - Tamaño de modelo pequeño: Un modelo pequeño como Claude 100 o Claude 150 sería adecuado para un asistente interno. Estos modelos tienen una capacidad de procesamiento de texto de 100-150 palabras por segundo.
   - Tamaño de modelo mediano: Un modelo mediano como Claude 250 o Claude 300 sería un buen compromiso entre capacidad y rendimiento. Estos modelos tienen una capacidad de procesamiento de texto de 250-300 palabras por segundo.
   - Tamaño de modelo grande: Un modelo grande como Claude 500 o Claude 700 sería un buen opción para un asistente interno con más personalización y capacidad de procesamiento. Estos modelos tienen una capacidad de procesamiento de texto de 500-700 palabras por segundo.

Recomendaciones adicionales:

1. Utiliza un modelo de texto de texto para evitar problemas de rendimiento con la GPU.
2. Asegúrate de tener suficiente espacio de almacenamiento en el servidor para almacenar la información de los empleados y sus interacciones.
3. Considera la posibilidad de usar un modelo de texto de texto para evitar problemas de rendimiento con la GPU.
4. Asegúrate de tener suficiente espacio de almacenamiento en el servidor para almacenar la información de los empleados y sus interacciones.
5. Considera la posibilidad de usar un modelo de texto de texto para evitar problemas de rendimiento con la GPU.
6. Asegúrate de tener suficiente espacio de almacenamiento en el servidor para almacenar la información de los empleados y sus interacciones.
7. Considera la posibilidad de usar un modelo de texto de texto para evitar problemas de rendimiento con la GPU.
8. Asegúrate de tener suficiente espacio de almacenamiento en el servidor para almacenar la información de los empleados y sus interacciones.
9. Considera la posibilidad de usar un modelo de texto de texto para evitar problemas de rendimiento con la GPU.
10. Asegúrate de tener suficiente espacio de almacenamiento en el servidor para almacenar la información de los empleados y sus interacciones.

Recuerda que estos son solo recomendaciones generales. La elección del modelo y la arquitectura dependerá de tus necesidades específicas y el tipo de trabajo que se realizará con el asistente interno.
```

---

## Prueba 6: qwen2.5:1.5b-instruct-q8_0

- **Categoría de Prompt:** Largo (Generación de Código)
- **Métricas:** `TTFT: 3147.77 ms` | `Velocidad: 4.47 TPS` | `Tokens: 691` | `Tiempo Total: 157.83 s`

### Prompt Enviado:
> Escribe una función en Python bien documentada que implemente búsqueda binaria sobre una lista ordenada, incluyendo manejo de excepciones y 3 casos de prueba.

### Respuesta Generada:
```text
Aquí tienes una función en Python que implementa la búsqueda binaria sobre una lista ordenada. La función está bien documentada y incluye manejo de excepciones y 3 casos de prueba.

```python
def binary_search(arr, target):
    """
    Realiza una búsqueda binaria en una lista ordenada.

    Parámetros:
    arr (list): Lista ordenada en que se realizará la búsqueda.
    target (int): El valor objetivo a buscar.

    Retorna:
    int: El índice del elemento objetivo en la lista, si se encuentra. -1 si no se encuentra.

    Excepciones:
    ValueError: Si la lista no está ordenada.
    TypeError: Si el target no es un entero.

    Casos de prueba:
    >>> binary_search([1, 2, 3, 4, 5], 3)
    2
    >>> binary_search([1, 2, 3, 4, 5], 6)
    -1
    >>> binary_search([], 1)
    -1
    >>> binary_search([1], 1)
    0
    >>> binary_search([1, 2, 3, 4, 5], 'a')
    ValueError: 'a' is not an integer
    """
    # Verificar si la lista está ordenada
    if not arr or arr != sorted(arr):
        raise ValueError("La lista no está ordenada")

    # Verificar si el target es un entero
    if not isinstance(target, int):
        raise TypeError("El target debe ser un entero")

    # Inicializar los índices de inicio y fin
    low = 0
    high = len(arr) - 1

    # Realizar la búsqueda binaria
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1

    # Si no se encontró el target, devolver -1
    return -1

# Casos de prueba
if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

### Explicación de la función:

1. **Parámetros**:
   - `arr`: La lista ordenada en la que se realizará la búsqueda.
   - `target`: El valor objetivo a buscar.

2. **Retorno**:
   - El índice del elemento objetivo en la lista, si se encuentra. -1 si no se encuentra.

3. **Excepciones**:
   - `ValueError`: Si la lista no está ordenada.
   - `TypeError`: Si el target no es un entero.

4. **Casos de prueba**:
   - Se utilizan `doctest.testmod()` para ejecutar los casos de prueba y verificar que la función funcione correctamente.

5. **Documentación**:
   - La función está bien documentada con comentarios que explican cada paso del proceso y los tipos de excepciones que pueden ocurrir.

Este código es una implementación clara y fácil de entender de la búsqueda binaria, incluyendo las excepciones y casos de prueba necesarios.
```

---

