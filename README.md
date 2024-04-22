# TA1_CC82_TopicosCS

 <h2 align="center">Universidad Peruana de Ciencias Aplicadas</h2>
<h2 align="center">Tópicos en Ciencias de la Computación - CC58</h2>
 
<h3 align="center"> TB1</h3>
 
<h3 align="center"> Sección</h3>
<h3 align="center"> Profesor: Luis Martín Canaval Sanchez</h3>
<h3 align="center"> Alumnos</h3>
 <ul>
   <li align="center">Camargo Ramírez, Enzo Fabricio (U202010122)</li>
   <li align="center">Costa Mondragón, Paulo Sergio (U201912086)</li>
   <li align="center">Caballero Lara, Eduardo Roman (U202019644)</li>
 </ul>
 
 
 <h3 align="center">CICLO 2024-1</h3>


## Introducción
### Problema
<p align="justify">
El presente trabajo consiste en agrupar una pareja entre 2 grupos de 6 hombres y mujeres. A esta agrupación se le dará el nombre de matrimonio, para lo cual se deberá tener 6 parejas conformadas por un hombre y una mujer. No obstante, se nos da un criterio de condición, el cual es la inestabilidad entre las parejas por preferir a otro hombre o mujer.
 </p>
<p align="center">
  <img width="600" src="https://github.com/PSCostaM/TA1_CC82_TopicosCS/assets/48858434/dcadf064-99d3-425d-b632-e5ab98e7e144">
</p>
<p align="center">Tabla de preferencias</p>

### Motivación

<p align="justify">
 Para este trabajo tenemos la motivación de desarrollar un sistema para agrupar a los hombres y mujeres respetando el criterio de condición dado, el cual es que una pareja deberá estar casada como máximo con la cuarta persona de su preferencia. Ello con el fin de encontrar un matrimonio estable y duradero en este caso.
</p>

### Técnica propuesta

<p align="justifiy">
Para un conjunto de “n” hombres y “n” mujeres, es necesario definir una variable para cada hombre $m$. La variable para el hombre “m”, denota cómo $M_m$ tomará un valor del conjunto $[1,2,...,n]$, representando a las mujeres. Así, $M_m = i$ indica que el hombre $m$ está casado con la mujer $i$.
</p>

#### Establecer las restricciones
<p align="justify">
<ul>
<li><b>Restricción de Biyectividad</b>: Asegurar que cada hombre esté casado con una mujer diferente. Esto puede ser impuesto por una restricción global como “AllDifferent” sobre las variables $M_1, M_2, …, M_n$.</li>
<li><b>Restricción de Estabilidad</b>: No deben existir dos parejas $(m, w)$ y $(m’, w’)$  tales que m prefiera a $w’$ sobre $w$ y $w’$ prefiera a $m$ sobre $m'$. Esta restricción puede ser un poco más compleja de implementar y a menudo requiere iterar pares de hombres y a menudo requiere iterar sobre pares de hombres y mujeres correspondientes, comparando sus preferencias.
 </li>
 </ul>
</p>

#### Implementar las Restricciones de Estabilidad
<p>
Para las restricciones de estabilidad, para cada par de hombres m y m’, y cada par de mujeres w y w’, añadimos restricciones tales que:
 <ul>
<li>Si $M_m = w$ y $M_m’ = w’$, entonces:</li>
<ul>
<li>Si $P_m,w’$ < $P_m,w$ (es decir, $m$ prefiere a $w’$ sobre $w$), debe ser que $P_w’,m > P_w’,m’$ (es decir, $w’$ prefiere a $m’$ sobre $m$)</li>
</ul>
 </ul>
<h4>Resolver el problema</h4>
Debido al contexto del curso y lo aprendido en clase consideramos como OR-Tools de Google que puede manejar restricciones de manera eficiente. 
</p>

### Objetivos
<p align="justify">
 <ul>
<li>Encontrar un “matrimonio estable” y que cada pareja se encuentre agrupada.</li>
<li>Cumplir con la condición de preferencia, es decir, relacionar las parejas evitando agruparlas con personas de quinta o sexta preferencia.</li>
<li>Implementar una solución a las condiciones mediante un CSP (Problema de Satisfacción de Restricciones).</li>  
 </ul>
</p>

### Marco teórico

<p align="justify">
 El Algoritmo de Gale-Shapley, conocido por resolver el problema de emparejamiento estable, que proponen a sus candidatos preferidos, mientras que el otro conjunto acepta o rechaza estas propuestas según sus propias preferencias. La iteración continúa hasta que se logra un conjunto de emparejamientos donde nadie tiene incentivos para romper la pareja actual por otra preferida. Una de las cualidades distintivas de este algoritmo es su capacidad para siempre llegar a una solución estable, favoreciendo al grupo que hace las propuestas, y por lo tanto asegurando el mejor escenario posible para dicho grupo bajo la condición de estabilidad.
</p>

#### Pseudocódigo
```
Inicializar todos los m y w como solteros
mientras exista un hombre m que sea soltero y no haya propuesto a todas las mujeres:
    seleccionar tal hombre m
    w = primera mujer en la lista de preferencias de m a la que m aún no ha propuesto
    si w es soltera:
        (m, w) se comprometen
    sino si w prefiere m sobre su actual pareja m':
        w rompe el compromiso con m'
        (m, w) se comprometen
    sino:
        w rechaza a m
retornar el conjunto de parejas comprometidas
```
<p align="justify">
El Problema de Satisfacción de Restricciones (CSP) permite tratar con problemas donde se debe encontrar una asignación de valores a un conjunto de variables que satisfaga un conjunto de restricciones. 
</p>

#### Pseudocódigo
```
Procedimiento matrimonio_estable(preferencias_hombres, preferencias_mujeres):
    Inicializar modelo CSP
    Para cada mujer en preferencias_mujeres:
        Crear una variable CSP(elección del candidato) para la mujer con dominio igual al conjunto de todos los hombres
    Asegurar que todas las mujeres estén comprometidas con hombres diferentes usando una restricción AllDifferent
    Para cada mujer en preferencias_mujeres:
        Restringir las elecciones de la mujer a sus 4 principales preferencias de hombres
    Resolver el modelo CSP
    Si se encuentra una solución:
        Imprimir las parejas establecidas
    Sino:
        Imprimir que no se encontró una solución estable
```
### Planteamiento
<p align="justify">
Para el desarrollo del trabajo será fundamental el uso de las bibliotecas Or-Tools y Graphviz.
</p>

#### Or-Tools

<p align="justify">
Es una biblioteca de optimización combinatoria que nos permite utilizar herramientas para resolver problemas de optimización, incluido el problema de satisfacción de restricciones (CSP). Por ello, su uso será relevante para encontrar una solución óptima al momento de relacionar las parejas y encontrar un matrimonio estable.
 </p>
 
#### Graphivz

 <p align="justify">
Con esta biblioteca implementaremos grafos para conocer de manera gráfica las relaciones de las parejas. Nuestra solución será plasmada mediante estas estructuras para visualizar los matrimonios encontrados.
</p>


