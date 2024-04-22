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
<li><b>Restricción de Biyectividad</b>: Asegurar que cada hombre esté casado con una mujer diferente. Esto puede ser impuesto por una restricción global como “All Different” sobre las variables $M_1, M_2, …, M_n$.</li>
<li><b>Restricción de Estabilidad</b>: No deben existir dos parejas $(m, w)$ y $(m’, w’)$  tales que m prefiera a $w’$ sobre $w$ y $w’$ prefiera a $m$ sobre $m'$. Esta restricción puede ser un poco más compleja de implementar y a menudo requiere iterar pares de hombres y a menudo requiere iterar sobre pares de hombres y mujeres correspondientes, comparando sus preferencias.
 </li>
 </ul>
</p>
