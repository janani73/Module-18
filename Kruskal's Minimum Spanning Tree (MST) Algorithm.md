# Ex. No: 18B - Kruskal’s Algorithm for Minimum Spanning Tree (MST)

## AIM:
To compute the Minimum Spanning Tree of a weighted undirected graph using Kruskal’s algorithm, which selects edges in ascending order of weight while ensuring no cycles are formed.
## ALGORITHM:
```
1.Graph Representation:
       ->Represent the graph as a list of edges [u, v, w], where u and v are vertices and w is the weight.
2.Sort Edges:
       ->Sort all edges by increasing weight.
3.Initialize Disjoint Sets:
       ->Each vertex is its own parent (parent[]) and has a rank[] initialized to 0.
4.Select Edges for MST:
      ->For each edge in sorted order:
            ->Use find() to determine the root of both vertices.
            ->If roots are different, include the edge in MST and perform union() to merge sets.
     ->Repeat until MST contains V-1 edges.
5.Output MST:
     ->Print all edges included in MST along with their weights.
     ->Compute and print the total weight of the MST.
```

## PYTHON PROGRAM

```
from collections import defaultdict
class Graph:
	def __init__(self, vertices):
		self.V = vertices # No. of vertices
		self.graph = [] # default dictionary
	def addEdge(self, u, v, w):
		self.graph.append([u, v, w])
	def find(self, parent, i):
		if parent[i] == i:
			return i
		return self.find(parent, parent[i])
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
	def KruskalMST(self):
		result = [] # This will store the resultant MST
		i = 0
		e = 0
		self.graph = sorted(self.graph,
							key=lambda item: item[2])
		parent = []
		rank = []
		for node in range(self.V):
		    parent.append(node)
		    rank.append(0)
		while e<self.V-1:
		    u,v,w=self.graph[i]
		    i=i+1
		    x=self.find(parent,u)
		    y=self.find(parent,v)
		    if x!=y:
		        e=e+1
		        result.append([u,v,w])
		        self.union(parent,rank,x,y)
		minimumCost=0
		print("Edges in the constructed MST")
		for u,v,weight in result:
		    minimumCost+=weight
		    print("%d -- %d == %d" % (u,v,weight))
		print("Minimum Spanning Tree",minimumCost)
# Driver code
g = Graph(4)
g.addEdge(0, 1, 10)
g.addEdge(0, 2, 6)
g.addEdge(0, 3, 5)
g.addEdge(1, 3, 15)
g.addEdge(2, 3, 4)
# Function call
g.KruskalMST()
```

## OUTPUT
<img width="1192" height="292" alt="image" src="https://github.com/user-attachments/assets/fd5b7ee5-d183-40ad-9923-f289d1b3e263" />

## RESULT
->The program successfully verified the selection of edges with minimum weight to construct the MST.

->All vertices are connected without forming cycles, ensuring the MST is valid.

->Total weight of the MST is correctly computed and successfully verified.
