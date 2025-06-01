# Multi-Controlled-U-Gate

This is a mini-project for the summer-2025-quantum-computing Boot Camp in the Erdos Institute. 

## Mini-projet #2: Multi-Controlled U Gate

Write a Qiskit function that takes two inputs: a positive integer $n$ and a matrix $U\in U(2)$ and outputs a quantum circuit on $n+1$ qubits, possibly with further ancillas, that implements a multi-controlled $U$ gate, $C^nU$, that is 
 
$$C^nU|x\rangle_n |y\rangle_1 = \begin{cases}
|x\rangle_n U |y\rangle_1, & \mathrm{if}\, \, x=(1,1,\ldots, 1)\\
|x\rangle_n |y\rangle_1, &\mathrm{otherwise}.
\end{cases}$$

The construction may only use arbitrary 1-qubit gates and $CX$ gates. No classical bit and measurements allowed. 


## Solutions:

We follow the method outlined in Chapter 4 in the textbook "_Quantum Computation and Quantum Information_" by Michael A. Nielsen and Isaac L. Chuang. 

The basic idea is shown in the schematic figure with $5$ control qubits as an example (Figure 4.10. in the textbook). <img src="https://github.com/user-attachments/assets/54c503e9-53ab-43c7-9dde-31f1429a596e" width="700" height="400" />

The chain of Toffoli gates for successive pairs of one control qubit and one ancillary qubit makes sure that the last ancillary qubit is $|1\rangle$ only when all the control qubits are $|1\rangle$. After applying the single controlled $U$ gate, controlled by the last ancillary qubit, one needs to reverse all the Toffoli gates so that the ancillary qubits return to their original states $|0\rangle$.  

**For general $n$ control qubits, one needs $n-1$ ancillary qubits. There are $2(n-1)$ Toffoli gates and a single-controlled-U gate in the construction.** 

#### Toffoli gate:

The Toffoli gate can be constructed using single qubit gates and CNOT gate by (Figure 4.9. in the textbook)
<img src="https://github.com/user-attachments/assets/23385c48-255b-4b8e-a551-e304c6730c41" width="700" height="200" />

In this implementation, one only needs the CNOT gate, the Hadmard gate, $T$ gate, $T^{\dagger}$ gate and $S$ gate. 

#### CU gate:

The single qubit controlled $U$ gate $CU$ can be implemented according to (Figure 4.6. in the textbook)
<img src="https://github.com/user-attachments/assets/63751db4-efb8-4b74-b143-3e594f8912ce" width="600" height="200" />

This is because for a general $2\times 2$ unitary matrix $U$, it can be decomposed as $U=e^{i\alpha} R_z(\beta) R_y(\gamma) R_z(\delta)$ in terms of three angles $\beta, \gamma, \delta$ and one overall phase $\alpha$. $R_z(\beta)$ is rotation around direction set by the Pauli $Z$ matrix. $R_y(\gamma)$ is the rotation around direction set by the Pauli $Y$ matrix. 

It is also been explicitly proved in the textbook that the unitary matrix $U$ can also be expressed as $U =  e^{i\alpha} AXBXC$ with $A = R_z(\beta) R_y(\gamma/2)$, $B=R_y(-\gamma/2)R_z(-(\delta+\beta)/2)$, $C=R_z((\delta-\beta)/2)$. Here $X$ is the Pauli $X$ matrix. 

**In the Jupyter notebook, I implement the Toffoli gate, the single controlled U gate and then the multi-controlled U gate.**

In fact, in Qiskit, for arbitrary given $2\times 2$ unitary matrix $U$, one can construct multi-controlled U gate using the gate method _".control(n)"_. The codes are tested against this built-in method for arbitrary unitary matrix $U$ and some representative input qubits. 

### Analysis of Complexities and Resources
|Metric              |Complexity          |
|--------------------|--------------------|
|Number of Ancillas  |$O(n)$              |
|Gate Count          |$O(n)$              |
|Gate Depth          |$O(n)$              |

