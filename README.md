# Yahtzee
# Simulacion de Yatzhee con Metodo de Montecarlo

## Descripcion del Proyecto

Este proyecto implementa una simulacion completa del juego de Yatzhee clasico para dos jugadores, utilizando el metodo de Montecarlo para la toma de decisiones estrategicas. El programa decide que dados conservar en cada relanzamiento simulando multiples futuros posibles y eligiendo la opcion con mayor valor esperado.

## Requerimientos del Sistema

- Python 3.7 o superior
- Bibliotecas necesarias:
  - matplotlib (para graficos)
  - random (incluida en Python)
  - collections (incluida en Python)
  - dataclasses (incluida en Python)
  - functools (incluida en Python)

## Instalacion

1. Clonar el repositorio:
bash
git clone https://github.com/tu-usuario/yatzhee-montecarlo.git
cd yatzhee-montecarlo


2. Instalar dependencias:
bash
pip install matplotlib


## Como ejecutar

bash
python yatzhee_montecarlo.py


Al ejecutar, aparecera un menu con dos opciones:

- Opcion 1: Simular una sola partida (graficos detallados por categoria)
- Opcion 2: Simular multiples partidas (analisis estadistico y convergencia)

## Reglas del Juego Implementadas

- Dos jugadores alternan turnos
- 13 rondas por jugador (una por cada categoria)
- 3 lanzamientos maximos por turno
- 5 dados de 6 caras cada uno

### Categorias de Puntuacion

| Categoria | Descripcion | Puntaje |
|-----------|-------------|---------|
| Unos | Suma de dados con valor 1 | Variable |
| Dos | Suma de dados con valor 2 | Variable |
| Tres | Suma de dados con valor 3 | Variable |
| Cuatros | Suma de dados con valor 4 | Variable |
| Cincos | Suma de dados con valor 5 | Variable |
| Seis | Suma de dados con valor 6 | Variable |
| Trio | Al menos 3 dados iguales | Suma total |
| Cuarteto | Al menos 4 dados iguales | Suma total |
| Full House | 3 iguales + 2 iguales | 25 puntos |
| Escalera Chica | 4 dados consecutivos | 30 puntos |
| Escalera Grande | 5 dados consecutivos | 40 puntos |
| Yatzhee | 5 dados iguales | 50 puntos |
| Chance | Cualquier combinacion | Suma total |

## Metodo de Montecarlo Implementado

El corazon de la simulacion esta en la funcion valor_esperado_cached. Para decidir que dados conservar:

1. Se generan todas las mascaras de bloqueo posibles (17 combinaciones utiles)
2. Para cada mascara, se simulan N futuros lanzamientos (configurable, default 80)
3. Se calcula el puntaje promedio de esas simulaciones
4. Se elige la mascara con mayor valor esperado

Esto permite al jugador "mirar al futuro" mediante simulaciones aleatorias, sin conocer realmente el resultado.

### Optimizaciones implementadas

- Reduccion de mascaras de 32 a 17 (solo combinaciones logicas)
- Sistema de cache con lru_cache para evitar recalculos
- Simulaciones ajustables por mascara (balance entre velocidad y precision)

## Estructura del Codigo

yatzhee_montecarlo.py
├── Configuracion (CONFIG)
├── Funciones de dados (lanzar, secuencias, puntuacion)
├── Clases (Jugador, Estadisticas, Partida)
├── Nucleo Montecarlo (mascaras, valor esperado, cache)
├── Logica del juego (turnos, partida)
├── Visualizacion (graficas individuales y multiples)
└── Menu principal


## Resultados Esperados

Al simular multiples partidas (ej: 1000), se observa:

- Porcentaje de victorias cercano a 50% para cada jugador
- Puntajes promedio simetricos
- Distribucion uniforme de las caras de los dados (aproximadamente 16.67% cada una)
- Convergencia de los promedios al aumentar el numero de partidas (ley de grandes numeros)

## Ejemplo de Salida

========================================
SIMULADOR DE YATZHEE CON MONTECARLO
========================================
1. Simular una sola partida (con graficos detallados)
2. Simular multiples partidas (analisis estadistico)

Selecciona una opcion (1 o 2): 2
Cuantas partidas quieres simular? (ej: 1000, 5000, 10000): 1000

Simulando 1000 partidas...
Completadas 1000 de 1000 partidas

==================================================
RESULTADOS DE SIMULACION MULTIPLE
==================================================
Partidas simuladas: 1000
Victorias Jugador 1: 495 (49.50%)
Victorias Jugador 2: 505 (50.50%)
Empates: 0 (0.00%)
Puntaje promedio Jugador 1: 131.25
Puntaje promedio Jugador 2: 130.98


## Graficos Generados

### Una sola partida (Opcion 1)

- Grafico de barras: Puntuaciones por categoria comparando ambos jugadores
- Grafico de barras: Distribucion de caras de los dados vs teorico 16.67%
- Grafico de lineas: Evolucion del puntaje acumulado ronda por ronda

### Multiples partidas (Opcion 2)

- Histograma: Distribucion de puntajes de ambos jugadores
- Histograma: Distribucion de la diferencia (J1 - J2)
- Grafico de lineas: Convergencia del puntaje promedio
- Grafico de lineas: Convergencia del porcentaje de victorias al 50%

## Configuracion Personalizable

En el diccionario CONFIG al inicio del codigo:

python
CONFIG = {
    "sims_por_mascara": 80,   # Simulaciones por decision (menor = mas rapido)
    "semilla": 42             # Semilla fija para reproducibilidad (None para aleatorio)
}


### Ajustes recomendados

| Simulaciones por mascara | Velocidad | Precision |
|--------------------------|-----------|-----------|
| 30 | Muy rapida | Aceptable |
| 80 | Rapida (default) | Buena |
| 150 | Normal | Muy buena |
| 300 | Lenta | Excelente |

## Limitaciones Conocidas

- La estrategia de decision es simple (maximizar valor esperado inmediato)
- No implementa estrategias avanzadas como priorizar Yatzhee sobre otras categorias
- El tiempo de simulacion crece linealmente con el numero de partidas
- Para 10,000 partidas puede tomar varios minutos

## Mejoras Futuras Posibles

- Implementar paralelizacion para simular partidas en multiprocesador
- Agregar estrategia de priorizacion de Yatzhee
- Exportar resultados a CSV para analisis externo
- Interfaz grafica para visualizar el juego en tiempo real

## Autor

[Tu Nombre Completo]
[Tu Correo Electronico]
[Fecha de entrega]

## Asignatura

Simulacion - IUD
Semestre 5

## Licencia

Proyecto academico. Uso permitido para fines educativos.
