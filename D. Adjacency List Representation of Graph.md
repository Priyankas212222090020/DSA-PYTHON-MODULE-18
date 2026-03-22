**Topic:** Adjacency List Representation of Graph

**AIM:**  
To write a Python program with a print function that demonstrates the adjacency list representation of a graph.

**ALGORITHM:**  
1. Start  
2. Define `print_adjacency_list(graph)` function:  
   a. Iterate through each vertex in the graph  
   b. Print "Adjacency list of vertex" followed by vertex number  
   c. Print the vertex followed by "->" and each neighbor  
   d. Format output with proper spacing  
3. Create adjacency list representation of the graph  
4. Call the print function to display the adjacency list  
5. End  

**PROGRAM:**  
```
def print_adjacency_list(graph):
    for vertex in sorted(graph.keys()):
        print(f"Adjacency list of vertex {vertex}")
        print(f" {vertex} ->", end="")
        for neighbor in graph[vertex]:
            print(f" {neighbor} ->", end="")
        print()

graph = {
    0: [4, 1],
    1: [4, 3, 2, 0],
    2: [3, 1],
    3: [4, 2, 1],
    4: [3, 1, 0]
}

print_adjacency_list(graph)
```

**OUTPUT:**  
```
Adjacency list of vertex 0
 0 -> 4 -> 1 ->
Adjacency list of vertex 1
 1 -> 4 -> 3 -> 2 -> 0 ->
Adjacency list of vertex 2
 2 -> 3 -> 1 ->
Adjacency list of vertex 3
 3 -> 4 -> 2 -> 1 ->
Adjacency list of vertex 4
 4 -> 3 -> 1 -> 0 ->
```

**RESULT:**  
The program successfully demonstrates the adjacency list representation of a graph. The `print_adjacency_list` function iterates through all vertices and prints each vertex followed by its adjacent vertices in the required format with arrows. The output matches the expected format with proper spacing and arrow separators. All test cases pass successfully.
