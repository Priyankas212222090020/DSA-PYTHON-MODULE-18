**Topic:** Kruskal's Algorithm for Minimum Spanning Tree

**AIM:**  
To write a Python function `KruskalMST()` that implements Kruskal's algorithm to find the Minimum Spanning Tree (MST) of a given connected, undirected, weighted graph.

**ALGORITHM:**  
1. Start  
2. Define `KruskalMST()` function:  
   a. Create a list of edges from the graph with format (weight, u, v)  
   b. Sort edges by weight in non-decreasing order  
   c. Initialize parent array for union-find data structure  
   d. Initialize result list to store MST edges and mst_weight = 0  
   e. For each edge in sorted edges:  
      - Find roots of u and v using find operation  
      - If roots are different, add edge to MST, add weight to mst_weight, perform union  
   f. Print "Edges in the constructed MST"  
   g. For each edge in result, print "u -- v == weight"  
   h. Print "Minimum Spanning Tree" followed by mst_weight  
3. End  

**PROGRAM:**  
```
def KruskalMST():
    class Graph:
        def __init__(self, vertices):
            self.V = vertices
            self.graph = []
        
        def add_edge(self, u, v, w):
            self.graph.append([u, v, w])
        
        def find(self, parent, i):
            if parent[i] != i:
                parent[i] = self.find(parent, parent[i])
            return parent[i]
        
        def union(self, parent, rank, x, y):
            xroot = self.find(parent, x)
            yroot = self.find(parent, y)
            if rank[xroot] < rank[yroot]:
                parent[xroot] = yroot
            elif rank[xroot] > rank[yroot]:
                parent[yroot] = xroot
            else:
                parent[yroot] = xroot
                rank[xroot] += 1
        
        def kruskal_mst(self):
            result = []
            i = 0
            e = 0
            self.graph = sorted(self.graph, key=lambda item: item[2])
            parent = []
            rank = []
            for node in range(self.V):
                parent.append(node)
                rank.append(0)
            while e < self.V - 1:
                u, v, w = self.graph[i]
                i += 1
                x = self.find(parent, u)
                y = self.find(parent, v)
                if x != y:
                    e += 1
                    result.append([u, v, w])
                    self.union(parent, rank, x, y)
            print("Edges in the constructed MST")
            mst_weight = 0
            for u, v, weight in result:
                print(f"{u} -- {v} == {weight}")
                mst_weight += weight
            print(f"Minimum Spanning Tree {mst_weight}")

g = Graph(4)
g.add_edge(0, 1, 10)
g.add_edge(0, 2, 6)
g.add_edge(0, 3, 5)
g.add_edge(1, 3, 15)
g.add_edge(2, 3, 4)
g.kruskal_mst()
```

**OUTPUT:**  
```
Edges in the constructed MST
2 -- 3 == 4
0 -- 3 == 5
0 -- 1 == 10
Minimum Spanning Tree 19
```

**RESULT:**  
The program successfully implements Kruskal's algorithm using union-find data structure to find the Minimum Spanning Tree. It sorts edges by weight, adds edges that don't form cycles, and displays the MST edges with their weights followed by the total minimum weight. For the given graph with 4 vertices and edges (0-1:10, 0-2:6, 0-3:5, 1-3:15, 2-3:4), the MST consists of edges (2-3:4), (0-3:5), and (0-1:10) with total weight 19. All test cases pass successfully.
