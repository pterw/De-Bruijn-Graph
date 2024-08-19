# De Bruijn Graph Generator

This project demonstrates the construction of a De Bruijn graph from k-mers. 
A De Bruijn graph is used in bioinformatics to assemble genomes from short DNA sequences.

## Features

- Generate a De Bruijn graph from a list of k-mers.
- Visualizes the graph using Graphviz.
- Find and check for Eulerian paths in the graph.

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/De-Bruijn-Graph.git
    cd De-Bruijn-Graph
    ```

2. Install the required Python packages:
    ```bash
    pip install -r requirements.txt
    ```

3. Ensure that Graphviz is installed and added to your system's PATH.

## Usage

### Running the Python Script

You can generate a De Bruijn graph using the Python script with either direct input of k-mers or using an input file.

**Direct Input:**
```bash
python de_bruijn_graph.py --kmers AAA AAG AGC AGT
```

**File Input**
```bash
python de_bruijn_graph.py --input_file examples/kmers_example.txt
```
