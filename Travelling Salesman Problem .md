# Ex. No: 18D - Dijkstra’s Algorithm for Single Source Shortest Path

## AIM:
To compute the shortest path distances from a given source vertex to all other vertices in a weighted graph using Dijkstra’s algorithm, ensuring the results are efficiently and correctly determined.
## ALGORITHM:
```
1.Graph Representation:
      ->Represent the graph using an adjacency matrix graph[i][j] indicating the weight of the edge from vertex i to vertex j.
2.Initialization:
      ->Create a dist[] array initialized with infinity for all vertices except the source, which is initialized to 0.
      ->Create sptSet[] (shortest path tree set) initialized to False for all vertices.
3.Iterative Process:
      ->Repeat for all vertices:
            ->Select the vertex u not in sptSet[] with the minimum distance (minDistance() function).
            ->Mark u as visited by setting sptSet[u] = True.
            ->Update dist[v] for all adjacent vertices v of u if the new path through u is shorter.
4.Output:
      ->Print the shortest distances from the source vertex to all other vertices using printSolution().
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
<img width="1186" height="407" alt="image" src="https://github.com/user-attachments/assets/853c1f04-c3e7-4374-9a41-65ede0ce45ba" />

## RESULT
->The program successfully verified the shortest paths from the source vertex to all other vertices.

->Distances are correctly computed according to the adjacency matrix weights.

->The algorithm successfully verified that each vertex is assigned the minimum possible distance from the source.
