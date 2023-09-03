# Diffie-Hellman key Exchange

It is a exchange of the secrets between two different entities of same massage for encryption to decryption. This method help us to achieving confidenciality and authenticity and Integrity of message.

It is completely based on the modular arithmetic and discrete logrithm over G = {Z_{p}*,×}. So, we needed to have knowledge about the following mathematical topics.

- Finite Group Theory
  - Cyclic Group : $(Z_{n}, *)$
- Modular Arithmetic
- Discrete Logrithm

Note : As we already studied the concepts of the Modular Arithmetic and we have some knowledge about the group theory then we proceed with discrete logrithm problem

## Discrete Logrithm Problem

Discrete logarithms are theanalogue of ordinary logarithms in modular arithmetic. It is defined for a multiplicative group G = {Z_n*, ×}, where Z_n* is a set of coprimes of n. If a and b are two elements of Z_n* such that b = a^ i mod n, then discrete logarithm of b to base a is defined as: i = log{a,n} b.

Relevant properties of Multiplicative group of Zn*  i.e. G =

- It satisfies the properties of a group i.e. Closure, Associativity, existence of Identity element and Inverse.
- The multiplicative identity element e of the group is 1.
- If n is prime number p, elements of Zp* are integers from 1 to p - 1.
- Order of group, |G|, is the number of elements in Zn* i.e. is the number of coprimes to n denoted by Euler's totient function φ(n). If n is prime number p, then |G| = p – 1.
- Order of an element a of the group is the smallest i such that ai = e = 1. For example, Order of elements of Z_10* = is: Order of element 1 is 1 since 11 mod 10 = 1 Order of element 3 is 4 since 34 mod 10 = 1 Order of element 7 is 4 since 74 mod 10 = 1 Order of element 9 is 2 since 92 mod 10 = 1
- The element of Z_n*, which has the order equal to φ(n) is called primitive root of the group. For example, for G =, elements 3 and 7 are primitive roots since their order is φ(10) = 4.
- A multiplicative group G = may not have any primitive root. It can be shown that multiplicative group G = has at least one primitive root if n is 2, 4, pi, 2piwhere p is prime and i is integer.
- The number of primitive roots is given by φ(φ(n)). For example, for G =, the number of primitive roots is φ(φ(10)) = φ(4) = 2.
- A cyclic group has a generator g which can generate all the elements of Z_n* using repeated application of multiplicative operator, i.e. Z_n* = {g^1, g^2, .... g^{φ(n-1)}, g^{φ(n)}}.
- Each primitive root is a generator. In fact it can be shown that gφ(n) = g0 mod n. Hence, Z_n* = {g^0,g^1, g^2, .... g^{φ(n-1)}}.From the above, it is clear that if n is a prime number p then, Zp* consists of all the integers from 1 to p-1 and there is always atleast one primitive root in Z_p*.
- Zp* is cyclic with the primitive root as the generator g. All the elements of Zp* can be expressed as exponentiation gi i.e. Z_p* = { g^0, g^1, g^2, .... g^{p-2}} where Z_p*  is the set comprising of the elements from 1 to p-1.

### Discrete logarithm over G

Discrete  logarithm  is  fundamental  to  many  cryptographic  algorithms  based  on  modular exponentiation. For example, Diffie-Hellman algorithm in cryptography uses exponentiation to hide a secret number x as number y using  y = g*x mod p      where 0 ≤ x < p-1 Discrete logarithm of y can give the secret number x. But, given y, g and p, it is very difficult to compute x = log_{g,p} y, when p is a very large prime number. Diffie Hellman key exchange algorithm’s security is primarily based on this difficulty of finding discrete logarithm for very large prime numbers.

## Diffie-Hellman Key Exchange

Diffie  Hellman  key  exchange  allows  two  entities  to  exchange  non-secret  parameters  and calculate a unique shared secret from these parameters i.e. the communicating entities are able to share a secret without even sending the secret directly to each other. The adversary cannot calculate the shared secret from these parameters. Once established, the shared secret can be used as the symmetric key for encryption or as seed for generating symmetric key. Diffie-Hellman algorithm is based on two parameters p and g where p is a large prime number of the order of 300 decimal digits and g is a generator of the multiplicative group {Z_p*,×}. p and g are not confidential and can be known publicly. The steps of Diffie-Hellman algorithm are given below:

1. Alice chooses a large secret random number a, 0 < a < p – 1.  She calculates K_A = g^a mod p and sends (p, g, K_A) to Bob. K_A is called DH half key of Alice and is not a secret.
2. Bob also chooses a large secret random number b, 0 < b < p – 1, and calculates his DH half key K_B = g^b mod p. He sends K_B to Alice.
3. Alice and Bob independently calculate the shared secret key K as given below:
   Alice calculates K = (K_B)^a mod p = (g_b)^a mod p = (g_a)^b mod p.
   Bob calculates K = (K_A)^b mod p = (g_a)b mod p = (g_a)^b mod p.
   Thus, both Alice and Bob are able to exchange the secret among themselves secretly without ever requiring to reveal the secret directly.

### A simple implementation of these mathematical diffie-hellman key exchange algorithm from scratch in python

*1. Calculate the discrete Log*
def mod_exp(base, exponent, modulus):
    result = 1 
    while exponent > 0:
        if exponent % 2 == 1:
            result = (result * base) % modulus
        exponent = exponent // 2
        base = (base * base) % modulus
    return result

*2. Calcuate the public key for diffie-hellman key exchange*
def diffie_hellman(p, g, private_key):
    public_key = mod_exp(g, private_key, p)
    return public_key

*3. Calculate the shared secred using public and private key between alice and bob*
def shared_secret(p, public_key, private_key):
    secret = mod_exp(public_key, private_key, p)
    return secret

*4. Till Now we defined all functions that we use for our diffie hellman key exchange calculations : let's apply them*

#shared prime number and primitives root modulo
p = 23 
g = 5

#Private Keys for the Alice and Bob
private_key_alice = 6
private_key_bob = 15

#Alice's and Bob's Public Key
public_key_alice = diffie_hellman(p, g, private_key_alice)
public_key_bob = diffie_hellman(p, g, private_key_bob)

#calculate the shared secret of both alice and bob
shared_secret_alice = shared_secret(p, public_key_alice, private_key_alice)
shared_secret_bob = shared_secret(p, public_key_bob, private_key_bob)

print("Shared Secret of Alice : ", shared_secret_alice)
print("Shared secret of Bob : ", shared_secret_bob)
        
