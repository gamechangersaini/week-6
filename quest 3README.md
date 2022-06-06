# week-6
#include<bits/stdc++.h>

using namespace std;

class Solution {
  private:
    bool checkCycle(int node, vector < int > adj[], int vis[], int dfsVis[]) {
      vis[node] = 1;
      dfsVis[node] = 1;
      for (auto it: adj[node]) {
        if (!vis[it]) {
          if (checkCycle(it, adj, vis, dfsVis)) return true;
        } else if (dfsVis[it]) {
          return true;
        }
      }
      dfsVis[node] = 0;
      return false;
    }
  public:
    bool isCyclic(int N, vector < int > adj[]) {
      int vis[N], dfsVis[N];
      memset(vis, 0, sizeof vis);
      memset(dfsVis, 0, sizeof dfsVis);

      for (int i = 0; i < N; i++) {
        if (!vis[i]) {
          // cout << i << endl; 
          if (checkCycle(i, adj, vis, dfsVis)) {
            return true;
          }
        }
      }
      return false;
    }
};

void addEdge(vector < int > adj[], int u, int v) {
  adj[u].push_back(v);
}


int main()
{
    int vertices;
	cin >> vertices;
	vector<int> adj[vertices];
	int matrix[vertices][vertices];
	for (int i = 0; i < vertices; i++)
	{
		for (int j = 0; j < vertices; j++)
		{
			cin >> matrix[i][j];
		}
	}
	for (int i = 0; i < vertices; i++)
	{
		for (int j = 0; j < vertices; j++)
		{
			if (matrix[i][j])
			{
				addEdge(adj, i ,j);
			}
		}
	}   
    Solution obj;
  if (obj.isCyclic(vertices, adj))
    cout << "Yes Cycle Exists";
  else
    cout << "No Cycle Exists";

  return 0;
}
