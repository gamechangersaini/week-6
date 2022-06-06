# week-6
#include <bits/stdc++.h>
using namespace std;
class Solution
{
	void dfs(int node, vector<int> &vis, vector<int> adj[], int destiny)
	{
		if (node == destiny)
		{
			reach = true;
		}

		vis[node] = 1;
		for (auto it : adj[node])
		{
			if (!vis[it])
			{

				dfs(it, vis, adj, destiny);
			}
		}
	}

public:
	static bool reach;
	void Ispath(int node, int V, vector<int> adj[], int destiny)
	{

		vector<int> vis(V + 1, 0);
		bool reach = false;

		dfs(node, vis, adj, destiny);
	}
};
bool Solution::reach = false;

void addEdge(vector<int> adj[], int u, int v)
{
	adj[u].push_back(v);
	adj[v].push_back(u);
}
int main()
{
	int vertices;
	cin >> vertices;
	vector<int> adj[vertices+1];
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
				addEdge(adj, i + 1, j + 1);
			}
		}
	}
	int start, end;
	cin >> start >> end;
	Solution obj;
	obj.Ispath(start, vertices, adj, end);
	if (Solution::reach)
	{
		cout << "Yes Path Exists";
	}
	else
	{
		cout << "NO path exists";
	}

	return 0;
}
