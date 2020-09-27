# EXAMEN FINAL - Poma Zamudio Camilo
## PREGUNTA 5:
### a. Ajuste y analice un modelo de regresión con interacción
Tenemos las siguientes variables:
* **Precio** de las viviendas (variable dependiente cuantitativa) : $Y$
* Superficie (variable independiente cuantitativa): $X_{1}$
* Antiguedad (variable independiente cuantitativa): $X_{2}$
* Presencia de aire acondicionado (variable independiente cualitatitva): $X_{3}$

Dado que es de suponer que las casas con poca antiguedad, es decir, las casas más recientes o nuevas, por ser modernas, es muy probable que tengan *aire acondicionado*.
Por ello, la interacción se considerará entre las variable *antiguedad* y *presencia de aire acondicionado*.

El modelo planteado es el siguiente:

$ Y =  \beta_{0}+ \beta_{1}X_{1} + \beta_{2}X_{2}+\beta_{3}X_{3}+\beta_{4}X_{2}X_{3} + \epsilon$

Teniendo como resultado un modelo significativo, pero las variables Superficie y Antiguedad resultan no significativos.
Utilizando el software R tenemos los siguientes resultados:

![todos.](captura.png)

De lo cual, el modelo resultante es:

$ Y =  98.81+ 0.44X_{1} - 0.79X_{2}+201.27X_{3}-4.54X_{2}X_{3} + \epsilon$

### b. Analice y explique si tiene algún impacto el aire acondicionado sobre el precio de las casas
Como podemos observar en la siguiente imagen:

![aire.](eee.png)

El coeficiente de la variable *aire* tiene un p-valor de 0.0269, lo cual, si trabajamos con un nivel de significancia del 10% podemos afirmar que esta variable es significativa para el modelo.

### b.Realice el análisis correspondiente para determinar si el modelo final funcionará bien en la realidad.

Realizamos el análisis de residuos para ver si el modelo cumple con los supuestos de normalidad, independiencia


![residuos.](rrr.png)

Según la gráfica podemos ver que los residuos no se distribuyen normalmente (histograma y gráfico QQ)

![residuos.](qqq.png)

Además, podemos ver que la varianza de los errores no es constante.

## PREGUNTA 1:
### i. En un modelo de regresión estimado por MCO es suficiente analizar el gráfico de residuos resultantes, para detectar observaciones influyentes.
Falso, es necesario analizar también gráficos de cajaso estadísticos como la distancia de Cook o estadísticas de apalancamiento.

### ii. En un modelo de regresión, siempre es necesario eliminar las observaciones influyentes, ya que su presencia empeora la bondad del ajuste (o R cuadrado) del mismo.
FALSO. Es cierto que al ser una observación influyente, este distorciona el ajuste del modelo ya que gráficamente hace que la recta de regresión gire hacia la posición en la que se encuentra. Pero, se debe tener bastante cuidado al retirar un par de observaciones.
### iii. En una regresión, la presencia de unas pocas observaciones influyentes puede alterar significativamente algunos resultados de la estimación MCO.
VERDADERO. El método MCO minimiza las distancias entre los valores observados y las valores estimados. De esta manera, si existe un valor alejado de los demás, provocaría un aumento en la varianza de los estimadores.

## PREGUNTA 2:
### a. Analizar el posible problema de multicolinealidad.

Con los datos proporcionados podemos hallar los estadísticos $t$ para la significancia individual del modelo. Esto realizando la división del coeficiente (valor estimado del parámetro) y su desviación estándar.

Para la variable $X_{2}$:
$ t_{calculado} = 0.7/0.56 = 1.25  $

Para la variable $X_{3}$:
$ t_{calculado} = 0.4/0.7 = 0.57  $

Para la variable $X_{4}$:
$ t_{calculado} = 0.1/0.5 = 0.20  $

Como se tienen $20$ datos y $4$ parámetros a estimar, entonces se tienen $ 20 - 4 = 16 $ grados de libertad.

El $t$ de tablas con 16 grados de libertad y un nivel de significancia del 5% es de $ 2.12$

Vemos que ninguno de los $t$ calculados son mayores a el estadístico $t$ de tablas. Además el coeficiente de determinación $R^2$ es muy cercano a $1$.

Calculemos la significancia global del modelo para llegar a una conclusión más acertada:

$F_{calculado} = \frac{ \frac{R^2}{k-1} }{ \frac{1-R^2}{n-k} } = 128 $

Nos resulta un valor muy grande. Lo cual comparado con el $F$ de tablas con un nivel de significancia del 5%:
$F_{tablas} = 3.24$

Resulta que el modelo es muy significativo, lo cual, sumado a que no existen coeficientes significativos podemos afirmar que existe presencia de multicolinealidad.
Es razonable obtenter un $R^2$ artificialmente bastante grande (inflado por presencia de multicolinealidad).

### b. Si hay algún problema, indique la forma más adecuada de solucionarlo.
La solución sería identificando a la variables o las variables que estén provocando la multicolinealidad y retirarlas del modelo.

## PREGUNTA 3:
### a. La autocorrelación entre las perturbaciones, ut, conduce a estimaciones sesgadas y errores sesgados cuando la regresión yt = βxt + ut es estimada por mínimos cuadrados ordinarios.
VERDADERO. La presencia de autocorrelación hace que la estimación MCO deje de ser eficiente ya que $\beta$ ya no es insesgado. Además, dependiendo del tipo de autocorrelación se tienen a cometer error de tipo I y II.

### b. El test de Durbin-Watson para la autocorrelación no es aplicable si las perturbaciones son heterocedásticas.
VERDADERO. Uno de los supuestos para aplicar este estadístico es que las perturbaciones sean homocedasticas.

## PREGUNTA 4:
### a) Detectar la posible presencia de heteroscedasticidad.
Para detectar la heteroscedasticidad en el modelo usamos el estadístico de Goldfeld Quant :

$ F_{calculado} = SCR_{2}/SCR_{1} = 97548/65432 = 1.5$

El cual, es menor que el $F$ de tablas = 2.27.
Por lo cual podemos afirmar podemos afirmar  presencia de heteroscedasticidad.

### b) Indique cuales serían los efectos que tendría la presencia de heteroscedasticidad sobre los estimadores por MCO y cómo se resolvería dichos efectos suponiendo que en este caso la varianza de las perturbaciones depende proporcionalmente del IPC.
Si hubiera heteroscedasticidad, los estimadores por MCO no serían los mejores. Para resolverlo se tendría que transformar el modelo a uno con perturbaciones
esféricas, de tal forma que al aplicarle MCO se obtuvieran estimadores lineales, insesgados y óptimos.
