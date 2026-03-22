## Aim
To find the minimum number of dice throws required to reach the last cell from the first cell on a Snake and Ladder board, considering that ladders move the player forward and snakes move the player backward, using Breadth-First Search (BFS) to find the shortest path.

## Algorithm
1. Create a move array where move[i] = destination if cell i has a snake/ladder, else -1
2. Perform BFS from cell 0:
   - Initialize distance array with -1, set distance[0] = 0
   - Use queue to process cells level by level
   - For each cell, try all 6 dice outcomes (1 to 6)
   - Calculate next cell = current + dice
   - If move[next] != -1, update next to move[next]
   - If next cell not visited, mark distance and enqueue
3. Return distance[N-1] as minimum dice throws

## Program
```python
from collections import deque

def min_dice_throws(N, moves):
    dist = [-1] * N
    dist[0] = 0
    queue = deque([0])
    
    while queue:
        curr = queue.popleft()
        
        for dice in range(1, 7):
            next_cell = curr + dice
            
            if next_cell >= N:
                continue
            
            if moves[next_cell] != -1:
                next_cell = moves[next_cell]
            
            if dist[next_cell] == -1:
                dist[next_cell] = dist[curr] + 1
                queue.append(next_cell)
                
                if next_cell == N - 1:
                    return dist[next_cell]
    
    return dist[N - 1]

N = 30
moves = [-1] * N

ladders = {2: 21, 4: 7, 10: 25, 19: 28}
snakes = {26: 0, 20: 8, 16: 3, 18: 6}

for start, end in ladders.items():
    moves[start - 1] = end - 1

for start, end in snakes.items():
    moves[start - 1] = end - 1

result = min_dice_throws(N, moves)
print(f"Min Dice throws required is {result}")
```

## Output
```
Min Dice throws required is 3
```
