# Cryptographic Hash Functions

A cryptographic hash function (H) takes an input (M) and produces an output (H(M)). The function (H) satisfies some properties, makes it suitable for various cryptographic applications such as data integrity verification, digital signatures, and password storage.

A cryptographic hash function \(H\) in mathematical notation:

$H: \{0, 1\}^* \rightarrow \{0, 1\}^n$

Where:

- $(\{0, 1\}^*)$ represents the set of all possible binary strings of any length (input space).
- $(\{0, 1\}^n)$ represents the set of all possible hash values of length \(n\) bits (output space).

A cryptographic hash function is a mathematical algorithm that takes an input (message) and produces a fixed-size output (hash value) that appears random. Cryptographic hash functions are designed to satisfy specific mathematical properties that make them suitable for various security applications. Let's explore the mathematical aspects of hash functions:

1. *Deterministic:* For a given input, a hash function always produces the same hash value. In mathematical terms, \(H(x)\) is deterministic, where \(x\) is the input message.
2. *Fixed Output Length:* A hash function produces a hash value of fixed size, regardless of the input size. Mathematically, $(H: \{0, 1\}^* \rightarrow \{0, 1\}^n)$, where $(\{0, 1\}^*)$ is the set of all possible binary strings of any length, and $(\{0, 1\}^n)$ is the set of hash values of length \(n\) bits.
3. *Pre-image Resistance:* Given a hash value \(h\), it is computationally infeasible to find any input \(x\) such that \(H(x) = h\). In other words, finding a pre-image \(x\) for a given \(h\) is difficult. Mathematically, $(H: \{0, 1\}^* \rightarrow \{0, 1\}^n)$ is pre-image resistant.
4. *Second Pre-image Resistance:* Given an input \(x_1\), it is computationally infeasible to find another input $(x_2) ((x_2 \neq x_1))$ such that \(H(x_1) = H(x_2)\). This property is also known as weak collision resistance.
5. *Collision Resistance:* It is computationally infeasible to find two distinct inputs \(x_1\) and \(x_2\) such that \(H(x_1) = H(x_2)\). This property is also known as strong collision resistance.
6. *Avalanche Effect:* A small change in the input should result in a significantly different hash value. In mathematical terms, a slight change in the input \(x\) should lead to a drastic change in \(H(x)\).
7. *Efficiency:* Hash functions are designed to be efficiently computable for any input. This includes being able to compute the hash value in a reasonable amount of time.
8. *Pseudorandomness:* Hash functions aim to produce hash values that appear random. This property helps ensure that the hash values do not reveal any information about the original input.

Mathematically, cryptographic hash functions rely on various operations such as modular arithmetic, bitwise operations, logical functions, and complex transformations to achieve these properties. The specific algorithms used in cryptographic hash functions, such as SHA-256, are designed to provide strong security guarantees and resist various cryptographic attacks.

## Properties of MAC (Message Authentication Code) algorithm

The  basic  required  properties  of  the  MAC  algorithm  h(K,  x)  for  any  message  x  are  as follows:

1. Ease of Computation: The MAC algorithm h(K, x) given a key K and an input x is easy to compute.
2. Compression: The MAC algorithm maps an input x of arbitrary finite length to an output h(K,x) of fixed length say, n.
3. Computation   resistant:  Given  one  or  more  message-MAC  pairs,  it  is computationally infeasible to find MAC of a new message. This property also implies that the key K used for generating the MAC cannot be recovered from the given one or more message-MAC pairs.

This  property  also  implies  pre-image  resistant,  2nd  pre-image  resistant  and  strong collision resistant properties when key K is unknown. Recovery of the MAC key by adversary  is  an  attack  which  will  allow  selective  forgery  i.e.  the  adversary  can generate valid MAC for a message of his choice and hence MAC algorithm should have computation resistant property. Further, to avoid brute-force attack the key size of MAC algorithm is kept sufficiently large.
