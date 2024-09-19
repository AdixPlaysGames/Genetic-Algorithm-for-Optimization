# Genetic Algorithm for Optimization

This repository implements a genetic algorithm designed to optimize the placement of rectangles within a circle. The goal is to maximize the total value of the rectangles placed inside the circle without overlap. Each rectangle has a width, height, and associated value. The algorithm considers the orientation (horizontal or vertical) and aims to find the most valuable arrangement.

## Features

- **Efficient Optimization**: Utilizes a genetic algorithm for effective searching of the optimal placement.
- **Customizable Parameters**: Adjust population size, number of generations, and mutation rates.
- **Collision Detection**: Ensures rectangles do not overlap and fit within the circle.
- **Value Maximization**: Prioritizes placement of rectangles with the highest value-to-area ratio.
- **Orientation Handling**: Supports both horizontal and vertical orientations for rectangles.
- **Visualization**: Provides graphical representation of the final optimized placement.

## How It Works

### 1. Value to Area Ratio

The algorithm starts by calculating the value-to-area ratio for each rectangle to prioritize rectangles that offer the most value per unit area.

$$
\text{Value-to-Area Ratio} = \frac{\text{Value}}{\text{Width} \times \text{Height}}
$$

### 2. Initialization of Population

An initial population of potential solutions (individuals) is generated. Each individual is a list of rectangles placed at random positions and orientations within the circle.

- **Population Initialization**:
  - Sort rectangles by their value-to-area ratio in descending order.
  - For each individual:
    - Randomly select a number of rectangles.
    - For each rectangle:
      - Randomly assign position \( (x, y) \) within the circle.
      - Randomly assign orientation (horizontal or vertical).

### 3. Collision Detection

To ensure that rectangles do not overlap, the algorithm checks for collisions between rectangles using their positions and dimensions.

- **Collision Check between Two Rectangles**:

  Two rectangles \( R1 \) and \( R2 \) collide if:

$$
\text{Fitness}(I) = \sum_{i \in I} {\text{Value}_i} \cdot \mathrm{inside}(i) \cdot \mathrm{no\_collision}(i)
$$

  Where $$\ x_{\text{min}} \$$ and $$\ x_{\text{max}} \$$ are the minimum and maximum x-coordinates of the rectangle, respectively.

### 4. Fitness Evaluation

The fitness of an individual is evaluated based on the total value of the rectangles that are within the circle and do not overlap with others.

- **Fitness Function**:

$$
\text{Value-to-Area Ratio} = \frac{\text{Value}}{\text{Width} \times \text{Height}}
$$

  Where:

- inside(i) = 1, if rectangle i is inside the circle, else 0.
- no_collision(i) = 1, if rectangle i does not collide with others, else 0.

### 5. Genetic Operators

#### Mutation

Random modifications are applied to individuals to maintain genetic diversity.

- **Mutation Types**:
  - **Add**: Attempt to add a new rectangle near the center.
  - **Remove**: Remove a random rectangle.
  - **Move**: Slightly adjust the position of a rectangle.
  - **Orient**: Change the orientation of a rectangle.

#### Crossover

Combines two parent individuals to produce offspring.

- **Single Point Crossover**:
  - Select a random crossover point.
  - Child 1: Inherit genes from Parent 1 up to the point, then from Parent 2.
  - Child 2: Inherit genes from Parent 2 up to the point, then from Parent 1.

### 6. Selection and Evolution

The algorithm iteratively evolves the population over a number of generations.

- **Selection**:
  - Sort individuals by fitness.
  - Select the top individuals to form the next generation.
- **Evolution Loop**:
  - **For** each generation:
    - **Selection**: Choose the fittest individuals.
    - **Crossover**: Generate new offspring.
    - **Mutation**: Apply mutations to offspring.
    - **Replacement**: Form the new population.

### 7. Positioning Near Center

To maximize value, the algorithm attempts to place new rectangles near the center of the circle, where there is more space.

- **Positioning Strategy**:
  - Start from the center and spiral outward.
  - Check for available space without collisions.

## Usage

1. **Define Rectangles**: Prepare a list of rectangles with their width, height, and value.
2. **Set Parameters**: Choose population size, number of generations, and circle radius.
3. **Run the Algorithm**: Execute the genetic algorithm function with the defined parameters.
4. **Visualize**: Use the provided plotting function to visualize the best arrangement.

## Mathematical Formulas

### Inside Circle Check

To verify if a rectangle is entirely inside the circle:

For all four corners \( (x_i, y_i) \) of the rectangle:

$$
(x_i)^2 + (y_i)^2 \leq R^2
$$

Where \( R \) is the circle radius.

### Angle Calculation for Movement

When mutating the position of a rectangle:

$$
\theta = \arctan\left( \frac{y}{x} \right)
$$

New position after moving a step \( s \):

$$
\begin{align*}
x_{\text{new}} &= x - s \cos(\theta) \\
y_{\text{new}} &= y - s \sin(\theta)
\end{align*}
$$

## Visualization

The visualization function generates a graphical representation using plotting libraries:

- **Circle**: Represents the boundary within which rectangles must be placed.
- **Rectangles**: Plotted with their positions, sizes, and orientations.
- **Value Labels**: Display the value of each rectangle at its center.

## Conclusion

This genetic algorithm efficiently optimizes the placement of rectangles within a circle, maximizing the total value while ensuring no overlaps occur. The combination of strategic initialization, mutation, and crossover operations allows for exploring a wide solution space to find an optimal or near-optimal arrangement.
