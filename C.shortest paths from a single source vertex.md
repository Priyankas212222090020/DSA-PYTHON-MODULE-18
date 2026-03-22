## Aim
To find the shortest paths from a single source vertex to all other vertices in a weighted graph using Dijkstra's algorithm, which selects vertices with minimum distance and relaxes edges.

## Algorithm
1. Initialize distance array with INFINITY, set source distance = 0
2. Create a visited set to track processed vertices
3. Repeat V times:
   - Select vertex u with minimum distance not yet visited
   - Mark u as visited
   - For each adjacent vertex v, update distance if a shorter path is found
4. Print all vertices with their shortest distances from source

## Program
```python
import sys

class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.graph = [[0 for _ in range(vertices)] for _ in range(vertices)]
    
    def add_edge(self, u, v, w):
        self.graph[u][v] = w
        self.graph[v][u] = w
    
    def min_distance(self, dist, visited):
        min_val = sys.maxsize
        min_index = -1
        
        for v in range(self.V):
            if dist[v] < min_val and not visited[v]:
                min_val = dist[v]
                min_index = v
        return min_index
    
    def dijkstra(self, src):
        dist = [sys.maxsize] * self.V
        dist[src] = 0
        visited = [False] * self.V
        
        for _ in range(self.V):
            u = self.min_distance(dist, visited)
            visited[u] = True
            
            for v in range(self.V):
                if self.graph[u][v] > 0 and not visited[v] and dist[v] > dist[u] + self.graph[u][v]:
                    dist[v] = dist[u] + self.graph[u][v]
        
        print("Vertex   Distance from Source")
        for i in range(self.V):
            print(f"{i}             {dist[i]}")

g = Graph(9)
g.add_edge(0, 1, 4)
g.add_edge(0, 7, 8)
g.add_edge(1, 2, 8)
g.add_edge(1, 7, 11)
g.add_edge(2, 3, 7)
g.add_edge(2, 5, 4)
g.add_edge(2, 8, 2)
g.add_edge(3, 4, 9)
g.add_edge(3, 5, 14)
g.add_edge(4, 5, 10)
g.add_edge(5, 6, 2)
g.add_edge(6, 7, 1)
g.add_edge(6, 8, 6)
g.add_edge(7, 8, 7)

g.dijkstra(0)
```

## Output
```
Vertex   Distance from Source
0             0
1             4
2             12
3             19
4             16
5             11
6             9
7             8
8             14
```
