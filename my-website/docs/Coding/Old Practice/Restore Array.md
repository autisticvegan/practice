```
#include <unordered_map>
#include <vector>


//insert values int adj list
//as you do so, keep track of degree count
//degree of 1 is our start point
//also keep track of all nodes

// check if all visited or size or whatever

class Solution {
    public:
    std::unordered_map<int, std::vector<int>> adjList;
    std::vector<int> finalAnswer;
    std::unordered_map<int, bool> node2isVisited;
    std::unordered_map<int, int> node2degree;

    void dfs(int source) {
        node2isVisited[source] = true;
        finalAnswer.push_back(source);


        for (int i = 0; i < adjList[source].size(); i++) {
            int neighbor = adjList[source][i];
            if (!node2isVisited[neighbor]) {
                dfs(neighbor);
            }
        }
    }

std::vector<int> restoreArray(std::vector<std::vector<int>>& pairs) {
    for (int i = 0; i < pairs.size(); i++) {
        int node1 = pairs[i][0];
        int node2 = pairs[i][1];
        adjList[node1].push_back(node2);
        adjList[node2].push_back(node1);
        node2degree[node1]++;
        node2degree[node2]++;
    }

    int startNode = -1;
    for (int i = 0; i < node2degree.size(); i++) {
        if (node2degree[i] == 1) {
            startNode = i;
            break;
        }
    }

    if (startNode == -1) {
        return {};
    }

    dfs(startNode);
    return finalAnswer;
}
    
}

``