# Cone Optimization using Genetic Algorithms

This project focuses on optimizing the dimensions of a cone (radius and height) using genetic algorithms. The goal is to explore multi-objective optimization techniques to find a set of optimal cone designs that balance conflicting objectives, such as maximizing volume while minimizing surface area.

## Problem Description

The cone optimization problem involves finding the optimal dimensions for a cone, specifically its radius (r) and height (h). The optimization process aims to satisfy certain objectives and constraints:

- **Variables:**
    - Radius (r)
    - Height (h)
- **Objectives:**
    - Minimize Surface Area (S) = π * r * l (where l is the slant height, l = sqrt(r^2 + h^2))
    - Minimize Total Surface Area (T) = π * r * (r + l)
- **Constraints:**
    - Volume (V) > 200 (V = (1/3) * π * r^2 * h)

## Methods

This project explores two approaches to solve the cone optimization problem:

### Method 1: Solution using `pymoo` library

This method utilizes the `pymoo` library, a powerful framework for multi-objective optimization in Python.
It employs the NSGA-II (Non-dominated Sorting Genetic Algorithm II) algorithm, a widely used evolutionary algorithm for multi-objective optimization.
A custom problem class, `Cones`, is defined, inheriting from `pymoo.core.problem.Problem`. This class encapsulates the cone optimization problem, including the definition of variables, objectives, and constraints.

### Method 2: Solution implemented from scratch

This method involves building a genetic algorithm from the ground up. The core components of this custom GA are:

-   **`Individual` class:** Represents a candidate solution (a cone). Each individual's chromosome includes its radius, height, and strategy parameters for self-adaptive mutation. The class also handles the calculation of the objective functions (Surface Area S and Total Surface Area T) and checks for feasibility (Volume V > 200).
-   **Mutation:** A self-adaptive mutation strategy is implemented. This means that the mutation strength (strategy parameters) co-evolves with the solutions, allowing the algorithm to dynamically adjust the mutation operator.
-   **Crossover:** Two types of crossover operators are used:
    -   Blend Crossover (BLX-α): Creates new individuals by taking a weighted average of the parent's genes.
    -   Whole Arithmetic Crossover: Computes the arithmetic mean of the two parent chromosomes.
-   **Parent Selection:** Linear ranking based on the `num_dominated` count (the number of individuals in the population that dominate a given individual) is used to select parents for reproduction. Individuals with lower `num_dominated` values (less dominated) have a higher chance of being selected.
-   **Survival Selection:** A combination of elitism and selection from the combined population is used. Non-dominated individuals from the parent generation are automatically carried over to the next generation (elitism). The remaining slots in the new generation are filled by selecting the best individuals from the combined pool of parents and offspring, based on their non-domination rank and crowding distance.

## Project Structure and Files

The repository contains the following key files and directories:

*   `Assignment2.pdf`: The original assignment document outlining the problem, objectives, and constraints.
*   `Assignment2_Solution.ipynb`: A Jupyter Notebook that serves as the main codebase. It includes the problem definition, the implementation of both the `pymoo`-based solution (Method 1) and the custom genetic algorithm (Method 2), as well as code for running the optimizations, and visualizing the results (e.g., Pareto fronts).
*   `Assignment2_Solution_Report.pdf`: A PDF document providing a detailed report of the project, likely including the methodology, results, analysis, and conclusions drawn from the optimization experiments.
*   `pareto_front_per_generation_NSGA2.mp4`: A video file visualizing the evolution of the Pareto front across generations for the NSGA-II algorithm implemented using the `pymoo` library.
*   `pareto_front_per_generation_my_implementation.mp4`: A video file visualizing the evolution of the Pareto front across generations for the custom-implemented genetic algorithm.
*   `README.md`: This document, providing an overview of the project, its structure, and how to understand its components.

## How to Run

The primary way to execute the code and explore the solutions is through the Jupyter Notebook:

1.  Ensure you have a Python environment with Jupyter Notebook or JupyterLab installed.
2.  Clone or download this repository to your local machine.
3.  Navigate to the repository's directory.
4.  Launch Jupyter Notebook or JupyterLab.
5.  Open the `Assignment2_Solution.ipynb` file.
6.  You can then run the cells in the notebook sequentially to execute the code for problem setup, genetic algorithm implementations, optimization runs, and result visualizations.

### Dependencies

The Python libraries required to run the notebook are listed below. You can install them using pip.

```bash
pip install numpy matplotlib tqdm pickle pymoo pyrecorder
```

*   **numpy:** For numerical operations.
*   **matplotlib:** For plotting graphs and visualizations.
*   **tqdm:** For displaying progress bars during iterative processes.
*   **pickle:** For saving and loading Python objects (used for storing results).
*   **pymoo:** For the NSGA-II based multi-objective optimization (Method 1).
*   **pyrecorder:** Used for creating video recordings of the Pareto front evolution.

## Results

The primary output of the optimization algorithms is a set of non-dominated solutions, forming the Pareto front. These fronts represent the trade-offs between the conflicting objectives (minimizing surface area S and total surface area T) under the given volume constraint.

The evolution of these Pareto fronts over generations is visualized in the following video files:

*   `pareto_front_per_generation_NSGA2.mp4`: Shows the convergence of the Pareto front for the solution using the `pymoo` library (NSGA-II algorithm).
*   `pareto_front_per_generation_my_implementation.mp4`: Shows the convergence of the Pareto front for the custom-implemented genetic algorithm.

These videos demonstrate how the genetic algorithms progressively refine the population of solutions, converging towards the optimal set of cone dimensions that offer the best possible compromises between the objectives. Detailed analysis and comparison of the results from both methods can be found in the `Assignment2_Solution.ipynb` notebook and the `Assignment2_Solution_Report.pdf`.

## Contributing

Contributions to this project are welcome. If you have suggestions for improvements or find any issues, please feel free to open an issue or submit a pull request.

## License

This project is currently not under a specific license. Please contact the author(s) for licensing information.
