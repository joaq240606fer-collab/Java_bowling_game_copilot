# Documento de requerimientos

## Introduccion 

Se va a simulaR una partida de bolos y el objetivo de este programa es gestionar la targeta de puntuaciones (scoreCard).

---

## motor de gestion de proyecto 

en este caso vamos a utilizar maven 21 ...

El archetype seria : edu.Teamrocket.bowlingame

y necesitara de las siguientes dependencias dentro de su pom:

junit : 5.11.0

org.junit.jupiter : para los casos test 


---


## Convenciones 

el codigo a de disfrutar de multiples casos test que prueben la funcionalidad de todo el codigo del programa atendiendo al principios SOLID , DDD y las estructuras de POO y TDD .


## Requerimientos 

---

### Requerimiento 1

 Como usuario juega un total de 10 turnos por partida <<Frames>> por cada frame el jugador cuenta con hasta 2 intentos para eliminar todos los bolos  <<Pines>>> de no lograr deribar todos los pines su puntuacion pasa a ser la suma de todos los pines derribados en los dos intentos.

---

### Requerimiento 2


 En caso de derriar todos los pines en sus dos intentos esto se denomina <<Spare>> su puntuacion seria de 10 + los puntos logrados en el siguiente lanzamiento.

---

### Requerimiento 3

 Si el usuario derriba todos los pines en el primer intento esto se denomina <<Strike>> y la puntuacion pasa a ser 10 mas la suma de todos los pines de los siguientes dos lanzamientos y el turno termina.

---

### Requerimiento 4


 En caso que en el decimo Frame un Spare o un strike se suman en el mismo turno de 1 a 2 lanzamientos extras respectivamente en caso de los lanzamientos de bonificación derriban todos los bolos, el proceso no se repite:los lanzamientos de bonificación solo se utilizan para calcular la puntuación del frame final.
    La puntuación del juego es la suma de todas las puntuaciones de los frames.

---

### Estas son algunas cosas que el programa no hará:

    No comprobaremos si los lanzamientos son válidos.
    No comprobaremos si el número de lanzamientos y frames es correcto.
    No proporcionaremos puntuaciones para los frames intermedios.


## representacion 

Strikes se representan por el caracter : x

spares se representan por el caracter : /

el resto de puntuaciones entre 1 a 9 pines se representan por enteros

en caso de no conseguir deribar ningun pin se reprenta por - y tiene el valor de 0


---

### Historias de usuario - Tests que deben estar si o si 

**User story:** el ususario siempre logra tirar pines sin Strikes ni Spares 

  pins = "12345123451234512345"
  total = 60

**User story:**  solo tira pines en el primer intento de cada frame y siempre tira 9
   pins = "9-9-9-9-9-9-9-9-9-9-"
   total = 90

**User story:** prueba de partida normal sin strikes ni spares 

    pins = "9-3561368153258-7181"
    total = 82

**User story:** partida con Spares 

    pins = "9-3/613/815/-/8-7/8-"
    total = 121

**User story:** partida con 1 Strike
    pins = "X9-9-9-9-9-9-9-9-9-"
    total = 100

**User story:** partida con 2 Strikes 
    pins = "X9-X9-9-9-9-9-9-9-"
    total = 110

**User story:** partida con 2 Strikes al principio 
    pins = "XX9-9-9-9-9-9-9-9-"
    total = 120

**User story:** partida con 3 Strikes al principio 
    pins = "XXX9-9-9-9-9-9-9-"
    total = 141

**User story:** partida con extra roll
    pins = "9-3/613/815/-/8-7/8/8"
    total = 131

**User story:** partida con extra roll
    pins = "5/5/5/5/5/5/5/5/5/5/5"
    total = 150

**User story:** extra roll + 2 Strikes
    pins = "9-9-9-9-9-9-9-9-9-XXX"
    total = 111

**User story:**extra roll + 1 Strikes
    pins = "8/549-XX5/53639/9/X"
    total = 149

**User story:** Spare en extra roll
    pins = "X5/X5/XX5/--5/X5/"
    total = 175

**User story:** todo Strikes
    pins = "XXXXXXXXXXXX"
    total = 300


# Para DDD


Mi enfoque no es 100 % formal, sino que se centra en el DDD (diseño basado en el dominio); es decir, el autómata facilita la expresión de la lógica (y el algoritmo) del problema en una notación bien definida, también en lo que respecta al vocabulario del juego de bolos.

Un autómata finito es una colección de quintuples (Q, ∑, δ, q0, F), donde:

Q: conjunto finito de estados  
∑: conjunto finito de símbolos de entrada  
q0: estado inicial   
F: estado final  
δ: función de transición
λ: función de salida
