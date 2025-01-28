# Análisis de Datos en iGaming: insights visuales para la toma de decisiones estratégicas según patrones de depósito en usuarios de servicios de entretenimiento y apuestas.

## Resumen

Este proyecto tuvo como propósito realizar un análisis de datos integral de los usuarios y sus depósitos en servicios de entretenimiento y apuesto del sector iGaming, buscando identificar patrones de comportamiento, detectar las diferencias entre predicciones internas del negocio y datos observados, y desarrollar un tablero visual BI para facilitar la interpretación y toma de decisiones basadas en datos. El proceso analítico fue realizado sobre datos en crudo suministrados por una empresa ecuatoriana de juegos de casino y apuestas en línea. Este estudio tuvo como propósito principal contribuir con información de valor para la creación de estrategias de adquisición y retención de jugadores. 

Aunque los datos no son representativos debido al tamaño reducido de la base de datos general, su calidad en términos de características o variables relacionadas con la dinámica de los depósitos y los costos asociados a los usuarios y unidades de publicidad, es muy bueno. No obstante, aunque puede realizarle un análisis general de los datos, no pueden modelarse estadísticamente para obtener información más confiable por las limitaciones existentes. 

El análisis permitió evidenciar que en el año 2023 se redujeron las diferencias entre el pronóstico de los indicadores FTD y CPA y los resultados, adicionalmente, aumentaron los depósitos gracias a la mayor estabilidad y confianza en los servicios. En general, todos los usuarios pueden dividirse en dos grupos muy distintos, los “rollers” y los “casuales”, destacando la necesidad de estrategias específicas para optimizar costos y beneficios según el perfil de juego de cada uno. En este mismo sentido, aunque el costo de adquisición por jugador suele ser en promedio moderado-bajo para una empresa emergente en el sector de apuestas y juegos de azar, algunos periodos mensuales presentaron costos elevados por estrategias de marketing poco efectivas, sobre todo en el año 2022 cuando la compañía inició operaciones, lo que requiere un análisis más a fondo para identificar los factores de riesgo asociados al proceso de atracción de nuevos usuarios a los servicios iGaming/iGambling.

## Entendimiento de la problemática del negocio

La Superintendencia Financiera de Colombia (Superfinanciera), que opera como ente máximo regulador de las entidades del sistema financiero colombiano, comparte datos sobre las FIC y su rentabilidad periódica a corto, mediano y largo plazo, de manera pública, desde enero de 2016. Esta información que hace parte del proyecto de datos abiertos nacionales para la transparencia y generación de conocimiento, es la base fundamental del presente proyecto en el que se busca entender la dinámica operativa de los fondos y la incidencia de las estrategias de los inversionistas en la generación de rentabilidad en todos los periodos mensuales del año 2024, con intención de construir un modelo predictivo que permita un acercamiento a las rentabilidades esperadas del primer mes del año 2025. 

## Entendimiento de los datos

El conjunto de datos aportados por la Superfinanciera está comprendido por 2,293,315 registros y 26 campos, de los cuales se extrajo solamente 342,565 registros que comprenden todo el histórico del año 2024. Las características o variables incluyen información sobre la fecha exacta de la operación diaria, el tipo y nombre de la empresa que administra el FIC, el tipo y nombre legal del patrimonio común, el compartimento usado en la operación del fondo, el tipo de participación de los inversores, el número de inversores, los valores de precierre y cierre del fondo diario, los rendimientos abonados, el numero de unidades operativas en el fondo, el valor de los aportes recibidos por los inversores, el valor de los retiros, redenciones y anulaciones; y la rentabilidad diaria, mensual, semestral y anual de los fondos.
Los gráficos a continuación muestran la distribución de los registros y la evolución de la rentabilidad promedio según cada periodo mensual del año 2024.

**Figura 1. Distribución de los registros por mes del año 2024**
<p align="center">
    <img src="assets/img/img1.png" alt="Distribución de los registros" width="700">
</p>
La cantidad de operaciones registradas se mantiene relativamente estable a lo largo de los meses, lo que indica que no existen fluctuaciones significativas en la actividad mensual. Esto sugiere una operación constante en los FIC durante todo el año.

####

**Figura 2. Evolución de la rentabilidad prommedio mensual 2024**
<p align="center">
    <img src="assets/img/img2.png" alt="Evolución de la rentabilidad promedio mensual" width="700">
</p>
Enero mostró la rentabilidad más alta, alcanzando un valor cercano al 11%. Sin embargo, esta cayó rápidamente durante los primeros meses. En abril, la rentabilidad promedio llegó a su punto más bajo, con valores alrededor del 6%. Entre mayo y agosto, se observó una tendencia al alza, alcanzando un segundo pico en agosto. Desde septiembre, la rentabilidad mostró una caída sostenida, terminando en diciembre con valores bajos similares a los observados en abril.

####

***NOTA:*** Como parte de la preparación para modelado de los datos, se eliminaron columnas innecesarias, se verificaron valores nulos y registros duplicados, se gestionaron valores atípicos y se realizó un formateo de algunas variables al tipo de dato correcto.

## Modelado y Evaluación

Con base en el análisis exploratorio de datos y el estudio de las correlaciones entre variables, se formuló antes del modelado analítico, el supuesto inicial de baja predictibilidad de las características operativas de los fondos sobre su rentabilidad mensual. El gráfico de calor a continuación, muestra la importancia de las características del modelo Random Forest.

**Figura 3. Correlación de las variables**
<p align="center">
    <img src="assets/img/img4.png" alt="Importancia de las características" width="700">
</p>

A pesar de haber identificada la poca existencia de correlaciones entre la rentabilidad mensual y las variables predictoras, se demostró que la hipótesis de que ningun modelo podría ajustarse correctamente a los datos para realizar predicciones aceptables, era parcialmente incorrecta una vez se probaron los algortimos de modelado. Aunque las variables operativas tengan muy baja correlación individual con la rentabilidad mensual de los FIC, el modelo de Random Forest logró modelar relaciones complejas entre estas variables y el objetivo. Esto sugiere que hay información útil en las variables, aunque no sea obvia con modelos simples como los de regresión lineal.

Se seleccionó un modelo de bosques aleatorios (Random Forest) como opción ganadora, el cual se encuentra compuesto por 100 árboles de decisión para determinar el peso de incidencia de cada carcaterística operativa sobre la rentabilidad mensual de los FIC. El gráfico a continuación muestra que el valor unitario de las operaciones de inversión (valor_unidad_operaciones), el valor del cierre diario del fondo (valor_fondo_cierre_dia_t) y la cantidad de proyectos en los que ha participado (numero_proyectos) contityen los dos factores cláves al momento de determinar la rentabilidad mensual, con un peso conjunto de más del 60% de incidencia. 

El gráfico de barras horizontales muestra la importancia de las características del modelo Random Forest.

**Figura 4. Importancia de las variables en el modelo Random Forest**
<p align="center">
    <img src="assets/img/img3.png" alt="Importancia de las características" width="700">
</p>

En cuanto al desempeño, el modelo explicó aproximadamente el 84.73% de (R2) la variabilidad de la rentabilidad, indicado que tiene un buen desempeño. Por otro lado, en promedio, las predicciones del modelo tienen un error de ±29.62% de la rentabilidad (MSE = 0.087763 equivalente a RMSE = 0.2962). Aunque el R2 es alto, un error promedio (RMSE) de aproximadamente 29.62% puede ser significativo en el contexto de rentabilidad, ya que podría hacer que las predicciones sean imprecisas en escenarios donde se necesitan estimaciones más ajustadas. Por lo tanto, en fúturos proyectos internos de creación de horizontes financieros no es recomedable la utilización de un modelo analítico basado solamente en variables operativas


## Conclusión

- Los fondos de inversión colectiva (FIC) de tipo general tienen, por mucho, el mayor número de registros operativos. Este segmento es claramente el más activo dentro del mercado en el año 2024.
-  Los FIC de mercado monetario, inmobiliarios y bursátiles parecen estar infrautilizados o tener una base de clientes más reducida. Esto resulta en una oportunidad para las administradoras que busquen diversificar su oferta o atraer nuevos inversionistas.
-  Las sociedades fiduciarias parecen ofrecer mayor estabilidad y consistencia en los retornos mensuales, lo que podría ser atractivo para inversores conservadores.
-  Los comisionistas de bolsa reflejan un perfil más arriesgado, con mayores posibilidades de obtener altos retornos, pero también con un mayor riesgo de pérdidas significativas.
- La falta de correlación significativa en el análisis inicial no implicó ausencia de información útil en las variables. Random Forest, al ser un modelo no lineal y basado en árboles, pudo detectar interacciones complejas y patrones no evidentes en los datos.
- Se realizaron segundas validaciones cruzadas sobre el modelo ganador Random Forest para verificar que el desempeño aceptable sobre los datos de prueba no se debiese a simple azar, se encontró que incluso con 10 subjconjunto de pruebas cruzadas, el modelo siguió desempeñandose muy bien con un R2 medio de 0.847 y un MSE de 0.087 siendo incluiso ligeramente superior al primer modelo Random Forest desarrollado. En este sentido, se confirma que el modelo Random Forest es el que mejor se ajustó correctamente a los datos y se escogió como base para estudiar el peso de las variables predictoras sobre la rentabilidad mensual. No obstante, en futuras investigaciones, se debe analizar un poco más a fondo si puede llegar a existir un sobre ajuste díficil de detectar con solo realizar validaciones cruzadas.
- En escenarios fúturos de investigación se recomienda utilizar técnicas adicionales como SHAP o LIME para entender cómo las variables más importantes (como valor_unidad_operaciones, valor_fondo_cierre_dia_t) están influyendo en las predicciones. Esto puede dar insights adicionales sobre las relaciones subyacente. Si es posible, añadir más variables operativas o del contexto macroeconómico donde se ven envueltos los FIC para estudiar si es posible mejorar aún más el modelo.
