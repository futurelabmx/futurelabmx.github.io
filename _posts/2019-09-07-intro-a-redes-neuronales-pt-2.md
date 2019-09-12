---
date: 2019-09-07
title: "Introducción a las Redes Neuronales Pt. 2"
categories:
  - Redes neuronales
  - Inteligencia Artificial
author_staff_member: 01-ulises
---

> ## Programación de un perceptrón en Python

#### Requerimientos:
- Editor de código (pycharm, jupyter notebook, vsc, etc)
- Python 3.6
- numpy

### Introducción
En el post anterior de "[Introducción a las Redes Neuronales Pt. 1](https://futurelab.mx/redes%20neuronales/inteligencia%20artificial/2019/06/25/intro-a-redes-neuronales-pt-1/)" explicamos los conceptos básicos que conforman al mundo de las redes neuronales, donde partimos del modelo de un perceptrón que es la parte fundamental y la unión de estos forman una red neuronal.

Para este segundo post haremos la implementación del perceptrón en el lenguaje de programación Python en su versión 3.6.8 utilizando el paradigma de programación orientado a objetos.

Retomames el modelo del perceptrón y el ejemplo de la compuerta lógica AND, donde obtenemos verdaero (1) si los dos casos de entrada son verdaderos (1).

###### Modelo de un perceptrón

![image1](/images/blog/perceptronE.png)

###### Compuerta Lógica AND

                            | Entrada A| Entrada B | Salida |
                            | ---------|-----------| -------|
                            |   0      |    0      |   0    |
                            |   0      |    1      |   0    |
                            |   1      |    0      |   0    |
                            |   1      |    1      |   1    |




> ### A programar!

Dentro de los procesos del modelo del perceptrón encontramos

1. Señales de entrada: Estos pueden ser valores boolenos, reales o valores enteros + un valor **b**  el caul es llamado **bias**

2. Pesos sinápticos: Se generan pesos aleatorios en el rango [-1,1] para dos entradas dadas

3. Unión Sumatoria: Se realiza la suma ponderada de entradas con pesos + **bias**

4. Función de activación: Indica si una salida se dispara hacia arriba o hacia abajo de acuerdo a la condición

5. Salida: Se realiza la comparación de la salida del perceptrón con la salida deseada

Siguiendo los procesos del modelo del perceptrón iremos programando nuestro perceptrón en python

###### Estructura del proyecto python
![image2](/images/blog/ProjectStructure.png)

#### Paso 1: Definición de las entradas del perceptrón que es una matriz de entradas más el valor **bias**

###### archivo main.py
```python
if __name__ == '__main__':

    inputs = [
        [0,0,1],
        [0,1,1],
        [1,0,1],
        [1,1,1]
    ]
```
Definimos las salidas

```python
    outputs = [0,0,0,1]
```

###### archivo Perceptron.py

```python
import numpy as np


class Perceptron:

      def __init__(self, inputs, outputs):
          self.inputs = np.array(inputs)
          self.outputs = np.array(outputs)
```

Importamos el modulo de numpy para poder convertir nuestra matriz de entrada en un arreglo de numpy y poder trabajarlo de manera más facíl.

Enseguida creamos la clase Perceptron el cual recibira la matriz de entrada y el arreglo de salidas las cuales serán convertidas a arreglos numpy al instanciar la clase Perceptron.


Ahora crearemos un método nombrado Fit (se refiere al entrenamiento de nuestro perceptrón). Primero definimos dos variables: epocas y num_inputs, el número de épocas indica el tiempo en épocas que se tardo el perceptrón en aprender las entradas encontrando los mejores pesos, y para el caso de num_inputs es una variable de control que sirve para detener el ciclo **while**, esta condición se cumple cuando el numero de salidas esperadas sea igual al número de salidas obtenidas.

###### Método Fit

```python
def Fit(self):
    epochs, num_inputs = 0, 0

    while num_inputs < 4:
        print('-------------------- epochs {} -------------------- '.format(epochs))
```

#### Paso 2: Generación de pesos aleatorios en el rango [-1,1].

```python
# se generan pesos aleatorios en el rango [-1,1]
weights = np.array(np.random.uniform(-1, 1, self.inputs.shape))
```

####  Paso 3: Unión sumatoria o suma ponderada de las entradas por los pesos.

Recorremos la matriz de entradas, la matriz de pesos y el vector de salidas. La función **zip** nos permite recorrer multiples estructuras en una sola corrida.

```python
for input,weight, output in zip(self.inputs, weights, self.outputs):

    # Realiza la suma ponderada de entradas con pesos
    y_generate = input@weight
```

Para realiza la suma ponderada utilizamos el operador **@** que nos permite realizar la sumatoria de las entradas por los pesos


![image3](/images/blog/plusWeighted.png)


#### Paso 4: Función de activación:
El funcionamiento de la función de activación es que si el resultado de la suma ponderada es menor a 0 la salida resultante es 0 y si el resultado de la suma ponderada es mayor a 0 entonces la salida resultante es 1

```python
# Función sigmoide
y_generate = 0 if y_generate < 0 else 1

```

#### Paso 5 Salida: Comparación de salidas obtenidas con salidas esperadas

```python
if y_generate == output:
   num_inputs +=1
else:
   num_inputs = 0
```

![image5](/images/blog/OutputComparation.png)

## Ejecución
En esta ejecución el perceptrón se tardo 5 épocas en aprender las entradas y encontrar los mejores pesos
![image6](/images/blog/Execution.png)

###### Link del repositorio: https://github.com/ugarciac/PerceptronPython

### Dudas, Comentarios, Críticas constructivas
Twitter: [@ugarciacal](https://twitter.com/ugarciacal)
Facebook: [UlisesGC](https://www.facebook.com/ulises.garciac)
