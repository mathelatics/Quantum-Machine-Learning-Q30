# The Development of Shor's Algorithm and Error Correction by Peter Shor

Introduction

In 1981 at CalTechFeymann published a paper on Negative Probability to avoid infinities from renormalization : Quantum Mechanics. and at that time Peter Shor a Graduate Students at the caltech.

Feymann In a conference talk about the Bell's Theorem, he said EPR paradox are unavoidable i.e Quantum Mechanics can't be local and realistic( ? ), assumption all probabilites of observables between [0,1]. 

Charlie Bennett at Bell Lab 1986 after BB84 , 1984 QKD in 1991 aperatus. Is there any way to prove mathematically that this QKD Protocol is secure ?

Jorhn Preskill and Peter Shor in 2000 gave a simple proof of security of the BB84 QKD: Quantum Information, Quantum Error Correction, Quantum Computation.

Umesh Vazirani at Bell Labs in 1992 : Talk on Bernsein and Vazirani - Put Quantum Turing Machine into a Mathematically regorous framework i.e a algorithm for constarained problems i.e Bernstein Vazirani Problem which run faster on Quantum Turing Machine compared to classical machine.

Simon's Problem : Finding the period on the vertices of the high dimensional cube ?

3 -500 dim cube : function on vertices of cube with property that go into screen and move horizontely then you will see the same color vertices. means colors of vertices are periodic $f(x+T) = f(x)$ he overcome with this problem by applying fourier transform on binary vector space.

Fourier Transform is good at periodic function to find period and Discrete Log problem is also has properties of periodicity used in Public Key Cryptosystems like diffie-hellman and RSA

Discrete Log Problem : Finding period on a large torus(topological) not cube. How to take Fourier Transfrom on Quantum Computers for Exponentially large period then he find how to apply and figure out discrete log problem solve. and after he solve the factoring problem

Discrete Log and Factoring Algorithms are used in public key cryptosystem can be solved by the shor's algorithm. How to factor large number on Quantum Computer told to Umesh Vazirani.

Shor's Algorithm

We are going to construct a set of functions to implement the shor's algorithm using Qiskit. Then Question arises what is the goal of the Shor's algorithm. It is used to find the prime factors of larger numbers and speedup for this algorithm by executing the period finding using Quantum fourier transfrom on the quantum computer.

Steps for Shor's Algorithm

1. Choose a co-prime $a$, where $a\in [2,N-1]$ and the greatest common divisor of $a$ and $N$ is 1.
2. Find the order (periodicity) of $a$ modulo $N$, i.e. the smallest integer $r$ such that $a^r\text{mod} N=1$
3. Obtain the factor of $N$ by computing the greatest common divisor of $a^{r/2} \pm1$ and $N$.
