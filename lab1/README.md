# Lab 1: Set covering

ALL the codes and the comments are in the file lab1.ipynb

## SOLUTION 1: THE BEST
### Greedy_first

```python
def greedy_first(N):
    INITIAL_STATE = State()
    parent_state = dict()
    state_cost = dict()
    covering = set()
    goal  =  set(range(N))
    def h(state):
        return len(goal.difference(set([el for a in state.array for el in a])))
    final = searchV2(
        N,
        INITIAL_STATE,
        goal_test=goal,
        parent_state=parent_state,
        state_cost=state_cost,
        priority_function=lambda s: h(s) ,
        unit_cost=lambda a: sum(len(_) for _ in a.array)
    )
    logging.info(
            f"gready_best_first first solution for N={N}: w={sum(len(_) for _  in final[0])} (bloat={(sum(len(_) for _ in final[0])-N)/N*100:.0f}%)"
        )
logging.getLogger().setLevel(logging.INFO)
for N in [5,10,20,100,500,1000]:
    greedy_first(N)
```

We get this solution


- NEW SOL: Found a solution in 3 nodes;
    - gready_best_first first solution for N=5: w=5 (bloat=0%)
- NEW SOL: Found a solution in 3 nodes; 
    - gready_best_first first solution for N=10: w=10 (bloat=0%)
- NEW SOL: Found a solution in 4 nodes;
    - gready_best_first first solution for N=20: w=28 (bloat=40%)
- NEW SOL: Found a solution in 5 nodes; 
    - gready_best_first first solution for N=100: w=192 (bloat=92%)
- NEW SOL: Found a solution in 7 nodes; 
    - gready_best_first first solution for N=500: w=1320 (bloat=164%)
- NEW SOL: Found a solution in 8 nodes;
    - gready_best_first first solution for N=1000: w=2893 (bloat=189%)

## SOLUTION 2: 
### A*
```python
def a_star(N):
    INITIAL_STATE = State()
    parent_state = dict()
    state_cost = dict()
    covering = set()
    goal  =  set(range(N))
    def h(state):
        return len(goal.difference(set([el for a in state.array for el in a])))

    final = searchV2(
        N,
        INITIAL_STATE,
        goal_test=goal,
        parent_state=parent_state,
        state_cost=state_cost,
        priority_function=lambda s: h(s) + state_cost[s] ,
        unit_cost=lambda a: sum(len(_) for _ in a.array)
    )
    logging.info(
            f"A* first solution for N={N}: w={sum(len(_) for _  in final[0])} (bloat={(sum(len(_) for _ in final[0])-N)/N*100:.0f}%)"
        )
logging.getLogger().setLevel(logging.INFO)
for N in [5,10,20,100,500,1000]:
    a_star(N)
```

- NEW SOL: Found a solution in 5 nodes; 
    - A* first solution for N=5: w=5 (bloat=0%)
- NEW SOL: Found a solution in 6 nodes; 
    - A* first solution for N=10: w=11 (bloat=10%)
- NEW SOL: Found a solution in 7 nodes; 
    - A* first solution for N=20: w=28 (bloat=40%)
- NEW SOL: Found a solution in 13 nodes; 
    - A* first solution for N=100: w=230 (bloat=130%)
- NEW SOL: Found a solution in 20 nodes;
    - A* first solution for N=500: w=1828 (bloat=266%)
- NEW SOL: Found a solution in 23 nodes; 
    - A* first solution for N=1000: w=4130 (bloat=313%)

## SOLUTION 3: 
### Breath first
```python
def breath_first(N):
    INITIAL_STATE = State()
    parent_state = dict()
    state_cost = dict()
    covering = set()
    goal  =  set(range(N))


    final = searchV2(
        N,
        INITIAL_STATE,
        goal_test=goal,
        parent_state=parent_state,
        state_cost=state_cost,
        priority_function=lambda s: len(state_cost) ,
        unit_cost=lambda a: 1
    )
    logging.info(
            f"breath_first first solution for N={N}: w={sum(len(_) for _  in final[0])} (bloat={(sum(len(_) for _ in final[0])-N)/N*100:.0f}%)"
        )
logging.getLogger().setLevel(logging.INFO)
for N in [5,10,20,100,500,1000]:
    breath_first(N)
```
- NEW SOL: Found a solution in 6 steps; visited 40 nodes
    - breath_first first solution for N=5: w=5 (bloat=0%)
- NEW SOL: Found a solution in 8 steps; visited 267 nodes
    - breath_first first solution for N=10: w=13 (bloat=30%)
- NEW SOL: Found a solution in 13 steps; visited 304 nodes
    - breath_first first solution for N=20: w=46 (bloat=130%)
- NEW SOL: Found a solution in 20 steps; visited 7,270 nodes
    - breath_first first solution for N=100: w=332 (bloat=232%)
- NEW SOL: Found a solution in 25 steps; visited 40,366 nodes
    - breath_first first solution for N=500: w=2162 (bloat=332%)
- NEW SOL: Found a solution in 27 steps; visited 87,907 nodes
    - breath_first first solution for N=1000: w=4652 (bloat=365%)

## Solution 4

```python
def depth_first(N):
    INITIAL_STATE = State()
    parent_state = dict()
    state_cost = dict()
    covering = set()
    goal  =  set(range(N))


    final = searchV2(
        N,
        INITIAL_STATE,
        goal_test=goal,
        parent_state=parent_state,
        state_cost=state_cost,
        priority_function=lambda s: -len(state_cost) ,
        unit_cost=lambda a:1
    )
    logging.info(
            f"breath_first first solution for N={N}: w={sum(len(_) for _  in final[0])} (bloat={(sum(len(_) for _ in final[0])-N)/N*100:.0f}%)"
        )
logging.getLogger().setLevel(logging.INFO)
for N in [5,10,20,100,500,1000]:
    depth_first(N)
```
- NEW SOL: Found a solution in 5 steps; visited 47 nodes
    - breath_first first solution for N=5: w=8 (bloat=60%)
- NEW SOL: Found a solution in 5 steps; visited 119 nodes
    - breath_first first solution for N=10: w=19 (bloat=90%)
- NEW SOL: Found a solution in 8 steps; visited 159 nodes
    - breath_first first solution for N=20: w=57 (bloat=185%)
- NEW SOL: Found a solution in 10 steps; visited 3,123 nodes
    - breath_first first solution for N=100: w=379 (bloat=279%)
- NEW SOL: Found a solution in 11 steps; visited 16,751 nodes
    - breath_first first solution for N=500: w=2044 (bloat=309%)
- NEW SOL: Found a solution in 14 steps; visited 40,987 nodes
    - breath_first first solution for N=1000: w=5242 (bloat=424%)