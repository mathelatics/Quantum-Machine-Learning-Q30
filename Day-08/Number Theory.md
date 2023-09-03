# Day-08 : Quantum Cryptography - Number Theory #Quantum30 Challenge

Till now we learn Classical Cryptography's mainly symmetrical algorithms like Stream Cipher, Block Cipher, Affine Cipher, DES, AES etc. but today we are going to learn about mathematical foundation for the second kind of Classical Cryptographic Algorithms called Asymmetric(Public-Key) Algorithms and End of This week we will also learn about the Standard Protocols like Digital Signature, Certificates etc.

Thus, today's learning objectives are 

- Euclidean Algebra
- Advanced Euclidean Algebra
- Importend Theorems

## Principles of Asymmetric Cryptography

Let's take a analogy of mail box at home, any person can put it's main into the mail-box but the owner has right to open the mail box to access the every mail i.e owner has key of the mail box.

Similarly, We split up the key K into two part (1) Public Key : Encryption (2) Private Key : Decryption mean our random key generation algorithm will generate the key pairs. So, Alice uses some public key to encrypt the message and send it to Bob and Bob has it's private key along with encrypted message to decrypt it.


### Basic Protocols and Security Mechanism of Public Key Cryptography

**key Distribution Problem** : In Diffie-Hellmann key Exchange and RSA , we don't have a pre-shared secret key

**Non-Repudiation and Digital Signature** : It provides the message Integrity for the Algorithms like RSA, ECDSA etc.

**Identification**  : with digital signature we can verify the identity using the challenge response.

**Encryption** : It is computationally expensive as compared to the symmetric algorithms eg : RSA etc.

### Key Transport Protocol

In practice we don't only rely on the Aymmetric but also on the symmetric alorithms thus, to accomplish this task we use the hybrid systems

- Key Exchange  is Perform using symmetric schemes and Digital Signatures are performed with asymmetric schemes.
- Encryption of messages are done using symmetrical ciphers like block/stream ciphers.

### List of Importent Public Key Cryptographic Algorithm

Asymmetric Schemes are based on the one way function $f(.)$ means Computing $y = f(x)$ is quite easy but computing $x = f^{-1} (y)$ is quite computationally hard problem. Thus one way functions are based on the computationally hard problems.

- **Factoring Integer based algorithms** :
   - Prime Factorization Theorem
   - RSA
- **Discrete Logrithm based algorithms** :
   - Compuation of exponentiation $a^{x}$
   - Diffie-Hellmann, Elgamal,DSA etc
- **Elliptic Curves based algorithms**
   - These problems are based on the generalized discrete logrithms but are mathematically hard and they don't have any proof.
   - ECDH, ECDSA etc.

### Number Theory for Public Key Algorithms
Note : I will gave you topics not details because medium does't have features to render the latex code.

1. Compute the Greatest common divisor of any two integer using efficient algorithms like Euclid
2. Euclid Division Algorithm
3. Prime Factorisation Theorem
4. Eular's Phi Function $\phi(m) = \Pi_{i=1}^{n} (p_{i}^{e_i} - p_{i}^{e_{i-1}} \; Where \; m = p_{1}^{e_1}. p_{2}^{e_2}. p_{3}^{e_3}...p_{n}^{e_n}$
5. Fermat's Little Theorem : given some prime p and integer a s.t $$ a^p \equiv a * (mod \; p) \\ a^{p-1} \equiv 1 * (mod \; p)$$
6. Generalization of the Fermat't Little Theorem called Eular's Theorem  : $$a^{\phi (m)} \equiv 1 * (mod \; m)$$


## Conclusion 
We leaned about the Public Key Cryptographic Algorithm's capabilities that does't exits into the symmetric algorithms like digital signature and key establishment functions etc. It is also computationally expensive as compared to the symmetric algorithms. End the end we learn about some concepts and theorems from number theory

You reached here means you read the complete article, follow me for more articles on the classical and Quantum cryptography 


