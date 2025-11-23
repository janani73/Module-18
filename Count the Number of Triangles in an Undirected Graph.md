# Ex. No: 18E - Finding the Number of Triangles in an Undirected Graph Using Adjacency Matrix in Python

## AIM:
To determine and successfully verify the total number of triangles present in a given undirected graph using its adjacency matrix representation.
## ALGORITHM:
```
1.Input the graph:
       ->Represent the graph using an adjacency matrix graph[V][V], where V is the number of vertices.
2.Matrix multiplication:
       ->Compute graph^2 (square of the adjacency matrix).
       ->Compute graph^3 by multiplying graph with graph^2.
3.Compute trace:
       ->Calculate the sum of diagonal elements of graph^3.
4.Calculate total triangles:
       ->Divide the trace by 6 to get the exact number of triangles.
```
## PYTHON PROGRAM

```
def multiply(A, B, C):
	global V
	for i in range(V):
		for j in range(V):
			C[i][j] = 0
			for k in range(V):
				C[i][j] += A[i][k] * B[k][j]
def getTrace(graph):
	global V
	trace = 0
	for i in range(V):
		trace += graph[i][i]
	return trace
def triangleInGraph(graph):
	global V
	aux2 = [[None] * V for i in range(V)]
	aux3 = [[None] * V for i in range(V)]
	for i in range(V):
		for j in range(V):
			aux2[i][j] = aux3[i][j] = 0
	multiply(graph, graph, aux2)
	multiply(graph,aux2,aux3)
	trace=getTrace(aux3)
	return trace//6
V = int(input())
graph = [[0, 1, 1, 0],
		[1, 0, 1, 1],
		[1, 1, 0, 1],
		[0, 1, 1, 0]]
print("Total number of Triangle in Graph :",
					triangleInGraph(graph))
```

## OUTPUT
<img width="1187" height="272" alt="image" src="https://github.com/user-attachments/assets/651c548e-1505-4db5-8dbc-adf9c597473a" />

## RESULT
The program successfully verified that the total number of triangles in the graph.
