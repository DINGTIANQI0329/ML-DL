## 📜 Viterbi Algorithm and HMM Visualization (Matlab)

This project implements the classic **Viterbi Algorithm** in the **Matlab** environment to solve the **Decoding Problem** of a Hidden Markov Model (HMM)—that is, finding the **single most likely sequence of hidden states** that produced a given sequence of observations. The project also includes robust visualization functionality to display the algorithm's dynamic programming process and the optimal path in a **Trellis Diagram**.

### ✨ Key Features

* **Efficient Implementation**: Calculations are performed in **Log-Space** to effectively solve the common problem of **Numerical Underflow** in HMM algorithms.
* **Vectorization**: The core recursive step of the Viterbi algorithm uses **Matlab vectorization** for improved computational efficiency.
* **Visualization**: The `plot_viterbi_trellis.m` function draws an interactive trellis diagram, clearly showing:
    * The **Log Probability of the Optimal Path** to each node (distinguished by color and size).
    * The **Backpointer ($\psi$)** connections.
    * The trajectory of the **Best Path**.
    * Clicking on a node displays detailed information (time, state, log probability, and predecessor state).
* **Classic Example**: Includes the standard **"Weather and Activities"** prediction model to demonstrate the algorithm's flow.

### 📁 File Structure

| Filename | Description |
| :--- | :--- |
| `viterbi_custom.m` | **Core Algorithm**. Implements the vectorized Viterbi algorithm using log probabilities, returning the best path, path probability, the Viterbi matrix ($\delta$), and the backpointer matrix ($\psi$). |
| `plot_viterbi_trellis.m` | **Visualization Function**. Generates the interactive trellis diagram based on the output data from the Viterbi algorithm. |
| `Example.m` | **Basic Example Script**. Defines the HMM parameters, calls `viterbi_custom` for decoding, and prints the results. |
| `Visualization.m` | **Visualization Demo Script**. Based on `Example.m` parameters, it calls both `viterbi_custom` and `plot_viterbi_trellis` to generate and display the trellis diagram. |

### 🛠️ How to Run

1.  Place all `.m` files in your Matlab working directory.
2.  Open the **Matlab** software.
3.  To run the basic decoding example, type the following in the command window:
    ```matlab
    Example
    ```
    The expected output is the most likely hidden state sequence (`Sunny -> Rainy -> Rainy`) for the observation sequence (`Walk -> Shop -> Clean`).
4.  To run the visualization example with the trellis diagram, type:
    ```matlab
    Visualization
    ```
    This will open an interactive Viterbi Trellis Diagram window.

### 📚 Theoretical Background (from Slides)

The Viterbi algorithm is a method based on **Dynamic Programming** used to efficiently solve the HMM decoding problem.

* **Problem**: Given an observation sequence $O$, find the most probable state sequence $Q^*$: $Q^{*}=arg~max_{Q}P(Q|O,\lambda)$.
* **Dynamic Programming**: Avoids the brute-force search of $K^T$ paths. By storing only the optimal sub-path ($V_t(j)$) and its predecessor state ($\psi_t(j)$) for reaching each state $s_j$ at time $t$, it achieves an $O(K^2T)$ time complexity.
* **Log-Space**: To prevent numerical underflow caused by multiplying many small probabilities, calculations are performed in logarithmic space:
    $$\log(V_t(j)) = \max_{i=1}^K[\log(V_{t-1}(i)) + \log(A_{ij})] + \log(B_{j}(o_t))$$
