<p align="center"> ������������ ����������� ���������� ��������</p>
<p align="center">���������� �����������</p>
<p align="center">���������� ��������������� ����������� �����������</p>
<p align="center">������� ���</p>
<br><br><br><br><br><br><br>
<p align="center">������������ ������ �3</p>
<p align="center">�� ���������� ������ ������ ���������������� ������</p>
<p align="center">����: ����������� ������ ���������� ��� ������ �� ��������</p>
<br><br><br><br><br>
<p align="right">��������:</p>
<p align="right">������� 2 �����</p>
<p align="right">������ ��-26</p>
<p align="right">������ �. �.</p>
<p align="right">���������:</p>
<p align="right">�������� �. �.</p>
<br><br><br><br><br>
<p align="center">����� 2024</p>

<hr>

# ����� ������� #
1. �������� ����� �� ����������� ������������ ������ �1 � .md ������� (readme.md) � � ������� ������� �� �������� ��������� (pull request) ���������� ��� � ��������� ��������: trunk\ii0xxyy\task_02\doc (��� xx - ����� ������, yy - ����� ��������, �������� ii02302)..
2. �������� ��� ���������� ��������� ���������� � ��������: **trunk\ii0xxyy\task_01\src**.
## ������� ##
�������. �� C++ ����������� ���������, ������������ ������������� ���� ���-���������. � �������� ������� ���������� ������������ �������������� ������, ���������� � ���������� ������. � ������ ����� �������� ������� ��� ������ ������� ����������� �������, �������� ���������� ����������.

<hr>

# ���������� ������� #

��� ���������:
```
#include <iostream>
#include <vector>
#include <list>
#include <queue>
#include <unordered_set>

using namespace std;

class Graph {
private:
    struct Node {
        int id;
        list<int> adjNodes;
    };

    vector<Node> nodes;

    // �������� �� ������� �������� �����
    bool isEulerian() const {
        for (const auto& node : nodes) {
            if (node.adjNodes.size() % 2 != 0) {
                return false;
            }
        }
        return true;
    }

    // ����������� ������ ��� ���������� ������������ �����
    bool findHamiltonianCycle(int node, int depth, vector<int>& cycle, vector<bool>& visited) {
        if (depth == nodes.size()) {
            return cycle.front() == cycle.back();
        }

        for (int adj : nodes[node].adjNodes) {
            if (!visited[adj]) {
                visited[adj] = true;
                cycle[depth] = adj;
                if (findHamiltonianCycle(adj, depth + 1, cycle, visited)) {
                    return true;
                }
                visited[adj] = false;
            }
        }
        return false;
    }

public:
    // ���������� ������ ����
    void addNode(int id) {
        nodes.push_back({id, {}});
    }

    // ���������� ���� (����������������� ����)
    void addEdge(int start, int end) {
        nodes[start].adjNodes.push_back(end);
        nodes[end].adjNodes.push_back(start);
    }

    // ����� �����
    void showGraph() const {
        for (const auto& node : nodes) {
            cout << "Node " << node.id << ": ";
            for (int neighbor : node.adjNodes) {
                cout << neighbor << " ";
            }
            cout << endl;
        }
    }

    // ��������� �������� �����
    vector<int> getEulerianCycle() {
        vector<int> cycle;
        if (!isEulerian()) return cycle;

        vector<bool> visited(nodes.size(), false);
        list<int> stack;
        stack.push_back(0);

        while (!stack.empty()) {
            int current = stack.back();
            if (!nodes[current].adjNodes.empty()) {
                int next = nodes[current].adjNodes.front();
                stack.push_back(next);
                nodes[current].adjNodes.remove(next);
                nodes[next].adjNodes.remove(current);
            } else {
                cycle.push_back(current);
                stack.pop_back();
            }
        }
        return cycle;
    }

    // ��������� ������������ �����
    vector<int> getHamiltonianCycle() {
        vector<int> cycle(nodes.size(), -1);
        vector<bool> visited(nodes.size(), false);
        visited[0] = true;
        cycle[0] = 0;

        if (findHamiltonianCycle(0, 1, cycle, visited)) {
            return cycle;
        }
        return {};
    }

    // ���������� ��������� ������ (���������� BFS)
    Graph getSpanningTree() const {
        Graph spanningTree;
        for (int i = 0; i < nodes.size(); ++i) {
            spanningTree.addNode(i);
        }

        vector<bool> visited(nodes.size(), false);
        visited[0] = true;
        queue<int> q;
        q.push(0);

        while (!q.empty()) {
            int current = q.front();
            q.pop();

            for (int neighbor : nodes[current].adjNodes) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    spanningTree.addEdge(current, neighbor);
                    q.push(neighbor);
                }
            }
        }
        return spanningTree;
    }
};

int main() {
    Graph g;

    // ��������� ����
    g.addNode(0);
    g.addNode(1);
    g.addNode(2);
    g.addNode(3);
    g.addNode(4);

    // ��������� ����
    g.addEdge(0, 1);
    g.addEdge(1, 2);
    g.addEdge(2, 3);
    g.addEdge(3, 4);
    g.addEdge(4, 0);

    // ������� ����
    cout << "Graph structure:\n";
    g.showGraph();

    // �������� �� ������� ����
    vector<int> eulerCycle = g.getEulerianCycle();
    if (!eulerCycle.empty()) {
        cout << "Eulerian cycle: ";
        for (int node : eulerCycle) {
            cout << node << " ";
        }
        cout << endl;
    } else {
        cout << "No Eulerian cycle found.\n";
    }

    // �������� �� ����������� ����
    vector<int> hamiltonCycle = g.getHamiltonianCycle();
    if (!hamiltonCycle.empty()) {
        cout << "Hamiltonian cycle: ";
        for (int node : hamiltonCycle) {
            cout << node << " ";
        }
        cout << endl;
    } else {
        cout << "No Hamiltonian cycle found.\n";
    }

    // ���������� ��������� ������
    Graph spanningTree = g.getSpanningTree();
    cout << "Spanning Tree structure:\n";
    spanningTree.showGraph();

    return 0;
}



```     
```

Graph structure:
Node 0: 1 4 
Node 1: 0 2 
Node 2: 1 3 
Node 3: 2 4 
Node 4: 3 0 
Eulerian cycle: 0 4 3 2 1 0 
No Hamiltonian cycle found.
Spanning Tree structure:
Node 0: 
Node 1: 
Node 2: 
Node 3: 
Node 4: 
```