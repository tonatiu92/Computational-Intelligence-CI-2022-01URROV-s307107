# Lab2 - Evolutionary Algorithm

# Sources

- Computational Intelligence classes 
- https://github.com/squillero/computational-intelligence/blob/master/2022-23/one-max.ipynb

# Methodology

- I use a Genetical algotithm

## Parameters

- Population Size:
    - N in [5,10,20,50,100]: popsize == N*N
    - N in [500,1000]: popsize == 5000 
- Offspring Size:
    - N in [5,10,20,50,100]: offsize == N*10
    - N in [500,1000]: offsize == 1200 
- Number of Generation:
    - N in [5,10,20,50,100]: numgen == N*100
    - N in [500,1000]: numgen == 1000

**Obs**: I tried with several parameters combination, in all cases I observed an improvment until a certain point. After these boundaries, the performances were decreasing.  

## Population Initialisation:

### Fitness
- The fitness evaluate how fit a given solution is in solving the set covering problem. Set covering problem looks to minimize the size of the final solution to get all number in range(N).
- ```sum(len(_) for _ in genome)```

### Feasibility

- Our problem provide us a lot of an infeasible solution therefore it is better to take this values. 
- As the heuristic repair could be dangerous, I will not use it
- I will give a penalty to them. As set covering problem is a minminization problem, we will try to maximize this values
- According, I will provide a factor of 100 * N.

### Generation

- I take a sample of solutions inside our initial set search

## Evolution

### Tournament
- The set covering problem is a minimisation problem, therefore we will try to minimize it. As we are looking to the values closest to zero, we can use the absolute value of the fitness
- ```min(random.choices(population, k=tournament_size), key=lambda i: abs(i.fitness))```
### Mutation
Three types of mutation:
- if len(genome) < Len(goal) ==> insertion of random array from the initial set
- if len(genome) > len(goal) ==> deletion of a random array
- if len(genome) == len(goal) ==> change random value with one from the initial set

### Cross-over
As seen in cass, I take a random point of my genome and then I cut at this point. The cut must be maximum the length of the smallest genome

# Results
- N = 5:
    - TOP 3: [5,5,5]
- N = 10:
    - TOP 3: [10,10,10]
- N = 20:
    - TOP 3: [23,24,24]
- N = 50:
    - TOP 3: [66,66,66]
- N = 100:
    - TOP 3: [176,183,183]
- N = 500:
    - TOP 3: [1401,1401,1401]
- N = 1000:
    - TOP 3: [3558,3603,3605]