# Proyecto KNN Classifier

Este repositorio contiene la implementación de un clasificador KNN (K-Nearest Neighbors) en Java, diseñado para realizar clasificación supervisada sobre conjuntos de datos proporcionados por el usuario. 

---

## Descripción General

La clase principal del proyecto es `KNNClassifier`, que implementa el algoritmo KNN con funcionalidades para:

- Cargar y gestionar un conjunto de datos (dataset) de instancias.
- Dividir el dataset en conjuntos de entrenamiento y prueba mediante una proporción definida.
- Ejecutar la clasificación para una o múltiples instancias usando el método KNN.
- Calcular distancias entre instancias usando una métrica configurable (por ejemplo, distancia Euclidiana).
- Aplicar un esquema de votación ponderada para la predicción de la clase.
- Evaluar el desempeño con una matriz de confusión y cálculo de precisión.

---

## Detalles de la Clase KNNClassifier

### Atributos Principales

- `instances`: Lista de instancias cargadas.
- `trainSet`, `testSet`: Subconjuntos de entrenamiento y prueba, separados según el ratio definido.
- `k`: Número de vecinos más cercanos a considerar para la clasificación.
- `distanceMetric`: Función para calcular la distancia entre instancias.
- `weightingScheme`: Estrategia para ponderar el voto de los vecinos (por ejemplo, uniforme o basada en distancia).

### Métodos Clave

- `splitDatasetRatio(ratio, random)`: Divide aleatoriamente el dataset en conjuntos de entrenamiento y prueba.
- `runExperiment()`: Ejecuta la clasificación sobre el conjunto de prueba y actualiza la matriz de confusión.
- `classify(instance)`: Clasifica una instancia usando el algoritmo KNN.
- `computeDistance(a, b)`: Calcula la distancia entre dos instancias.
- `predictClass(neighbors)`: Determina la clase predicha con base en los vecinos y el esquema de votación.
- `updateConfusionMatrix(actual, predicted)`: Actualiza la matriz de confusión tras cada clasificación.
- `computeAccuracy()`: Calcula la precisión global del clasificador.

---

## Flujo de Ejecución General

1. **Carga del dataset:** Las instancias son cargadas en memoria.
2. **Configuración:** Se define el valor de `k`, la métrica de distancia y el método de ponderación.
3. **División del dataset:** Se divide en conjuntos de entrenamiento y prueba según un ratio configurado.
4. **Clasificación:** Se ejecuta el algoritmo KNN para cada instancia del conjunto de prueba.
5. **Evaluación:** Se calcula la matriz de confusión y la precisión del modelo.
6. **Resultados:** Se muestran los resultados al usuario.

---

## Diagrama de Comunicación General

```mermaid
graph LR
  User --> Main["Main: inicia programa y recibe opción de usuario"]
  
  Main --> EM["splitDatasetRatio(ratio, random): genera trainSet y testSet"]
  EM --> DS["getInstances(): recupera todas las instancias"]
  EM --> EM2["shuffleSplit(): baraja o hash split"]
  EM --> EM3["assignTrainTest(): llena trainSet y testSet"]
  EM --> Main["doneSplit(): división completada"]
  
  Main --> EXP["runExperiment(): inicia experimento"]
  EXP --> DS2["getInstances(testSet): obtiene subconjunto prueba"]
  EXP --> KC["classify(instance): clasifica instancia"]
  
  KC --> DM["computeDistance(a, b): calcula distancia"]
  DM --> KC["distance: valor de distancia"]
  KC --> CWS["getWeight(distance): calcula peso voto"]
  CWS --> KC["weight: valor del peso"]
  KC --> PC["predictClass(neighbors): vota y elige clase"]
  PC --> KC["label: etiqueta predicha"]
  KC --> EXP["prediction: clase predicha"]
  
  EXP --> UM["updateConfusionMatrix(actual, predicted): actualiza matriz confusión"]
  UM --> CA["computeAccuracy(): calcula precisión"]
  CA --> Main["doneExperiment(): experimento finalizado"]
  
  Main --> User["printResults(): muestra matriz y precisión"]
