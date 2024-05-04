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

### Desarrollo 
<p align="justify">
Marriage Problem fue desarrollado con OR-Tools. A continuación el código utilizado para la solución de este:
 
```python

from ortools.sat.python import cp_model
import graphviz

# Men and Women identifiers
men = ['Richard', 'James', 'John', 'Bill', 'Greg', 'Mario']
women = ['Helen', 'Tracy', 'Linda', 'Sally', 'Wanda', 'Mary']

# Preferences
# Men's preferences
men_preferences = {
    'Richard': [3, 5, 4, 2, 1, 6],
    'James': [3, 2, 5, 6, 4, 1],
    'John': [2, 4, 3, 1, 5, 6],
    'Bill': [5, 6, 4, 2, 3, 1],
    'Greg': [2, 5, 3, 6, 4, 1],
    'Mario': [1, 3, 4, 5, 6, 2]
}

# Women's preferences
women_preferences = {
    'Helen': [2, 4, 5, 3, 6, 1],
    'Tracy': [3, 5, 4, 2, 1, 6],
    'Linda': [1, 3, 6, 2, 4, 5],
    'Sally': [3, 2, 5, 6, 4, 1],
    'Wanda': [6, 4, 2, 1, 3, 5],
    'Mary': [6, 4, 3, 1, 5, 2]
}

# Model
model = cp_model.CpModel()

# Variables: man_to_woman[man][woman] is 1 if man is paired with woman
man_to_woman = {}
for man in men:
    man_to_woman[man] = {}
    for woman in women:
        man_to_woman[man][woman] = model.NewBoolVar(f'{man}_{woman}')

# Each man is paired with exactly one woman
for man in men:
    model.Add(sum(man_to_woman[man][woman] for woman in women) == 1)

# Each woman is paired with exactly one man
for woman in women:
    model.Add(sum(man_to_woman[man][woman] for man in men) == 1)

# Stability constraint: prevent instability in any pairing
for m1 in men:
    for w1 in women:
        for m2 in men:
            for w2 in women:
                if m1 != m2 and w1 != w2:
                    condition1 = men_preferences[m1][women.index(w2)] < men_preferences[m1][women.index(w1)]
                    condition2 = women_preferences[w2][men.index(m1)] < women_preferences[w2][men.index(m2)]
                    model.AddBoolOr([man_to_woman[m1][w1].Not(), man_to_woman[m2][w2].Not(), man_to_woman[m1][w2].Not(), man_to_woman[m2][w1].Not()])

# Solve the model
solver = cp_model.CpSolver()
status = solver.Solve(model)

# Graphviz setup
dot = graphviz.Digraph(comment='Stable Marriage Problem')

# Output results and build graph
if status == cp_model.OPTIMAL:
    for man in men:
        dot.node(man, man, color='lightblue2', style='filled')
    for woman in women:
        dot.node(woman, woman, color='lightpink1', style='filled')
    
    for man in men:
        for woman in women:
            if solver.Value(man_to_woman[man][woman]) == 1:
                print(f'{man} is married to {woman}')
                dot.edge(man, woman, color='red')
else:
    print("No stable marriage configuration found.")

# Render and view the graph
dot.render('stable_marriage_output', view=True, format='png')

```

</p>

![image](https://github.com/PSCostaM/TA1_CC82_TopicosCS/assets/48858434/debd15c9-325c-4084-85be-b03704cceba7)
Image showing the mariages that were created thanks to the code provided

### Conclusiones
<p align="justify">
Stable Marriage Problem (SMP) abordado mediante Google OR-Tools y visualizado con Graphviz proporciona una demostración sólida de cómo aplicar la programación por restricciones para resolver un problema combinatorio complejo. Aquí están las conclusiones clave de este trabajo:

#### 1. Efectividad de la Programación por Restricciones:
La programación por restricciones (CP) es muy efectiva para resolver problemas que se pueden modelar con variables, restricciones y, potencialmente, una función objetiva. El enfoque de CP en OR-Tools manejó eficientemente el SMP, que implica asegurar que cada participante esté emparejado bajo condiciones estrictas que previenen la inestabilidad.

#### 2. Complejidad y Escalabilidad:
El modelo manejó un escenario con seis hombres y seis mujeres, mostrando cómo CP puede gestionar conjuntos de datos de tamaño pequeño a moderado. Sin embargo, la escalabilidad a conjuntos de datos mucho más grandes debe considerarse, ya que la complejidad de agregar restricciones de estabilidad crece cuadráticamente con el número de participantes.

#### 3. Beneficios de la Visualización:
Usar Graphviz para visualizar los resultados proporcionó una comprensión clara e inmediata de los emparejamientos estables. Esta representación gráfica es invaluable, especialmente cuando se presentan los resultados a una audiencia que no está familiarizada con los detalles computacionales del problema.

#### 4. Verificación de Estabilidad:
Las restricciones añadidas al modelo aseguraron que no existiera inestabilidad dentro de los matrimonios, adhiriéndose estrictamente a la definición de estabilidad en el SMP. Este enfoque garantiza que todas las soluciones sean estables, pero no considera preferencias más allá de prevenir la inestabilidad, como optimizar la satisfacción general.

#### 5. Implicaciones Prácticas:
Aunque este modelo sirve como un buen ejercicio teórico y una demostración de las capacidades de CP, las aplicaciones del mundo real podrían requerir ajustes. Por ejemplo, los escenarios reales podrían introducir preferencias más dinámicas o la necesidad de manejar casos donde los participantes puedan optar por no emparejarse si no se encuentra un match adecuado.

#### 6. Limitaciones y Trabajo Futuro:
Optimización: Los modelos futuros podrían incluir objetivos de optimización, como maximizar la satisfacción general de las preferencias.
Preferencias Dinámicas: Manejar preferencias cambiantes a lo largo del tiempo podría hacer el modelo más realista y adaptable.
Conjuntos de Datos Más Grandes: Sería necesario probar y optimizar el modelo para grupos más grandes para entender sus limitaciones y mejorar la eficiencia.
#### 7. Valor Educativo:
Esta implementación es una excelente herramienta educativa para comprender tanto el problema del matrimonio estable como la aplicación de la programación por restricciones. Proporciona un marco práctico que puede extenderse o simplificarse según las necesidades educativas.

En conclusión, la aplicación de Google OR-Tools y Graphviz al problema del matrimonio estable destaca el poder de las herramientas computacionales modernas para resolver problemas clásicos de maneras innovadoras y eficientes. Este proyecto no solo resalta la practicidad de la programación por restricciones en la solución de problemas de asignación y emparejamiento, sino que también demuestra cómo estas soluciones pueden hacerse accesibles y comprensibles mediante una visualización efectiva.
</p>
