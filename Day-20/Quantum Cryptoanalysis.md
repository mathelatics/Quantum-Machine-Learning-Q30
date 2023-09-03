# Quantum Crypto-analysis

Quantum Algorithms

1. Shor's Quantum Factoring Algorithm (1994) :
   - Factoring an integer N in $O((logN)^3).$
   - Best classical algorithm's(General Number Field Sieve) upper bound is $O(N^{1/2})$.
   - Shor's Algorithm provides the exponential speed-up as compared to classical existing algorithms.
   - Shor's Algorithms are also applicable in many places like Crypto-anaysis of the public key crypto-systems like Diffie Hellman, RSA etc.
2. Grover's Quantum Search algorithm (1996) :
   - For any function $f: [N] \to \{0, 1\}$, find $x \in [N]$ s.t $f(x) = 1$ is $O(\sqrt N)$ evaluation of f with high probability.
   - Best Classical Algorithm Upper Bound $O(N)$
   - Grover's Algorithm provides Quandratic SpeedUp as compared to the classical existing algorithms.
   - Grover's algorithm applicable in many places for search problems.
   - The best attack on crypto-system with polynomial speed-ups with key sizes.

Techniques for designing of Quantum Algorithms

1. Quantum Search(Amplitude Amplification)
   - Applied to Collision Finding Problem
   - Applied to the Element Distinctness Problem
2. Quantum Walk Search : design Quantum algorithm based classical random walk
   - Applied to Element Distinctness
   - Generalizing Element Distinctness

Search Problem :

- Input : a marked set $M \sube \Omega$
- Output : a state u s.t $u \in M$
  Collsion Finding : $\Omega := [N]^{2}, \; [N] = \{1, ..., N\}$

  - Input : a 2to1 function$H:[N] \to [R]$ s.t $M := \{(i, j) \in [N]^{2}: i \ne j, h(i) = h(j)\}$
  - Valid Output : (2, 6) because h(2) = h(6) and (5, N)

| x   | h(x) |
| --- | ---- |
| 1   | 63   |
| 2   | 21   |
| 3   | 34   |
| 4   | 53   |
| 5   | 13   |
| 6   | 21   |
| 7   | 45   |
| ... | ...  |
| ... | ...  |
| ... | ...  |
| N   | 13   |

Any Search Problem can be solve using generalize algorithms, we sample the object u according to some probability distribution and then check is that object is marked or not

Sample $u \in \Omega$ according to $\pi$
Check if $u \in M$ and if so, output u.

Random Search for a Collision

Collision Finding problem we just sample the uniform random integers and then compute h(.) on both and check if there is a collision or not.

Repeat N times :

- Sample $i \in [N] \; and \; j \in [N]$ uniformly at random.
- If $i \ne j \; and \; h(i) = h(j)$, output $(i, j)$

Randomized Search framework

Step-1 : Choose Parameters lik $\Omega, \{M_x \}_x$ a search problem where $\pi$ is a distribution on $\Omega$

Step-2 : Compute Properties like $\epsilon \le \sum_{u \in M} \pi(u)$

Step-3 : Implement Subroutines that samples the objects according to distribution $\pi$ and analyze it complexity etc.

- Sampling Subroutine
