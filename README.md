# Evidencia-Implementacion-de-Analisis-Lexico
## Lenguajes y Autómatas 

Los lenguajes formales y los autómatas son conceptos fundamentales en la teoría de la computación ya que estos permiten modelar cómo una máquina puede leer una secuencia de símbolos y determinar si dicha secuencia pertenece o no a un lenguaje específico. A través de estos modelos es posible representar distintos procesos de reconocimiento de patrones utilizados en computación.

En este proyecto profundizaremos un poco sobre estos temas analizando un conjunto de palabras pertenecientes a un lenguaje ficticio y construyendo un autómata finito determinista (DFA) capaz de reconocerlas, asi mismo se presentará la expresión regular que describe el mismo lenguaje y mostraré su implementación a traves de un programa y un análisis de los resultados.

Empecemos definiendo que es un autómata, "un autómata es una construcción que posee las características fundamentales de una computadora digital, ya que puede recibir una entrada, producir una salida, almacenar información temporalmente y tomar decisiones durante la transformación de la entrada en la salida" (Linz & Rodger, 2022). Por otro lado un lenguaje formal puede describirse como una representación abstracta de las características que comparten los lenguajes de programación. Está formado por un conjunto de símbolos y por reglas que determinan cómo estos símbolos pueden combinarse para formar cadenas válidas dentro del mismo lenguaje. El conjunto de todas las cadenas que cumplen con estas reglas constituye el lenguaje formal (Linz & Rodger, 2022).

En mi caso, el lenguaje que escogí de las opciones disponibles, y del que estaré analizando sus reglas, fue "Chakobsa" una lengua ficticia utilizada principalmente por los "Freman" en "Dune". Este universo fue introducido originalmente en las novelas escritas por Frank Herbert y más tarde fue adaptado al cine. En ambas representaciones, tanto en los libros como en sus adaptaciones cinematográficas, se utilizan diversas palabras pertenecientes a este idioma (Herbert, 1965). 
En Dune: Parte Dos el idioma Chakobsa es especialmente utilizado con frecuencia y tiene una estructura gramatical definida. Este lenguaje emplea declinaciones, de manera similar al latín, lo que provoca que los sustantivos cambien ligeramente su forma dependiendo de su función dentro de la oración, ya sea como sujeto u objeto. La lengua cuenta con aproximadamente 700 palabras de vocabulario básico, además de otras formadas mediante modificaciones de las existentes. En las novelas de Frank Herbert, los Fremen presentan varias similitudes con los pueblos beduinos, y por esta razón el idioma tiene ciertas influencias del árabe tanto en su sonido como en algunos de sus elementos lingüísticos. Herbert utilizó estas características para sugerir una conexión entre el mundo actual y el universo de su historia, el cual esta ambientado aproximadamente veinte mil años en el futuro (Tracy, 2024).

Para este proyecto se trabajará con cinco palabras específicas provenientes de este sistema lingüístico, las cuales servirán como base para la construcción del autómata y expresión regular. Estas palabras son las siguientes:

- misr
- mu'addib
- muad'dib
- mudir
- mushtamal

**Alfabeto resultante:**

<img width="260" height="34" alt="image" src="https://github.com/user-attachments/assets/39725b03-8318-431c-ab27-165805cda941" />


## Modelos 
### DFA

En computación existen diferentes tipos de autómatas, cada uno con características que los hacen especiales, sin embargo en esta ocasión nos enfocaremos solamente en el Deterministic Finite Automata (DFA) o en español Autómata Finito Determinista (AFD).
De acuerdo con Hopcroft, Motwani y Ullman (2008),un autómata finito determinista es un modelo matemático utilizado para reconocer lenguajes formales cuya propiedad más importante es que, tras leer una secuencia de símbolos de entrada, el sistema solo puede encontrarse en un único estado, se denomina como determinista porque, para cada símbolo que es recibido, existe solamente una única transición posible hacia el siguiente estado.

Formalmente, un DFA consta de los siguientes 5 elementos:

<img width="200" height="60" alt="image" src="https://github.com/user-attachments/assets/522d6d07-e08b-4f08-bcc0-1cb5e1cba83a" />



- **Conjunto de estados (*Q*):** representa el conjunto finito de estados del autómata, cada uno describe una posible situación en la que puede encontrarse el autómata mientras procesa la cadena de entrada.
- **Alfabeto de entrada (Σ):** representa el conjunto de símbolos de entrada que el autómata puede leer, en otras palabras son los símbolos que forman el alfabeto del lenguaje que el autómata reconocerá.
- **Función de transición (δ):** determina cómo cambia el autómata de un estado a otro al leer un símbolo de entrada.

  <img width="110" height="45" alt="image" src="https://github.com/user-attachments/assets/7a885c90-9f8e-437e-95d9-ab55f2608c42" />

  - *q*: estado
  - *a*: simbolo de entrada

  Esto significa que:

  - si el autómata se encuentra en el estado *q*
  - leerá el simbolo *a*
  entonces se moverá al estado *p*.


- **Estado inicial (*q₀*):** este es el estado en el que el autómata comienza antes de procesar cualquier símbolo de entrada y aquí se inicia el procesamiento de cualquier cadena.
- **Conjunto de estados de aceptación (*F*):** estos estados indican que la cadena de entrada es aceptada por el autómata, esto quiere decir que si al terminar de leer toda la cadena el autómata se encuentra en uno de estos estados, la cadena pertenece al lenguaje.

En pocas palabras:

"***A*** es el nombre del AFD, ***Q*** es su conjunto de estados, ***Σ*** son los símbolos de entrada,***δ*** es la función de transición, ***qo*** es el estado inicial y ***F*** es el conjunto de estados finales"(Hopcroft, Motwani, & Ullman, 2008).

#### Construcción de mi DFA

Para comenzar con el modelado del autómata, primero analicé las palabras asignadas con el objetivo de identificar los prefijos comunes entre ellas. A partir de este análisis se observó que varias de las palabras compartían las letras iniciales m y u, como se muestra a continuación:

- **mu**'addib
- **mu**ad'dib
- **mu**dir
- **mu**shtamal
- misr

Debido a que la palabra misr no comparte este mismo prefijo, decidí dejarla de lado y enfocarme primero en las palabras que sí coincidían en sus caracteres iniciales. Posteriormente, tomé la palabra con mayor número de caracteres que compartiera este prefijo como base para establecer el camino principal del autómata. En este caso, la palabra seleccionada fue mushtamal, la cual cuenta con un total de nueve caracteres. A partir de este camino inicial se comenzó a diseñar el autómata, generando posteriormente las distintas ramas necesarias conforme las demás palabras empezaban a diferenciarse en sus caracteres, hasta completar la representación de las cinco palabras que me fuerron asignadas.Finalmente, se modelaron las transiciones correspondientes a todos aquellos caracteres que no conducían a la formación de alguna de las palabras válidas, dirigiéndolos hacia un estado trampa, cuyo propósito es indica el rechazo de la cadena; este comportamiento puede entenderse como una configuración muerta, es decir, una situación en la que el autómata deja de avanzar al no existir una transición válida para continuar procesando la cadena (Linz & Rodger, 2022).Desde mi punto de vista esta fue la etapa que requirió más tiempo y especial cuidado, ya que fue necesario verificar detalladamente que cada estado incluyera todos los símbolos que el lenguaje no debía aceptar, evitando al mismo tiempo redirigir caracteres que sí formaban parte de las transiciones válidas.

Al finalizar este proceso, el autómata resultante fue el siguiente:


<img width="2688" height="1038" alt="DFA drawio" src="https://github.com/user-attachments/assets/1319cdfd-98f6-4fd4-bca5-476c74788e35" />

**Tabla de transiciones:**


![DFA drawio 2](https://github.com/user-attachments/assets/00c8155f-ecf3-44d8-9237-45291b9a5948)

### Expresión Regular
Una vez completado el diseño del autómata, se puede proceder al siguiente paso de esta evidencia, el cual consiste en describir el mismo lenguaje utilizando una representación alternativa: las expresiones regulares.

Las expresiones regulares son una herramienta utilizada para definir patrones dentro de un conjunto de cadenas. Estas tienen aplicaciones importantes en áreas como la búsqueda de texto o el desarrollo de compiladores, además, tienen una relación directa con los autómatas finitos, ya que ambos permiten describir exactamente el mismo tipo de lenguajes, conocidos como lenguajes regulares, sin embargo, a diferencia de los autómatas, las expresiones regulares permiten especificar de manera declarativa las cadenas que se desean aceptar, por lo que son ampliamente utilizadas como mecanismo de entrada en diversos sistemas que procesan de texto (Hopcroft, Motwani, & Ullman, 2008).

Tabla proporcionada en clase, la cual fue usada como base para conocer la sintaxis:

<img width="500" height="image" alt="image" src="https://github.com/user-attachments/assets/0364f2b2-40af-48dd-948e-8ef0d3fb2f4e" />


Para construir la expresión regular seguí un proceso similar al utilizado durante el diseño del autómata, identificando primero los caracteres comunes entre las palabras del lenguaje, en este caso observé que todas las palabras comienzan con el carácter m, por lo que la expresión regular inicia con este símbolo. Posteriormente, se identificaron dos posibles continuaciones después de este primer carácter: la palabra misr y las palabras que comienzan con mu. Para poder representar estas dos posibilidades se utilizó el operador de ***OR ( | )***, el cual permite indicar diferentes opciones dentro de una expresión regular. Para las palabras que comienzan con mu, se agruparon las diferentes terminaciones posibles: 'addib, ad'dib, dir y shtamal. Estas opciones se incluyeron dentro de un mismo grupo utilizando nuevamente el operador ***"|"***. Para finalizar, añadí los símbolos ***^*** al inicio de la expresión y ***$*** al final. El primero indica que la cadena debe comenzar con el patrón especificado (m), mientras que el segundo señala que la cadena debe terminar en ese punto, es decir, finaliza en el momento que detecte la última letra de cada palabra aceptada, sin continuar leyendo más allá. Esto permitió garantizar que únicamente se acepten las cinco palabras asignadas y no cadenas similares, como misrr, que contiene una letra adicional al final.

De esta manera se obtuvo la expresión regular:

**^m(isr | u('addib | ad'dib | dir | shtamal))$**

Al probarla con una página web de expresiones regulares proporcionada por nuestro profesor, comprobamos que en efecto solo recibe estas 5 palabras y rechaza todas las demás:

<img width="96" height="658" alt="image" src="https://github.com/user-attachments/assets/98e7130b-e71a-4a47-a064-04e0e597d76d" />

## Implementación
Para la implementación del análisis léxico decidí utilizar el DFA, cuyo funcionamiento fue comprobado mediante un programa escrito en Prolog, el cual es el lenguaje de programación que se ha utilizado a lo largo del curso. A través de este programa se implementaron las transiciones del autómata y se realizaron pruebas con diferentes cadenas para verificar que el DFA aceptara únicamente las palabras válidas del lenguaje y rechazara aquellas que no pertenecieran a él.

Para crear este progrma se usó como base la siguiente estructura vista previamente en clase:

Esta código proporciona la forma general de representar un autómata finito en Prolog, definiendo las transiciones con "move", los estados de aceptación con "accepting_state" y un predicado principal que se encarga de recorrer la lista de símbolos de entrada, simulando así el comportamiento del autómata.

<img width="215" height="177" alt="Screenshot 2026-03-11 at 7 17 59 p m" src="https://github.com/user-attachments/assets/01b41520-68c0-480e-854c-bf6b0b4b7422" />

<img width="392" height="224" alt="Screenshot 2026-03-11 at 7 18 07 p m" src="https://github.com/user-attachments/assets/59c94053-8c39-4ec4-9a26-70e66090d013" />

Gracias a esto, la creación del código fue relativamente fácil, solo quedó que adaptarlo a mi autómata, lo cual resultó un poco laborioso debido a la gran cantidad de transiciones presentes, tomando en consideración que en Prolog cada transición debe declararse de forma individual.

Para ejecutar el programa se deben seguir las siguientes instrucciones:

- **1. Abrir SWI-Prolog**
  - Abre SWI-Prolog en la computadora.

- **2. Cargar el archivo**
  - Una vez abierto Prolog, se debe cargar el archivo que contiene la implementación del autómata:
    - ['Evidencia 1 - DFA Dune'].
  - Si el archivo se carga correctamente, Prolog mostrará 'true'.
- **3. Ejecutar la función**
  - Después de cargar el archivo, el autómata se prueba utilizando el predicado:
    - parseDFA([tu_input]).
  - Por ejemplo:
    - parseDFA([m,u,s,h,t,a,m,a,l]).
  - **Nota:**
    - En el caso del símbolo **' (comilla simple)**, es necesario escribirlo de la siguiente manera: <img width="28" height="30" alt="image" src="https://github.com/user-attachments/assets/311af125-e351-4601-8f2d-29fc721923fb" />

    - Por ejemplo, para poder probar una cadena que contenga este símbolo se debe escribir de esta forma: <img width="300" height="100" alt="image" src="https://github.com/user-attachments/assets/5a19f006-39b2-49b1-b507-68031e78f6f7" />


Cada elemento de la lista representará un carácter de la cadena que se quiere analizar. El programa los evaluará siguiendo las transiciones ya definidas en el autómata y decidirá si pertenece o no al lenguaje.
Una vez que concluya el análisis, si es aceptado se mostrará:

  parseDFA([m,u,d,i,r]).

    Accepted
    true.

o en caso de rechazo:

  parseDFA([m,u,s,h,t,a,m,a]).

    Rejected
    true.

## Pruebas
Estas son las palabras que probaremos en el archivo "test_automataDune.pl" :

<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/1c5976ec-4329-437b-a790-45e737acd72a" />

<img width="600" height="1200" alt="image" src="https://github.com/user-attachments/assets/0cf7f78e-427f-4363-9b51-37fbecac1e94" />

**Como ejecutar el programa**

Para realizar el script de pruebas se utilizó SWI-Prolog y son las mismas que las presentadas en las tablas anteriores.

Los pasos para correr el programa son los siguientes:

Una vez cargado el programa principal, como se explicó en la sección anterior, se puede ejecutar el script.

**1. Cargar el archivo de pruebas:**
  [test_automataDune.pl]
**2. Ejecutar el script de pruebas:**
  Escribir: *run_dune_tests.*
  Este comando ejecutará el script con las múltiples pruebas utilizando cadenas aceptadas y rechazadas.

El programa mostrará en la consola si cada cadena es Accepted o Rejected, lo cual nos permite verificar que el autómata funciona reconociendo correctamente el lenguaje definido.

## Análisis

Esta última parte de la evidencia se enfocará en analizar el DFA construido y así poder determinar su complejidad temporal asintótica, para después compararla contra soluciones alternativas explicando sus diferencias.

#### Complejidad temporal asintótica

Para definir la complejidad de mi autómata me basaré en la Jerarquía de Chomsky.

Linz y Rodger (2022) explican en su libro "An Introduction to Formal Languages and Automata" que Noam Chomsky, considerado uno de los fundadores de la teoría de lenguajes formales, propuso una clasificación inicial de los lenguajes en cuatro tipos, numerados del 0 al 3, terminología que se ha mantenido a lo largo del tiempo y sigue utilizándose con frecuencia.
En su jerrarquía los lenguajes de tipo 0 son aquellos generados por gramáticas irrestrictas, también conocidos como lenguajes recursivamente enumerables, el tipo 1 corresponde a los lenguajes sensibles al contexto, el tipo 2 a los lenguajes libres de contexto y el tipo 3 a los lenguajes regulares.

<img src="https://github.com/user-attachments/assets/3b92a8bd-596d-4b72-86ae-9a72c354182a" width="400">

Figura 1. Jerarquía de Chomsky.
Tomado de "An Introduction to Formal Languages and Automata" (Linz & Rodger, 2022).

Ahora que ya conocemos que es esta jerarquía y el como funciona la clasificación, ya nos es posible ubicar mi DFA, ya que, de acuerdo con Linz y Rodger (2022), “El adjetivo ‘determinista’ significa que el autómata tiene una y solo una opción en cualquier momento. Utilizamos los DFA para definir un cierto tipo de lenguaje, llamado lenguaje regular”. 

Esta afirmación permite concluir que la solución propuesta, un Autómata Finito Determinista, clasifica como un lenguaje regular, y por tanto pertenece al nivel más básico de la jerarquía de Chomsky, el 3 *(LREG)*.

Ahora para la notación *Big O* tenemos esta cita que nos lo explica:

"Todo lenguaje regular puede ser reconocido por un autómata finito determinista en un tiempo proporcional a la longitud de la entrada. Por lo tanto:

<img width="170" height="30" alt="image" src="https://github.com/user-attachments/assets/4e78a2d6-55e2-4368-ae39-cb6a3bfa17e2" /> "

(Linz & Rodger, 2022).

Esta notación significa que el conjunto de los *lenguajes regulares* está dentro del conjunto de problemas que pueden resolverse en *tiempo determinista lineal*.


A lo que se refiere esta cita es que cualquier lenguaje regular, como el utilizado en este trabajo, puede ser procesado por un autómata finito determinista (DFA) en un tiempo que depende directamente de la longitud de la cadena de entrada, es decir, si la cadena tiene una longitud de 𝑛, el autómata realiza un número de operaciones proporcional a 𝑛, ya que procesa cada símbolo exactamente una vez y en cada paso solo existe una transición posible.

Por lo tanto, podemos decir que la complejidad temporal asintótica del autómata construido es 𝑂(𝑛).

#### Comparación y diferencias

La solución que propuse utiliza un autómata finito determinista (DFA), el cual, como mencionamos anteriormente, presenta una complejidad temporal de 𝑂(𝑛), porque procesa la cadena de entrada símbolo por símbolo realizando una única transición en cada paso.

En comparación con otras alternativas, como los autómatas finitos no deterministas (NFA), los cuales implican que el autómata puede tener varias opciones de transición en lugar de una sola, refiriendose a que en vez de establecer un movimiento único en cada situación, se permite un conjunto de posibles movimientos. De manera formal, esto se logra definiendo la función de transición de forma que su resultado sea un conjunto de estados posibles (Linz & Rodger, 2022). Ambos modelos mencionados reconocen lenguajes regulares, por lo cual comparten la misma complejidad asintótica, sin embargo, el DFA resulta más eficiente a la hora de implementarlo debido a que no requiere considerar múltiples transiciones posibles para un mismo símbolo, sino que solo tiene un único camino de ejecución.

Aparte de los ya mencionados (NFA y DFA) también existen todos los demás lenguajes en la jerarquia de Chomsky como se observa en la siguiente tabla:

<img width="700" height="image" alt="image" src="https://github.com/user-attachments/assets/26d49ee2-6dcd-438d-b3f2-d08b98dc9f50" />

En contraste, los lenguajes independientes del contexto (tipo 2), que son reconocidos por autómatas de pila, requieren algoritmos más complejos, 𝑂(𝑛^3),lo que implica un mayor costo computacional y para los niveles superiores, como los lenguajes sensibles al contexto (tipo 1) y los recursivamente enumerables (tipo 0), los problemas asociados pueden requerir tiempo exponencial o incluso ser indecidibles, lo que los hace considerablemente menos eficientes.





























































## Referencias 
- Linz, P., & Rodger, S. H. (2022). An introduction to formal languages and automata. Jones & Bartlett Learning.
- Hopcroft, J. E., Motwani, R., & Ullman, J. D. (2008). Teoría de autómatas, lenguajes y computación (3.ª ed.). Pearson Addison-Wesley.
- Herbert, F. (2005). Dune. Ace Books.
- Tracy, M. (2024, abril 21). Chakobsa: Inventan idioma único para el desierto de “Dune”. La Prensa. https://www.laprensa.hn/new-york-times-international-weekly/chakobsa-inventan-idioma-unico-pelicula-dune-HA18811116
