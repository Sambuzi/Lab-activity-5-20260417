# Lab Activity 5 - Controller NN con ARGoS e Algoritmo Genetico

Questo progetto allena un controller neurale (Lua) per robot foot-bot in ARGoS usando un algoritmo genetico scritto in Python.

Obiettivo: massimizzare la fitness, definita come vicinanza alla sorgente luminosa.

## Contenuto del progetto

- ga.py: algoritmo genetico per ottimizzare i pesi della rete neurale.
- controller-nn.lua: controller usato durante la valutazione, legge il genoma da variabile ambiente GENOME.
- evaluate-controller-nn.argos: scenario ARGoS per valutare un individuo.
- test-controller-nn.lua: controller con genoma fisso per test rapidi.
- test-controller-nn.argos: scenario ARGoS visuale con piu robot.
- nn.lua: implementazione rete neurale usata dai controller Lua.
- test/: piccoli test di integrazione per passaggio parametri.

## Prerequisiti

- ARGoS3 installato e disponibile da terminale (comando argos3).
- Python 3.

## Come eseguire

### 1) Test rapido ARGoS controller

Comando:

argos3 -c test-controller-nn.argos

Serve per verificare che ambiente ARGoS e controller Lua funzionino.

### 2) Test passaggio GENOME via variabile ambiente

Dalla cartella test:

python3 test-params.py

Output atteso: un valore FITNESS stampato su stdout (tipicamente in [0,1]).

### 3) Avvio training con algoritmo genetico

Dalla root del progetto:

python3 ga.py

Il training valuta ogni individuo con:

argos3 -c evaluate-controller-nn.argos

Per ogni generazione vengono stampati:

- Best fitness
- Best solution
- Elite fitnesses

## Note su algoritmo genetico

Parametri principali in ga.py:

- GENOME_LENGTH = 50
- POP_SIZE = 20
- ELITE_SIZE = 5
- GENERATIONS = 10
- MUTATION_RATE = 0.1
- CX_RATE = 1
- MUTATION_INTENSITY = 1
- N_EVAL = 3

Meccanismi implementati:

- Selezione proporzionale (roulette wheel)
- Crossover lineare
- Mutazione gaussiana con clipping in [-1, 1]
- Elitismo: i migliori ELITE_SIZE individui vengono copiati direttamente nella nuova popolazione



