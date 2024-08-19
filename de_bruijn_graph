import argparse
from collections import defaultdict
from graphviz import Digraph
import copy

# function to generate De Bruijn graph
def make_graph(k_mers):
    nodes = defaultdict(list)
    
    for kmer in k_mers:
        head = kmer[:-1]
        tail = kmer[1:]
        nodes[head].append(tail)
        
    return nodes

# function to visualize the graph using Graphviz
def visualize_graph(nodes, filename="de_bruijn_graph"):
    dot = Digraph(comment='debruijn')
    
    for km1mer in nodes:
        dot.node(km1mer, km1mer)
        
    for src in nodes:
        ends = nodes[src]
        for end in ends:
            dot.edge(src, end)
    
    dot.format = 'png'
    dot.render(filename, view=True)

# function to list all directed edges of the graph
def edges(graph):
    for node in graph:
        for target in graph[node]:
            yield (node, target)

# function to check if a tour is Eulerian
def follow_tour(tour, graph):
    edges_ = list(edges(graph))
    for start, end in zip(tour, tour[1:]):
        try:
            edges_.remove((start, end))
        except:
            return False
    return not edges_

# function to find and check the tour
def check_tour(start, graph):
    our_tour = tour(start, graph)
    valid_tour = follow_tour(our_tour, graph)
    return valid_tour, "".join(s[0] for s in our_tour)

# function to find an eulerian cycle or trail
def tour(start_node, graph):
    graph = copy.deepcopy(graph)
    return _tour(start_node, graph)

def _tour(start_node, graph, end=None):
    tour = [start_node]
    finish_on = end if end is not None else start_node
    while True:
        options = graph[tour[-1]]
        if not options:
            break
        tour.append(options.pop())
        if tour[-1] == finish_on:
            break
    offset = 0
    for n, step in enumerate(tour[:]):
        options = graph[step]
        if options:
            t = _tour(options.pop(), graph, step)
            n += offset
            tour = tour[:n + 1] + t + tour[n + 1:]
            offset += len(t)
    return tour

# main function to handle user input and execute the graph generation and tour check
def main():
    parser = argparse.ArgumentParser(description="Generate a De Bruijn graph from k-mers and check for Eulerian paths.")
    
    # accept k-mers directly as command-line arguments
    parser.add_argument('--kmers', nargs='+', help="List of k-mers to build the De Bruijn graph.")
    
    # or accept a file with k-mers
    parser.add_argument('--input_file', type=str, help="Path to a file containing k-mers (one per line).")
    
    args = parser.parse_args()

    if args.kmers:
        k_mers = args.kmers
    elif args.input_file:
        with open(args.input_file, 'r') as file:
            k_mers = [line.strip() for line in file]
    else:
        print("Please provide k-mers either through command-line or an input file.")
        return

    # generate and visualize the de bruijn graph
    graph = make_graph(k_mers)
    visualize_graph(graph)

    # check and print eulerian tour from a start node (example: 'AG')
    tour_result = _tour('AG', graph)
    print(f"Eulerian Tour starting from 'AG': {tour_result}")

if __name__ == "__main__":
    main()