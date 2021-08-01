# Proyecto de predicción de combates de Pokemons - Machine Learning
Este proyecto está basado en el Dataset de Kaggle: https://www.kaggle.com/shubhamchambhare/pokemons-and-there-stats

Creado por https://www.kaggle.com/shubhamchambhare

Es un Dataset con 1045 Pokemons y sus características: nombre, total, ataque, defensa, puntos de golpe, velocidad, ataque especial y defensa especial

La idea es crear un modelo predictivo para saber quién sería el ganador en una pelea entre dos Pokemons.

Para ello he realizado los siguientes procesos:

1- Transformación de datos originales añadiendo una característica más: Categoría, basado en la puntuación de la columna 'Total' del dataset.

2- Creación de una clase llamada Fight. Esta clase recibe el número de índice de 2 pokemons del dataset y nos devuelve el resultado del combate.

    Las reglas del combate no son las establecidas en el juego de cartas, sino que me he creado un sistema basado en las estadísticas proporcionadas por la base de datos, además de un componente aleatorio en relación a los porcentajes de daños de los ataques y de bloqueo de la defensa además de porcentajes de probabilidad de que ocurran atques y defensas especiales (explicación detallada en el apartado 2.5).
    El objeto resultado tiene las diferencias cuantitativas entre los valores de cada Pokemon y el ganador del combate. Otro paralelo tiene los mismos datos y las estadísticas aleatorias generadas (explicación detallada en el apartado 2.5).

3- Ese objeto es el que usaremos para crear nuestro modelo de ML, para ello creamos un dataset con un bucle que generará 186.750 enfrentamientos. Ese Dataset lo dividiremos en uno con el 60% de los enfrentamientos para entrenar y predecir los modelos y el 40% restante lo dejaremos sin tocar para evaluar los 3 mejores modelos más información en apartados 2.6 y 2.7. Esto nos deja un problema de clasificación binaria de aprendizaje supervisado.

4- Realizaremos pruebas con diferentes modelos y ensembles

5- Evaluaremos los modelos en función de varios conceptos y seleccionaremos los 3 mejores.

6- Con los 3 mejores volveremos a hacer fitting con todo el set de entrenamiento del 60% y lo validaremos de dos maneras:

    Obtendremos la accuracy del modelo para el 40% de los combates no vistos
    Haremos CrossValidation con el dataset del 40%
    El modelo ganador será el que obtenga la mejor media entre ambos valores

7- Con el modelo ganador haremos un fitting con toda la base de datos. Simularemos una puesta en producción con una pequeña interface a través de un formulario.

En este formulario también simularemos como si el propio modelo aprendiera con los nuevos combates de tal manera que cada 30 combates realiza dos acciones:

    Monitoriza con esos nuevos combates si el modelo sigue manteniendo buenas predicciones, sino lanza un aviso.
    Hace un fitting al modelo con el dataset completo y las nuevas 30 predicciones.

Además hay dos apéndices finales

Appendix 1: Permite hacer el tunning y el evaluado de todos los modelos de una vez

Appendix 2: Usando el modelo ganador, realiza las predicciones con el dataset que incluye las estadísticas aleatorias generadas en el combate. Aunque estas estadísticas son imposibles de conocer apriori, es un buen ejercicio para observar la importancia de la aleatoriedad en el performance del modelo.

IMPORTANTE

Los modelos y tunnig usados son mi elección. Entiendo que pueda haber otas opciones. Mi mejor resultado es 88.64% de accuracy. Si alguien quiere probar y encontrar mejores precisiones es bienvenido. En los repositorios dejo las bases de datos creadas para evitar tener que crearlas, además de así poder trabajar con los mismos datos
