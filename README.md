# corontine
#include <bits/stdc++.h>
using namespace std;
vector<int>cs;
int A[10][10];
int c;
  
// Graph class represents a undirected graph 
// using adjacency list representation 
class Graph { 
    // No. of vertices 
    int V; 
  
    // Pointer to an array containing adjacency lists 
    list<int>* adj; 
  
    // A function used by DFS 
    int DFSUtil(int v, bool visited[]); 
  
public: 
    // Constructor 
    Graph(int V); 
  
    void addEdge(int v, int w); 
    void NumberOfconnectedComponents(); 
}; 
  
// Function to return the number of 
// connected components in an undirected graph 
void Graph::NumberOfconnectedComponents() 
{ 
  
    // Mark all the vertices as not visited 
    bool* visited = new bool[V]; 
  
    // To store the number of connected components 
    int count = 0; 
    for (int v = 0; v < V; v++) 
        visited[v] = false; 
  
    for (int v = 0; v < V; v++) { 
        if (visited[v] == false) { 
            cs.push_back(DFSUtil(v, visited)); 
            count += 1; 
        } 
    } 
  
    
} 
  
int Graph::DFSUtil(int v, bool visited[]) 
{ 
  
    // Mark the current node as visited 
    visited[v] = true; 
  
    // Recur for all the vertices 
    // adjacent to this vertex 
    list<int>::iterator i; 
     
    for (i = adj[v].begin(); i != adj[v].end(); ++i) 
    { if (!visited[*i]) 
       { DFSUtil(*i, visited); 
          c++;    
       }
    }
return c; 
    c=0;
}
  
Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 
  
// Add an undirected edge 
void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); 
    adj[w].push_back(v); 
}

int main() {
    
   int n,k=1,ans,sum=0;
    cin>>n;
    Graph g(2*n);
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            A[i][j]=k++;
    int p;
    cin>>p;
    for(int i=0;i<p;i++)
    {
        int x1,y1,x2,y2;
        cin>>x1>>y1>>x2>>y2;
        g.addEdge(A[x1-1][y1-1],A[x2-1][y2-1]);
        
    }
     g.NumberOfconnectedComponents();
     for(int i=0;i<cs.size();i++)
     {
         sum+=(cs[i]*(cs[i]-1))/2;
         
     }
    ans= (n*(n-1))/2-sum;
    cout<<ans<<endl;
    
    return 0;
}
