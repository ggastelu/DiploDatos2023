# **Mentoria07**
## ** Cambio climático y ML: cómo mitigar las emisiones de CO2 mediante la reducción del consumo energético en construcciones edilicias **

**Integrantes:**
- [Carubelli, Marianella](https://github.com/Mariandela)
- [Gastelu, Gabriela](https://github.com/ggastelu)
- Rubio, Natalia
- [Santos, Maricel](https://github.com/MaricelSantos)

- **Mentora:**
    - [Tamara Maggioni](www.linkedin.com/in/tam-maggio)

En este proyecto se propone mitigar los efectos del cambio climático mediante el análisis de la eficiencia energética de una de las industrias más contaminates (en términos de sus emisiones de CO2) a escala global: la industria de la construcción. Se busca predecir el consumo energético de las edificaciones utilizando un set de datos que contempla algunas características de edificios ubicados en la costa NE de Estados Unidos (mayormente Nueva York) junto con datos climáticos y meteorológicos de los sitios donde dichos edificios están emplazados.

De esta manera, los agentes gubernamentales, tomadores de decisiones y las empresas constructoras podrían contar con una herramienta basada en ML para elaborar normativas, propuestas y/o acciones tanto preventivas (para nuevas construcciones) como de reacondicionamiento (para viejas construcciones).

- [**Base de datos cruda**] (https://raw.githubusercontent.com/TamaraMaggioni/Cambio-climatico-y-ML/main/energy.csv)

### **Objetivos propuestos:**

- Utilizar herramientas del ML y la ciencia de datos para ayudar en los esfuerzos de lucha contra el cambio climático.
- Construir un modelo que prediga con un grado aceptable de error el consumo energético de las edificaciones.
- Estudiar y elegir las mejores métricas que podemos implementar en un problema de regresión.
- Estudiar las variables que más influyen en la emisión de CO2 de las construcciones: ¿las características de las edificaciones o las variables climáticas?

### **Variables:**

Las variables o features que corresponden a características de los edificios son:

- facility_type: tipo de edificación (comercial, residencial, oficina, …)
- floor_area: área edificada
- year_built: año de construcción
- ELEVATION: altura sobre el nivel del mar

Las variables restantes corresponden a variables climáticas o meteorológicas:
- cooling_degree_days: una medida que indica cuán calurosa la temperatura fue en cierto día o cierto período de días 
- precipitation_inches: promedio de precipitaciones en pulgadas
- snowfall_inches: promedio de nevadas en pulgadas
- snowdepth_inches: promedio del grosor de la capa de nieve en pulgadas
- days_below_0F: días bajo 0 grados Farenheit
- days_above_80F: días sobre los 80 grados Farenheit
- days_above_90F: días sobre los 90 grados Farenheit
- days_with_fog: días con neblina
- winter_average_temp: temperatura promedio de invierno
- summer_average_temp: temperatura promedio de verano
- fall_average_temp: temperatura promedio de otoño
- spring_average_temp: temperatura promedio de primavera
- winter_average_maxtemp: temperatura máxima promedio de invierno
- summer_average_maxtemp: temperatura máxima promedio de verano
- fall_average_maxtemp: temperatura máxima promedio de otoño
- spring_average_maxtemp: temperatura máxima promedio de primavera
- winter_average_mintemp: temperatura mínima promedio de invierno
- summer_average_mintemp: temperatura mínima promedio de verano
- fall_average_mintemp: temperatura mínima promedio de otoño
- summer_average_mintemp: temperatura mínima promedio de primavera

### **Metodología:**

El trabajo de mentoría se dividió en tres trabajos prácticos:

- TP1: Análisis estadístico y visualización de las variables de la base de datos

- TP2: Análisis exploratorio y curación de datos
*Se procedió a la corrección, modificación y separación de la base de datos en los grupos: train, test y validación*
*Se plantearon 8 modelos distintos para luego comparar su comportamiento en los modelos de regresión*
Los pasos ejecutados en esta curación fueron:

P1: Eliminación de columnas con cantidad de datos faltantes mayor al 50%  
P2: Eliminación de filas duplicadas  
P3: Cambio de unidades SI  
P4: Traducción de features  
P5: Agrupación de variable categorica  
P6: Eliminación de variables correlacionadas

S1: OneHotEncoding  
S2: Eliminación de Outliers  
S3: Normalización  
S4: Escalado  
S5: Imputación

![Grafo1](https://graphonline.ru/tmp/saved/NN/NNInpQZDQTVcfoIp.png)

Por lo tanto, los ocho modelos de bases de datos son:
* M1_S3: Sin eliminación de variables correlacionadas, normalizado y eliminando las variables con datos faltantes
* M2_S4: Sin eliminación de variables correlacionadas, escalado y eliminando las variables con datos faltantes
* M3_S5: Sin eliminación de variables correlacionadas, normalizado y con datos imputados
* M4_S5: Sin eliminación de variables correlacionadas, escalado y con datos imputados
* M5_S3: Con eliminación de variables correlacionadas, normalizado y eliminando las variables con datos faltantes
* M6_S4: Con eliminación de variables correlacionadas, escalado y eliminando las variables con datos faltantes
* M7_S5: Con eliminación de variables correlacionadas, normalizado y con datos imputados
* M8_S5: Con eliminación de variables correlacionadas, escalado y con datos imputados

- TP3: Aprendizaje Supervisado
*Se definieron los modelos de regresión a utilizar y las métricas de evaluación. Se evaluó no sólo la performance de distintos modelos, sino que también se buscaron, entre las variables analizadas, cuáles tienen mayor relevancia en nuestra problemática.*
En esta etapa se agregaron cuatro modelos de bases de datos nuevas:
* df_dc0_c0_e0_t0 (df con todas las features, excluyendo los datacenter, con todos los valores de la variable target, sin imputar los valores faltantes y sin escalado)
* df_dc0_c1_e0_t0 (df con todas las features, excluyendo los datacenter, sin valores extremos de la variable target, sin imputar los valores faltantes y sin escalado)
* df_dc0_c1_e0_t1 (df con todas las features, excluyendo los datacenter, sin valores extremos de la variable target, imputando los valores faltantes y sin escalado)
* df_dc0_c1_e1_t1 (df con todas las features, excluyendo los datacenter, sin valores extremos de la variable target, imputando los valores faltantes y con escalado con StandardScaler)

### **Conclusiones:**
En un primer análisis con los distintos modelos de bases de datos, observamos que:
- Los dataframes sin imputación de la variable ranking dan valores muy bajos en las metricas.
- Los mejores modelos son aquellos que hacen boosting.

Luego de un proceso iterativo, probando distintos modelos, llegamos a la conclusión de que el tratamiento para obtener las mejores metricas que generalizan predicciones de datos nuevos lo conseguiremos utilizando los modelos m8_s5 y df_dc0_c0_e0_t0:

- **m8_s5:**
Pasos previos a curacion para mx_sy:

Eliminacion de filas con porcentaje de datos faltantes mayores al 50%
Eliminación de filas duplicadas
Agrupación de variable categoricas
Eliminación de features correlacionadas entre sí en mas del 50% (se dejó sólo la más correlacionada con la target)
Curación para mx_sy:

OneHotEncoding
Escalado MinMaxScaler
Imputación KNNImputer
Separacion 80/20 en train/test

Modelo: GradientBoostingRegressor

Parametros:
max_depth=15,
learning_rate = 0.1
min_samples_split=50,
min_samples_leaf = 1
n_estimators=200
random_state=42
Metricas:
mse_train: 4589.49
r2_train: 0.86
mse_test: 15505.29
r2_test: 0.54

- **df_dc0_c0_e0_t0:**
Pasos de previos curacion para df_dc0_c0_e0_t0:

Contiene todas las columnas del dataset original.
Eliminacion de outliers de la variable target (datos mayores al promedio más 2 sigmas).
Agrupación de tipos de edificios con poca frecuencia.
Eliminación del grupo datacenter.
Curación para dc0e0:

OneHotEncoding
Escalado StandardScaler
Imputación KNNImputer
Separacion 70/15/15 en train/val/test

Modelo: GradientBoostingRegressor

Parametros:
n_estimators = 200
max_depth = 15
min_samples_split = 50,
min_samples_leaf = 1,
learning_rate = 0.1,
random_state = 42)
Metricas:
mse_train: 2006.08
r2_train: 0.83
mse_test: 5211.33
r2_test: 0.55

**Features Importance:**

Es muy ineresante notar que a pesar de que m8 y dc0 son df curados de manera muy diferentes, obtienen métricas similares y en particular, si analizamos las 10 features más importantes para el modelo, hay una gran intersección en ambos modelos. Hay una intersección de 8 sobre 10 (aunque el orden varia levemente entre un modelo y el otro, estas 8 son las mismas). Estas son:

- superficie_cubierta_m2
- ranking_eficiencia_energética
- año_construcción
- tipo_instalación_Salud
- tipo_instalación_Otros
- altura
- tipo_instalación_Depósito
- tipo_instalación_Residencial

Si hacemos un análisis de estas variables, podemos decir que las dimensiones del edificio están directamente relacionadas con el gasto energético. Esto es razonable ya que a mayor dimensión mayor gasto, sin embargo quí resulta de interés observar como la variable target es de consumo energético por unidad de área, se observa que el tamaño del edificio (es decir la superficia total construida) es una variable muy importante en la prediciñon, indicando que no es lineal el consumo por unidad de area (si fuese asi todos los edificios tendrian el mismo consumo por unidad de area). Esto es muy im portante a la hora de tomar decisiones sobre los tamaños a contruir.

En segunda instancia aparece el ranking de eficiencia. Si bien se esperaba que esta variable fuera muy explicativa, el desafío fue la cantidad de valores faltantes de esta variable. El modelo fue exitoso en imputar datos faltantes y capturar poder de predicción. En este sentido, otra variable con datos faltantes (aunque mucho menor porcentaje) es el año de edificación que aparece como 3° variable de importancia. Esto puede deberse a las tecnologías y materiales utilizados que al avanzar en el tiempo deberían estar más adecuados a prestaciones de menor consumo.

Luego tenemos un grupo de variables referidas al tipo de edificio, entre las cuales aparecen: centros de salud, otros, depósito y residencial. Algunas conjeturas que podemos hacer son: Los centros de salud tienen seguramente grandes consumo debido al tipo de actividad. En “otros” están incluidos grupos como data center, con grandes consumos (aunque en dc0 ese grupo estaba excluido). Los depósitos por otro lado seguramente tengan grandes superficies y menos consumo.

Entre las últimas variables aparece la altura sobre el nivel del mar, una variable de la cual no podemos tener explicaciones tan intuitivas como las demás, pero podríamos especular que a mayor altura, se espera que las temperaturas sean más bajas y la temperatura media de invierno se encuentra entre las variables explicativas. Esto también puede ser importante a la hora de decidir dónde realizar o no una construcción.

Por último, podemos decir respecto a las variables climáticas que las mismas aportan muy poca o nula explicación, excepto por la de temperatura medias de la época mas fría, indicando que el gasto de energía es mayor para calefaccionar que para enfriar en épocas cálidad. Esto está en corcondacia con la observación que hicimos en el 1 TP de que las variables referidas al frio tienen mucha mayor correlación con la variable target que las referidas al calor, lo cual estaría indicando que el mayor consumo se debe al hecho de calefaccionar y no tanto de enfriar. Esto también puede ser importante a la hora de diseñar edificios, que tengan en cuenta la variable frio.

En conclusión, respecto a cómo se configura el modelo y cuáles son las variables más explicativas y, por lo tanto, aquellas que tendremos que tener bien definidas para hacer buenas predicciones al recibir nuevos datos son los siguientes: las dimensiones de edificio mismo, como rankea en eficiencia, su año de construcción; la función del edificio, la elevacion sobre el nivel del mar y las temperaturas medias de la estaciones más frías.


