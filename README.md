# Assignment-4
Project Overview
A Java implementation for scheduling city-service tasks using graph algorithms including Strongly Connected Components, Topological Sorting, and Shortest Paths in DAGs.

Features
Strongly Connected Components (Tarjan's algorithm)

Topological Sorting (Kahn's algorithm)

Shortest/Longest Paths in DAGs

Comprehensive performance metrics and analysis

Automated dataset generation

Project Structure
text
src/
├── main/java/graph/
│   ├── scc/          # Strongly connected components
│   ├── topo/         # Topological sorting
│   ├── dagsp/        # Shortest paths in DAGs
│   ├── model/        # Graph data structures
│   └── metrics/      # Performance metrics
├── test/java/graph/  # Unit tests
└── data/            # Graph datasets
Build & Run
Prerequisites
Java 11 or higher

Maven 3.6+

Installation
bash
git clone <repository-url>
cd smart-city-scheduler
Running the Application
bash
# Generate test datasets and run analysis
mvn compile exec:java -Dexec.mainClass="graph.SmartCityScheduler"

# Run only dataset generation
mvn compile exec:java -Dexec.mainClass="graph.DatasetGenerator"

# Run tests
mvn test
Running Individual Components
java
// Example usage in code
GraphData data = mapper.readValue(new File("data/tasks.json"), GraphData.class);
Graph graph = data.toGraph();

// SCC Analysis
TarjanSCC tarjan = new TarjanSCC(graph, new Metrics());
SCCResult sccResult = tarjan.findSCC();

// Topological Sort
TopologicalSort topo = new TopologicalSort(sccResult.condensationGraph, new Metrics());
TopoResult topoResult = topo.topologicalOrder();

// Shortest Paths
DAGShortestPath dagSP = new DAGShortestPath(graph, new Metrics());
ShortestPathResult spResult = dagSP.shortestPathFromSource(0);
Weight Model
This implementation uses edge weights as specified in the input JSON files. Edge weights represent dependencies or costs between tasks.

Input Format
JSON files in /data/ directory with structure:

json
{
  "directed": true,
  "n": 8,
  "edges": [
    {"u": 0, "v": 1, "w": 3},
    {"u": 1, "v": 2, "w": 2}
  ],
  "source": 4,
  "weight_model": "edge"
}
Output
The program generates comprehensive analysis including:

SCC components and sizes

Topological order of components

Shortest paths from source

Critical path (longest path)

Performance metrics (time, operations count)

Datasets
9 automatically generated datasets:

Small: 6-10 nodes (3 datasets)

Medium: 10-20 nodes (3 datasets)

Large: 20-50 nodes (3 datasets)

Each category includes cyclic and acyclic graphs with varying densities.

Testing
bash
# Run all tests
mvn test

# Run specific test class
mvn test -Dtest=GraphAlgorithmsTest
Dependencies
Jackson Databind (JSON processing)

JUnit 5 (testing)
