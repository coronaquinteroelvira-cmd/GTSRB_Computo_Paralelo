# GTSRB_Computo_Paralelo
## Evaluación del Rendimiento de SVM y Random Forest con Paralelización para Clasificación de Señales de Tráfico
En este proyecto se implementa un clasificador de señales de transito, haciendo uso del dataset **GTSRB (German Traffic Sign Recognition Benchmark)**.
En donde el objetivo, es hacer una comparación en el rendimiento que tiene un modelo entrenado de manera secuencial, contra una que fue hecha de manera paralela, haciendo uso de bibliotecas como `multiprocessing`, implementando SVM y Random Forest.

### Dataset
Se hace uso del dataset `GTSRB - German Traffic Sign Recognition Benchmark`, el cual contiene 43 clases diferentes de señales de tránsito alemanas.
El dataset se descarga automáticamente utilizando kagglehub, esto debido al tamaño que tiene el dataset, por lo que es más sencillo manejarlo de esta manera.

### flujo del programa

#### Descarga del dataset
El programa descarga el dataset desde Kaggle, esto debido al tamaño que tiene que este tiene, por lo que para manejarlo de mejor manera se opta por esta opción.

#### Preprocesamiento
Se cargan las imágenes de cada carpeta correspondiente y se le hacen los siguientes procesos, esto para ajustarse a las especificaciones que requiere el modelo, donde a cada imagen se procesa:
- Conversion a RGB.
- Redimensión a 96x96.
- Se normaliza entre valores de 0 y 1.
- Se vuelve un arreglo de numpy.

#### División del dataset
Una vez que el preprocesamiento de cada imagen fue hecho, se procede a hacer la división del dataset, en este caso se hizo con las proporciones de:
- 80% para entrenamiento.
- 20% para prueba.
#### Entrenamiento del modelo
El modelo SVM busca encontrar hiperplanos que separen correctamente las distintas clases, se utiliza una estrategia donde se generan múltiples fronteras de decisión entre clases.
El modelo aprende patrones utilizando las características principales generadas, ajusta los parámetros del hiperplano y maximiza la separación entre clases.
Ahora bien en la parte de paralelismo, el conjunto de entrenamiento se divide en:

- NUM_PROCESOS = 4

esta va a ser los subconjuntos independientes.
Donde cada subconjunto contiene:

- Parte de las imágenes.
- Sus etiquetas correspondientes.

Ahora bien cada proceso utiliza únicamente su subconjunto asignado, esto permite ejecutar múltiples entrenamientos simultáneamente aprovechando los varios núcleos del CPU.

#### Métricas
Ahora bien, se implementaron algunas métricas para observar el desempeño que tuvieron los modelos, tanto la versión secuencial, como la paralela, donde se buscó hacer la comparativa de rendimiento, que tanto se había equivocado, con la precisión y exactitud, así como métricas para la valoración del desempeño en paralelo, como lo son las métricas del speedup, y la eficiencia
