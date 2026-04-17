# Práctica 6: Conecta 4 - IA Q-Learning

Esta práctica implementa un agente de aprendizaje por refuerzo para jugar Conecta 4.

(Este proyecto fue generado con la ayuda de una IA).

### Reglas del Juego
1. El objetivo es alinear **4 fichas** (Horizontal, Vertical o Diagonal).
2. Se juega en un tablero de **6 filas x 7 columnas**.
3. Las fichas caen hasta la posición más baja disponible.

### Cómo ejecutar
1. Entrenar al agente:
   -Ejecute el archivo `main.py`
   -Escriba 1 (la opción para entrenar a la IA)
   -Escriba la cantidad de partidas que desee (ejemplo 10,000)
   -Eliga una cantidad de epsilon para jugar con su comportamiento (puede ser 0.1 o 0.03 hasta 1)
2. Jugar contra la IA:
   -Ejecuta el archivo `main.py `
   -Ecriba 2 (opción para jugar contra la IA)
   -Diviertase

## Estructura de la practica
Practica-6/

├── main.py              # Orquestador del juego y visualización (Matplotlib)

├── agente.py            # Lógica de Q-Learning (Ecuación de Bellman)

├── logica_juego.py      # Reglas del juego y gestión del tablero

├── q_table.pkl          # Archivo de memoria (se genera al entrenar)

└── README.md            # Documentación e instrucciones

## Explicación de cada archivo
1. main.py
Coordina los dos modos de ejecución:
Entrenamiento: Ejecuta miles de partidas a alta velocidad sin gráficos. Aquí el agente juega contra un rival aleatorio para recibir "castigos" (recompensa negativa) si pierde o "premios" (recompensa positiva) si gana.
Juego: Activa matplotlib para que tú puedas interactuar.
2. agente.py
Aquí reside la Ecuación de Bellman.
Q-Table: Es un diccionario donde la "llave" es el estado del tablero y el "valor" es una lista de 7 números (uno por columna).
Exploración vs. Explotación: Mediante Epsilon (ϵ), el agente decide si probar un movimiento al azar para aprender (exploración) o usar el mejor movimiento que ya conoce (explotación).
3. logica_juego.py
Su función principal es gestionar la matriz de $6 \times 7$.
get_valid_moves: Crucial para evitar que el código intente meter fichas en columnas llenas.
check_winner: Escanea el tablero en 4 direcciones. Es el "árbitro" que detiene el entrenamiento cuando alguien gana.

## Uso del epsilon y Ecuación De Bellman
 Epsilon:
 El Epsilon es el parámetro que decide si el agente se comporta como un explorador o como un experto.
 Exploración: El agente elige un movimiento al azar. Es vital al principio para descubrir que alinear 4 fichas da puntos. Sin esto, la IA nunca intentaría jugadas nuevas.
 Explotación: El agente elige el movimiento que su memoria (Q-table) dice que es el mejor. Es cuando la IA aplica lo que ya aprendió para ganar.

Ecuación de Bellman: 
Es la fórmula matemática que actualiza la memoria del agente. No solo premia el último movimiento que ganó el juego, sino que reparte esa "felicidad" hacia atrás, a los movimientos que permitieron llegar ahí.
En tu código, se ve así:
Q(s,a)=Q(s,a)+α[r+γmaxQ(s 
′
 ,a 
′
 )−Q(s,a)]
¿Qué significa cada parte?

Q(s,a): El valor actual de hacer el movimiento a en el tablero s.

α (Alpha): Qué tan rápido aprende (tasa de aprendizaje).

r (Recompensa): Los +100 por ganar o −100 por perder.

γmaxQ(s 
′
 ,a 
′
 ): El valor del mejor movimiento posible en el siguiente turno. Esto es lo que permite que el agente "anticipe" el futuro.

3
