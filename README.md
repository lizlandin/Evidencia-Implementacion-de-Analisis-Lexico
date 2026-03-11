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

## DFA

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

### Construcción de mi DFA

Para comenzar con el modelado del autómata, primero analicé las palabras asignadas con el objetivo de identificar los prefijos comunes entre ellas. A partir de este análisis se observó que varias de las palabras compartían las letras iniciales m y u, como se muestra a continuación:

- **mu**'addib
- **mu**ad'dib
- **mu**dir
- **mu**shtamal
- misr

Debido a que la palabra misr no comparte este mismo prefijo, decidí dejarla de lado y enfocarme primero en las palabras que sí coincidían en sus caracteres iniciales. Posteriormente, tomé la palabra con mayor número de caracteres que compartiera este prefijo como base para establecer el camino principal del autómata. En este caso, la palabra seleccionada fue mushtamal, la cual cuenta con un total de nueve caracteres. A partir de este camino inicial se comenzó a diseñar el autómata, generando posteriormente las distintas ramas necesarias conforme las demás palabras empezaban a diferenciarse en sus caracteres, hasta completar la representación de las cinco palabras que me fuerron asignadas.Finalmente, se modelaron las transiciones correspondientes a todos aquellos caracteres que no conducían a la formación de alguna de las palabras válidas, dirigiéndolos hacia un estado trampa, cuyo propósito es indica el rechazo de la cadena; este comportamiento puede entenderse como una configuración muerta, es decir, una situación en la que el autómata deja de avanzar al no existir una transición válida para continuar procesando la cadena (Linz & Rodger, 2022).Desde mi punto de vista esta fue la etapa que requirió más tiempo y especial cuidado, ya que fue necesario verificar detalladamente que cada estado incluyera todos los símbolos que el lenguaje no debía aceptar, evitando al mismo tiempo redirigir caracteres que sí formaban parte de las transiciones válidas.

Al finalizar este proceso, el autómata resultante fue el siguiente:


<img width="2688" height="1038" alt="DFA drawio" src="https://github.com/user-attachments/assets/1319cdfd-98f6-4fd4-bca5-476c74788e35" />




























































## Referencias 
- Linz, P., & Rodger, S. H. (2022). An introduction to formal languages and automata. Jones & Bartlett Learning.
- Hopcroft, J. E., Motwani, R., & Ullman, J. D. (2008). Teoría de autómatas, lenguajes y computación (3.ª ed.). Pearson Addison-Wesley.
- Herbert, F. (2005). Dune. Ace Books.
- Tracy, M. (2024, abril 21). Chakobsa: Inventan idioma único para el desierto de “Dune”. La Prensa. https://www.laprensa.hn/new-york-times-international-weekly/chakobsa-inventan-idioma-unico-pelicula-dune-HA18811116
