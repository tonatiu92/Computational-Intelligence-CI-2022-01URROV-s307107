# Lab 3: Nim Game

## Task 3.1: Rule based system

I choosed to define 4 type of strategy two according the state of the nim, the second according the action of the opponent

### Action Strategies
- The fisrt strategy is according the quantity of remaining quantity of row. If this quantity is paired, we doesn't want to remove the row, if it is unpaired, we want to remove ir
- The second strategy is according the quantity of remaining objects. If the number is paired, we want to keep a paired quantity, if it is unpaired, we want a paired quantity of nim
### Reaction Strategies
- The player will try to play in another domain than the opponent. If opponent plays on the shortest rows, he will play on the longest and vice versa
- The player will try  to play an opposite type of quantity, if opponent plays pair, player plays unpair
### Simple Strategies
- Here we will use some simple strategies as longest or shortest row, always 1 nim etc...
### Random
- As any player, sometime we will play randomly
### Results
- For this task, I implement a balanced weight between each params (this wheight is the beggining of the task 3.2 that I explain below) 
- I played against random player and get a result of 65% of success more or less
- I played against Expert System player and get a result of 18% of success more or less

## Task 3.2: Evolved 

### Parametrization
Too perform an evolved algorithm and improve my strategy, I decided to give a weight for each strategy. The **sum** should be equal to **1**.
Example of parameters: **[0.2,0.16,0.16,0.16,0.16,0.16]**

### Genetical Algorithm

#### Individuals
An individual is an array with all weights
#### Fitness
The average of victory agains random player for a nim size from 1 
to 20
```
NUM_MATCHES = 50
NIM_SIZE = 20
def fitness(genome: list):
    evolution = []
    for i in range(NIM_SIZE):
        winner = []
        for m in range(NUM_MATCHES):
            nim = Nim(i)
            p1 = RuleBased("classic_rules",genome)
            p2 = RuleBased("pure_random",[0,0,0,0,0,1])
            game = Game(p1,p2, i)
            winner.append(game.run())
        evolution.append(op.countOf(winner,"classic_rules")/len(winner))
        #print(f'Percentage of victory against pure random:{op.countOf(winner,"classic_rules")/len(winner)} with nim size {i}')
    return np.mean(evolution)
```
#### Cross-Over
Cross over with 3 parents producing one descendant
```
def cross_over(g1, g2, g3):
    cut = random.randint(0, 3)
    cut2 = random.randint(cut,5)
    return generate_weights(g1.tolist()[:cut] + g2.tolist()[cut:cut2] + g3.tolist()[cut2:])
```
#### Mutation
It will be a permutation of two "gene" (weight)
```
def mutation(g:list):
    point1 = random.randint(0, len(g) - 1)
    point2 = None
    while not point2:
        test = random.randint(0, len(g) - 1)
        if test != point1:
            point2 = test
    tmp = g[point1]
    g[point1] = g[point2]
    g[point2] = tmp
    return g
```
#### Evolution
See lab2

#### Results
We manage to improve to 83% of victory against the random adversary


