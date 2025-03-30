# ME5413_HW3

This file implements path planning and Traveling Salesman Problem (TSP) solutions on a map using various search algorithms. Below is a detailed explanation of each major part of the code and its purpose.

## 1. Importing Libraries and Loading Map Data

- **Library Imports**:  
  The script imports libraries such as `numpy`, `imageio`, and `matplotlib.pyplot` for image processing and numerical computations.

- **Loading Map Images**:  
  It loads two images:  
  - A detailed map image (e.g., a floor plan).  
  - A binary (grayscale) map where white (`255`) represents free space and black (`0`) represents obstacles.  
  The code prints out the map’s dimensions, as well as the count of occupied and free cells to verify the data.

## 2. Map Settings and Marking Locations

- **Map Resolution**:  
  The resolution is defined (each grid cell represents a 0.2m x 0.2m area).

- **Key Locations**:  
  A dictionary of key locations is defined (e.g., start, snacks, store, movie, food). These represent specific points on the map for path planning.

- **Plotting Function**:  
  The `plot_locations` function is defined to mark these key points on the map with markers and labels.

## 3. A* Algorithm and Obstacle Inflation

### 3.1 Obstacle Inflation

- **Purpose**:  
  To account for the robot's or person's physical size (e.g., a 0.3m radius), obstacles are “inflated” so that the resulting path avoids areas too close to obstacles.

- **Implementation**:  
  A circular structuring element (kernel) is created based on the inflation radius, and `binary_dilation` is used to expand the obstacles, creating an inflated grid map.

### 3.2 Heuristic Functions

- **Heuristic Options**:  
  The code supports different heuristic types (`manhattan`, `euclidean`, `chebyshev`, and `custom`) which are used by the A* algorithm to estimate distances.

### 3.3 A* Path Planning

- **A* Function**:  
  The `astar` function implements the A* search algorithm. It finds the optimal path between two points by considering both the cost so far and the heuristic estimate to the goal.
  
- **Visualization**:  
  The planned path and the visited cells during the search are displayed on the map using Matplotlib.

## 4. TSP Solving Using A* Algorithm

- **Distance Matrix Construction**:  
  The script computes a distance matrix between all key locations using the A* algorithm. It stores the shortest path, cost, visited cells, and runtime for each segment.

- **TSP Solution**:  
  Using brute-force (permuting all orders of visits), the code finds the optimal circuit route that starts and ends at the designated start location while visiting all other locations.
  
- **Detailed Segment Information**:  
  For each segment of the TSP route, the script outputs details such as path length, number of visited cells, and runtime. It also plots the complete TSP route on the map.

## 5. Greedy Best-First Search (GBFS) Algorithm

- **GBFS Implementation**:  
  A separate `greedy_best_first_search` function is implemented. Unlike A*, GBFS only uses the heuristic value for prioritizing nodes without adding the cost-so-far.
  
- **Distance Matrix and TSP**:  
  Similar to the A* section, the script builds a distance matrix using GBFS, solves the TSP, outputs segment details, and visualizes the optimal route.

## 6. Dijkstra’s Algorithm

- **Dijkstra Implementation**:  
  The `dijkstra_search` function is provided. Dijkstra’s algorithm is used to compute the shortest paths by considering only the accumulated cost, with no heuristic component.

- **Distance Matrix and TSP**:  
  Again, the script computes the distance matrix among key locations using Dijkstra’s algorithm, solves the TSP, and displays detailed information and visualizations of the resulting route.

## 7. Comparison of Multiple TSP Solving Methods

Besides using the above algorithms for TSP, the code also implements three additional TSP methods:

- **Brute-Force Method**:  
  Evaluates all possible permutations of the route to select the shortest circuit.

- **Nearest-Neighbor Method**:  
  Uses a greedy strategy by always moving to the closest unvisited location until all have been visited, then returning to the start.

- **Held-Karp Dynamic Programming**:  
  An optimized TSP solution using dynamic programming with memoization.

For each method, the script prints the route and total distance, and plots the corresponding route on the map for visual comparison.

## 8. Summary

- **Overall Functionality**:  
  The code demonstrates how to perform path planning on a real map using image processing and various search algorithms (A*, GBFS, Dijkstra’s).
  
- **TSP Problem Solving**:  
  It extends the single-path planning to solve the TSP by constructing a full distance matrix among key locations and applying multiple algorithms to find the optimal circuit route.
  
- **Visualization and Analysis**:  
  Detailed outputs and graphical visualizations help in analyzing performance (e.g., number of visited cells, runtime) and comparing different algorithmic approaches.

---

This comprehensive explanation covers the main components and functionalities of the code, providing insights into both its design and practical implementation.

