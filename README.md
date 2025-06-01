# Multi-Controlled-U-Gate

This is a mini-project for the summer-2025-quantum-computing Boot Camp in the Erdos Institute. 

### Mini-projet #2: Multi-Controlled U Gate

Write a Qiskit function that takes two inputs: a positive integer $n$ and a matrix $U\in U(2)$ and outputs a quantum circuit on $n+1$ qubits, possibly with further ancillas, that implements a multi-controlled $U$ gate, $C^nU$, that is 
 
$$C^nU|x\rangle_n |y\rangle_1 = \begin{cases}
|x\rangle_n U |y\rangle_1, & \mathrm{if}\, \, x=(1,1,\ldots, 1)\\
|x\rangle_n |y\rangle_1, &\mathrm{otherwise}.
\end{cases}$$

The construction may only use arbitrary 1-qubit gates and $CX$ gates. No classical bit and measurements allowed. 


### Solutions:

We follow the method outlined in Chapter 4 in the textbook "_Quantum Computation and Quantum Information_" by Michael A. Nielsen and Isaac L. Chuang. 

The general idea is shown in the schematic figure with $5$ control qubits (Figure 4.10. in the textbook). <img src="https://github.com/user-attachments/assets/54c503e9-53ab-43c7-9dde-31f1429a596e" width="800" height="600" />

For general $n$ control qubits, one needs $n-1$ ancillary qubits. There are $2(n-1)$ Toffoli gates and a single-controlled-U gate in the construction. 
