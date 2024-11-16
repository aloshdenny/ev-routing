# EV-Enrouting

### Find optimal path for electric vehicles using spatial information.

## Preprocessing

![Preprocessing](Images/x1_2.gif)

## Our Algorithm Solves Three Main Problems:
- Finding the Best Route
- Finding the Optimal Location to Set Up a Charging Station
- Dealing with Overhead on Charging Stations

### 1. Finding Best Route

#### a) Base Problem
Our algorithm identifies the best route that takes the shortest path among all available charging stations.

![Base Route](Images/x1_4.gif)

#### b) Now with Traffic Data
The benefit of this grid approach over a graph approach is that we can easily layer additional information, such as traffic data.

![Traffic Data](Images/x1_5.gif)

#### c) With Remaining Battery
By inputting available battery power, the algorithm informs us whether there are any charging stations within our battery limit. For example, with a remaining battery of 100 minutes, it may not show a path if all stations are out of range.

![Remaining Battery](Images/x1_8.gif)

Let's look at details of how it works:

![Algorithm Details](Images/x1_10.gif)

### 2. Finding Optimal Location to Set Up a Charging Station

Finding the optimal location for a charging station is complex and involves various factors such as demand and geographical feasibility. We applied three approaches:

- **a) Brute Force Approach:** We calculate total returns by placing a charging station at each point on a 50x50 grid, identifying the point with the maximum total return as optimal.
  
- **b) Sliding Window Technique:** A 10x10 window moves over the 50x50 matrix to calculate returns.
  
- **c) Sub-blocks Technique:** We divide the grid into four sub-grids (upper left, upper right, lower left, lower right) and calculate the return for the median point of each. This process repeats for the sub-grid with the maximum total return.

#### Optimality
- **Brute Force Approach > Sliding Window Technique > Sub-blocks Method**

#### Speed
- **Sub-blocks Method > Sliding Window Technique > Brute Force Approach**

(There is a trade-off between speed and optimality.)

![Sliding Window Technique](Images/x1_11.gif)
![Sliding Window with Traffic](Images/x1_13.gif)

Note: Due to traffic, the optimal charging station position may change, which makes sense.

### 3. Overhead on Charging Stations

We define two types of overhead on charging stations:
- **a) Dynamic Overhead:** Indicates the number of cars in queue and the wait time.
- **b) Static Overhead:** Average time required to charge a vehicle fully.

Together, these metrics help us find the best charging station at a given moment.

#### Case 1: Only Static Overhead

| Charging Station | Static Overhead | Travel Time | Total Time |
| :---: | :-: | :-: | :-: |
| Cs1   | 50  | 20  | 70  |
| Cs2   | 10  | 28  | 38  |
| Cs3   | 5   | 38  | 43  |

Our algorithm chooses: Cs2 >> Cs3 >> Cs1

![Static Overhead Verification](Images/x1_19.gif)

#### Case 2: Both Dynamic and Static Overhead

| Charging Station | Dynamic Overhead | Travel Time | Remaining Overhead | Static Overhead | Total Overhead | Total Time |
| :---: | :-: | :-: | :-: | :-: | :-: | :-: |
| Cs1   | 40  | 20  | 20  | 50  | 70            | 90         |
| Cs2   | 48  | 28  | 20  | 10  | 30            | 58         |
| Cs3   | 27  | 38  | 0   | 5   | 5             | 43         |

Our algorithm chooses: Cs3 >> Cs2 >> Cs1

In this case, we apply a greedy search, allowing us to find the optimal charging station without calculating travel time for each one. Greedy search provides an optimal solution, as detailed in the report.

![Dynamic and Static Overhead](Images/x1_16.gif)

## Theory

[Theory Notebook](https://colab.research.google.com/drive/1zSd24UZs3tKTVcDbJ61VH8CpsZ8QZA8d?usp=sharing)
