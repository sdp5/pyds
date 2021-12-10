# Graph

```python

#!/usr/bin/env python3

class GraphNode(object):

    data = None
    edges = None

    def __init__(self, data):
        self.data = data
        self.edges = []


class GraphEdge(object):

    weight = None
    start = None
    end = None

    def __init__(self, weight):
        self.weight = weight


class Graph(object):

    latest_edge = None
    graph_elements = dict()

    def add_edge(self, start, end, weight):
        if start not in self.graph_elements:
            start_node = GraphNode(start)
            self.graph_elements[start] = start_node
        else:
            start_node = self.graph_elements[start]

        if end not in self.graph_elements:
            end_node = GraphNode(end)
            self.graph_elements[end] = end_node
        else:
            end_node = self.graph_elements[end]

        edge = GraphEdge(weight)
        edge.start = start_node
        edge.end = end_node

        start_node.edges.append(edge)
        end_node.edges.append(edge)

        self.latest_edge = edge

    def print_nodes(self):
        for id, node in self.graph_elements.items():
            print("\n{}".format(node.data))
            for edge in node.edges:
                print("  {} <--> {} ({})".format(edge.start.data, edge.end.data, edge.weight))

    def print_graph(self):
        if not self.latest_edge:
            print("The graph is empty.")
        self.print_nodes()

    def get_paths(self, orig, dest, path=[]):
        if orig not in self.graph_elements and dest not in self.graph_elements:
            return []

        path = path + [orig]

        if orig == dest:
            return [path]

        paths = []

        orig_node, dest_node = self.graph_elements[orig], self.graph_elements[dest]
        for edge in orig_node.edges:
            if edge.end.data not in path:
                new_paths = self.get_paths(edge.end.data, dest_node.data, path)
                for p in new_paths:
                    paths.append(p)

        return paths


if __name__ == "__main__":

    g_obj = Graph()
    g_obj.add_edge("Mumbai", "Delhi", 1800)
    g_obj.add_edge("Mumbai", "Kolkata", 2200)
    g_obj.add_edge("Mumbai", "Bangalore", 1000)
    g_obj.add_edge("Delhi", "Bangalore", 2500)
    g_obj.add_edge("Kolkata", "Bangalore", 1400)
    g_obj.add_edge("Bangalore", "Chennai", 400)
    g_obj.add_edge("Delhi", "Pune", 1700)
    g_obj.add_edge("Kolkata", "Pune", 2000)
    g_obj.add_edge("Pune", "Chennai", 2600)

    g_obj.print_graph()

    orig = "Delhi"
    dest = "Bangalore"
    print(f"\nPaths between {orig} and {dest}: ", g_obj.get_paths(orig, dest))


```