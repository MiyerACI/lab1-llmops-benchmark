# Entregable Laboratorio 1: Benchmarking de Serving Local y Cuantización

- **Curso:** LLMOps, Serving Local y Arquitecturas RAG
- **Estudiante:** Miyer Arnulfo Cuetia Ipia
- **Hardware Utilizado:** Apple M1, 8GB, MacOS
- **Fecha:** 13 de noviembre de 2026

---

## Análisis Técnico de Resultados

### 1. Impacto en Memoria (MEM USAGE y KV Cache)
> ¿Cuál fue la diferencia exacta en MB/GB de RAM consumida entre `q4_K_M` y `q8_0` al ejecutar `docker stats`? ¿Por qué el consumo en ejecución supera el tamaño del archivo en disco?

**Respuesta:**
En reposo 15.51 MiB, Modelo qwen2.5:1.5b-instruct-q4_K_M: 1.233 GiB (39.94% del límite de 3.089 GiB), Modelo qwen2.5:1.5b-instruct-q8_0: 1.928 GiB (62.41% del límite de 3.089 GiB), Diferencia exacta: 0.695 GiB

---

### 2. Ancho de Banda de Memoria y Velocidad (TPS)
> En inferencia sobre CPU, el cuello de botella suele ser el ancho de banda de la memoria RAM. ¿En qué porcentaje aumentó la velocidad (TPS) al pasar de 8 bits a 4 bits?

**Respuesta:**
Modelo,Prompt,                                                               TTFT (ms),          Velocidad (TPS)
1.5b-instruct-q4_K_M,Corto (Definición),                           1318.94,           7.92
1.5b-instruct-q4_K_M,Medio (Razonamiento),                      2781.1,            7.58
1.5b-instruct-q4_K_M,Largo (Generación de Código),      2002.73,           7.66
1.5b-instruct-q8_0,Corto (Definición),                                  2168.39,            4.2
1.5b-instruct-q8_0,Medio (Razonamiento),                         4936.52,           4.25
1.5b-instruct-q8_0,Largo (Generación de Código),             3147.77,            4.47

Al pasar de 8 bits (q8_0) a 4 bits (q4_K_M), la velocidad promedio de generación aumentó en un 79.26%

---

### 3. Latencia Inicial (TTFT) y Fase Prefill
> ¿Por qué el `TTFT (ms)` es significativamente más alto en el Prompt Largo que en el Prompt Corto?

**Respuesta:**
Modelo,Prompt,                                                               TTFT (ms),          Velocidad (TPS)
1.5b-instruct-q4_K_M,Corto (Definición),                           1318.94,           7.92
1.5b-instruct-q4_K_M,Medio (Razonamiento),                      2781.1,            7.58
1.5b-instruct-q4_K_M,Largo (Generación de Código),      2002.73,           7.66
1.5b-instruct-q8_0,Corto (Definición),                                  2168.39,            4.2
1.5b-instruct-q8_0,Medio (Razonamiento),                         4936.52,           4.25
1.5b-instruct-q8_0,Largo (Generación de Código),             3147.77,            4.47

el TTFT alto del prompt largo ocurre porque el modelo debe procesar más tokens de entrada antes de poder generar la primera respuesta

---

### 4. Calidad vs. Eficiencia en `resultados_benchmark.md`
> Revisando las 6 respuestas completas generadas, ¿hubo alguna degradación perceptible en la lógica del código Python o en el razonamiento generado por el modelo de 4 bits frente al de 8 bits?

**Respuesta:**
No hubo degradación perceptible en q4_K_M frente a q8_0; de hecho, el modelo de 4 bits fue más estable. En programación, ambos implementaron correctamente la búsqueda binaria iterativa y validaron el orden de la lista, aunque q8_0 siguió mejor el formato pedido (TypeError y doctest). Sin embargo, en razonamiento arquitectónico q8_0 sufrió una alucinación severa (inventó modelos como "Claude 100") y cayó en un bucle repetitivo idéntico del punto 3 al 10, mientras q4_K_M mantuvo respuestas coherentes. En conclusión, q4_K_M ofrece un balance muy superior: gana un 79.26% en velocidad y ahorra 711.68 MiB de RAM sin perder calidad funcional

---
*Nota: Adjuntar junto con este documento los archivos generados `resultados_benchmark.csv` y `resultados_benchmark.md`.*
