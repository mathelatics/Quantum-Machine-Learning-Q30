Quantum Encoding - It is the encoding(storage) of classical information into quantum states such that we can perform quantum model like quantum circuits on it to get the desired results.

The Properties of the quantum encoding like No-Cloning Theorem are the fundamentally importent for the quantum computing, quantum communication, quantum cryptography and quantum machine learning etc.

How to load and retrieve data from the quantum computer i.e Input/Output Interface of quantum computer ?

What is quantum data ?

Quantum data is the quantum states which is generated by quantum processes like Quantum Circuit, Quantum Communication Channel like Quantum Internet, Density Matrix of our quantum experiment data.

How can we represent and store data as quantum states i.e encoding data into quantum computer ?

There are the two possible ways of quantum encoding

1. Binary(Basis) Encoding - Storage of each bit into the state of qubit. Numbers can be stored as binary encoding
2. Amplitude Encoding - Storage of the data into amplitude of quantum states. thus, we can encode n real values using $O(\lceil log n \rceil)$ qubits.
3. Probability Distribution - Given a probability distribution $p$ on a finite set $X$, encoded state

$$
\begin{equation}
|\psi_p \rangle = \sum_{x \in X} \sqrt{p(x) \ket x} \in \mathbb{H}
\end{equation}
$$

where $ \{\ket x\}_{x \in X}$ is an orthonormal basis of $|X|-dim$ Hilbert Space $\mathbb{H}$. Thus repeated measurement on the $| \psi_p \rangle$ w.r.t computational basis allow to sample teh distribution p.

Quantum States :
Quantum Registers :

Let $x \in \mathbb{N}$, how to represent it into quantum computer ?, lets consider a binary expansion as list of $n$ bits for $x$. Thus the state of the $i^{th}$ Qubit as teh value of the $i^{th}$ bit of $x$.

$$
\begin{equation}
|x \rangle =  \bigotimes_{i=0}^{m} | x_i \rangle
\end{equation}
$$

We needed to work with the larger number but not only integers but also reals and complex numbers thus we can represent them with decimal number with certain bit precision. Thus we can use some special bit to store sign, Real Numbers - Integral Parts and Decimal Part and Complex Number - Real Part and Complex Part with $i = \sqrt -1$.

**No-Cloning Theorem** :

- A quantum cloner(quantum cloning machine) is a composite quantum system described into the Hilbert Space $\mathbb{H} \otimes \mathbb{H}$ such that there is a state $\ket \eta \in \mathbb{H}$ and a unitary operator $U$ satisfying 
  $$
  U\ket {\psi \eta} = \ket {\psi \psi} \; \forall \; \ket \psi \in \mathbb{H}
  $$

  .Hence a quantum cloner is with the characterisitcs of the time evolution that duplicates the state of a quantum subsystem into the state of the other subsystem prepared in the blank state $\ket \eta$.