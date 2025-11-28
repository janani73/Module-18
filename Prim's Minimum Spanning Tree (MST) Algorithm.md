# Ex. No: 18A - Implementation of Prim’s Algorithm for Minimum Spanning Tree in Python

## AIM:
To compute a Minimum Spanning Tree (MST) of a weighted undirected graph using Prim’s algorithm, which incrementally builds the MST by selecting the least-weight edge connecting a vertex in the MST to a vertex outside it.
## ALGORITHM:
```
1.Graph Representation:
      ->Use an adjacency matrix to represent the weighted undirected graph.
2.Initialization:
      ->Create arrays:
            ->key[] — stores the minimum weight to connect a vertex to the MST.
            ->parent[] — stores the MST structure.
            ->mstSet[] — keeps track of vertices included in MST.
      ->Initialize all key[] values to INF except the first vertex (set to 0).
      ->Initialize parent[0] = -1 as the first vertex is the root of MST.
3.MST Construction Loop:
      ->Repeat for all vertices:
            ->Pick vertex u not in MST with the minimum key value.
            ->Include u in MST (mstSet[u] = True).
            ->For each adjacent vertex v of u:
                     ->If v is not in MST and graph[u][v] < key[v], update key[v] = graph[u][v] and parent[v] = u.
4.Output MST:
      ->Traverse parent[] to print all edges and their weights in the MST.
```
## PYTHON PROGRAM

```
import sys # Library for INT_MAX
class Graph():
	def __init__(self, vertices):
		self.V = vertices
		self.graph = [[0 for column in range(vertices)]
					for row in range(vertices)]
	# A utility function to print the constructed MST stored in parent[]
	def printMST(self, parent):
		print ("Edge   Weight")
		for i in range(1, self.V):
			print (parent[i], "-", i, "  ",self.graph[i][parent[i]])
	# A utility function to find the vertex with
	# minimum distance value, from the set of vertices
	# not yet included in shortest path tree
	def minKey(self, key, mstSet):
		# Initialize min value
		min = sys.maxsize
		for v in range(self.V):
			if key[v] < min and mstSet[v] == False:
				min = key[v]
				min_index = v
		return min_index
	# Function to construct and print MST for a graph
	# represented using adjacency matrix representation
	def primMST(self):
		# Key values used to pick minimum weight edge in cut
		key = [sys.maxsize] * self.V
		parent = [None] * self.V # Array to store constructed MST
		# Make key 0 so that this vertex is picked as first vertex
		key[0] = 0
		mstSet = [False] * self.V
		parent[0] = -1 # First node is always the root of
		for cout in range(self.V):
		    u=self.minKey(key,mstSet)
		    mstSet[u]=True
		    for v in range(self.V):
		        if self.graph[u][v]>0 and mstSet[v]==False and key[v]>self.graph[u][v]:
		            key[v]=self.graph[u][v]
		            parent[v]=u
		self.printMST(parent)
g = Graph(5)
g.graph = [ [0, 2, 0, 6, 0],
			[2, 0, 3, 8, 5],
			[0, 3, 0, 0, 7],
			[6, 8, 0, 0, 9],
			[0, 5, 7, 9, 0]]
g.primMST();
```

## OUTPUT
<img width="1163" height="277" alt="image" src="https://github.com/user-attachments/assets/f1a5d08b-4081-4a93-8827-bde0433b3cc2" />

## RESULT

Thus, the Minimum Spanning Tree (MST) has been successfully verified.
