# Reporte Comparativo: Rendimiento de Modelos AlexNet y VGG16 en CIFAR-10

## 1. Introducción

El presente trabajo se enfocó en la evaluación comparativa del rendimiento de modelos de redes neuronales convolucionales, específicamente la arquitectura **AlexNet**, aplicados al conjunto de datos **CIFAR-10**.  Para llevar a cabo esta comparación, se implementaron y entrenaron modelos bajo dos enfoques principales:

*   **Desde cero ("from scratch"):**  Se recreó la arquitectura clásica de AlexNet, implementándola tanto en el framework **PyTorch** como en **Keras**. Estos modelos fueron entrenados sin pesos preexistentes, aprendiendo las características directamente desde los datos de CIFAR-10.
*   **Preentrenados (Fine-tuning):** Se aplicó la técnica de **fine-tuning** utilizando modelos pre-entrenados. En **PyTorch**, se utilizó un modelo AlexNet pre-entrenado en ImageNet, ajustando sus capas finales para la clasificación en las 10 clases de CIFAR-10.  Debido a la **ausencia de una versión oficial de AlexNet pre-entrenada directamente en Keras**, se optó por utilizar **VGG16 pre-entrenado en ImageNet como alternativa**, adaptando su arquitectura para la tarea de clasificación de CIFAR-10 mediante la modificación de su cabeza de clasificación.

Todos los experimentos descritos en este reporte se ejecutaron en el entorno de **Google Colab**, empleando una **GPU Tesla T4**. Si bien la Tesla T4 no representa la GPU de más alto rendimiento disponible, demostró ser **suficiente para llevar a cabo el entrenamiento de los modelos de manera exitosa**, permitiendo obtener resultados comparativos significativos en un tiempo razonable.

## 2. Metodología

### 2.1. Conjunto de Datos y Preprocesamiento

*   **Dataset:** Se utilizó el conjunto de datos **CIFAR-10**, un benchmark clásico en visión por computadora, compuesto por **60,000 imágenes a color de 32×32 píxeles**, distribuidas equitativamente en **10 clases** diferentes (avión, automóvil, pájaro, gato, ciervo, perro, rana, caballo, barco, camión).
*   **Preprocesamiento:** Previo al entrenamiento, las imágenes de CIFAR-10 fueron sometidas a un proceso de preprocesamiento homogéneo en todos los experimentos. Este proceso consistió en:
    *   **Redimensionamiento:**  Las imágenes de entrada fueron **redimensionadas a un tamaño de 224×224** para asegurar la compatibilidad con la arquitectura AlexNet y VGG16, que típicamente operan con imágenes de mayor resolución.
### 2.2. Modelos Implementados

Para la comparación del rendimiento, se implementaron las siguientes arquitecturas y estrategias de entrenamiento:

*   **Modelos "from scratch" (Entrenados desde cero):**
    *   **AlexNet en PyTorch:** Se implementó la arquitectura original de AlexNet en PyTorch, caracterizada por tener **5 capas convolucionales, 3 capas de Max Pooling y 3 capas densas**. Este modelo fue entrenado completamente desde cero, con pesos inicializados aleatoriamente, utilizando el conjunto de datos CIFAR-10.
    *   **AlexNet en Keras:**  Se realizó una implementación de la arquitectura AlexNet similar a la de PyTorch, utilizando el framework Keras.  Al igual que la versión en PyTorch, este modelo fue entrenado desde cero con los datos de CIFAR-10.


*   **Hardware:** Todos los experimentos se ejecutaron utilizando la plataforma **Google Colab**, haciendo uso del acelerador por hardware **GPU Tesla T4** proporcionado por el entorno.

## 3. Resultados

A continuación, se presentan los resultados detallados de entrenamiento y evaluación obtenidos para cada modelo implementado.

### 3.1. Modelos "From Scratch"

#### AlexNet en PyTorch

| Época | Accuracy (%) |
|-------|--------------|
| 1     | 26.48        |
| 2     | 57.19        |
| 3     | 64.49        |
| 4     | 74.29        |
| 5     | 77.57        |

**Tiempo total de entrenamiento:** 90 min

**Precisión en el conjunto de test (Prueba):** 82.78%

#### AlexNet en Keras

| Época | Accuracy (%) | Val_accuracy (%) |
|-------|--------------|-----------------|
| 1     | 32.96        | 54.33           |
| 2     | 54.81        | 69.53           |
| 3     | 71.24        | 74.53           |
| 4     | 77.69        | 72.56           |
| 5     | 78.55        | 73.58           |


**Tiempo total de entrenamiento:** 35 min.


### 3.2. Modelos Preentrenados (Fine-tuning)

#### AlexNet preentrenado en PyTorch

| Época | Accuracy (%) |
|-------|--------------|
| 1     | 68.11        |
| 2     | 81.43        |
| 3     | 84.82        |
| 4     | 87.12        |
| 5     | 89.46        |


**Tiempo total de entrenamiento:**  67 min



#### VGG16 en Keras

| Época | Accuracy (%) | Val_accuracy (%) |
|-------|--------------|-----------------|
| 1     | 54.42        | 84.25           |
| 2     | 73.76        | 88.71           |
| 3     | 80.45        | 89.49           |
| 4     | 82.64        | 82.16           |
| 5     | 85.82        | 84.56           |
**Tiempo total de entrenamiento:** 50 min

