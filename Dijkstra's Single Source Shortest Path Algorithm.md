# Ex. No: 18C - Dijkstra’s Algorithm for Single Source Shortest Path

## AIM:
To determine the shortest distance from a given source vertex to all other vertices in a weighted graph using Dijkstra’s algorithm, which repeatedly selects the nearest unvisited vertex and updates distances.

## ALGORITHM:
```
1.Graph Representation:
      ->Represent the graph using an adjacency matrix where graph[i][j] is the weight of the edge between vertices i and j.
2.Initialization:
      ->Create a dist[] array to store shortest distances from the source, initialized to infinity for all vertices except the source (set to 0).
      ->Create sptSet[] to track vertices whose shortest distance is finalized.
3.Main Loop:
      ->Repeat for all vertices:
           ->Pick the vertex u not yet included in sptSet[] with the minimum distance (minDistance() function).
           ->Include u in sptSet[].
           ->For each adjacent vertex v of u:
                 ->If v is not in sptSet[] and dist[u] + graph[u][v] < dist[v], update dist[v].
4.Output Shortest Paths:
           ->Print the shortest distance from the source to each vertex using the printSolution() function.
```

## PYTHON PROGRAM

```
import sys
class Graph():
	def __init__(self, vertices):
		self.V = vertices
		self.graph = [[0 for column in range(vertices)]
					for row in range(vertices)]
	def printSolution(self, dist):
		print("Vertex   Distance from Source")
		for node in range(self.V):
			print(node, "           ", dist[node])
	def minDistance(self, dist, sptSet):
		min = sys.maxsize
		for u in range(self.V):
			if dist[u] < min and sptSet[u] == False:
				min = dist[u]
				min_index = u
		return min_index
	def dijkstra(self, src):
		dist = [sys.maxsize] * self.V
		dist[src] = 0
		sptSet = [False] * self.V
		for cout in range(self.V):
		    x=self.minDistance(dist,sptSet)
		    sptSet[x]=True
		    for y in range(self.V):
		        if self.graph[x][y]>0 and sptSet[y]==False and dist[y]>dist[x]+self.graph[x][y]:
		            dist[y]=dist[x]+self.graph[x][y]
		self.printSolution(dist)
# Driver program
g = Graph(9)
g.graph = [[0, 4, 0, 0, 0, 0, 0, 8, 0],
		[4, 0, 8, 0, 0, 0, 0, 11, 0],
		[0, 8, 0, 7, 0, 4, 0, 0, 2],
		[0, 0, 7, 0, 9, 14, 0, 0, 0],
		[0, 0, 0, 9, 0, 10, 0, 0, 0],
		[0, 0, 4, 14, 10, 0, 2, 0, 0],
		[0, 0, 0, 0, 0, 2, 0, 1, 6],
		[8, 11, 0, 0, 0, 0, 1, 0, 7],
		[0, 0, 2, 0, 0, 0, 6, 7, 0]
		];
g.dijkstra(0);
```

## OUTPUT
<img width="1181" height="410" alt="image" src="https://github.com/user-attachments/assets/57e40e85-ff07-48c0-a63d-15b9b262579a" />

## RESULT
->The program successfully verified the computation of shortest paths from the given source vertex to all other vertices.

->The distances are correctly computed using Dijkstra’s algorithm.

->Each vertex’s shortest distance is successfully verified against the adjacency matrix weights.
