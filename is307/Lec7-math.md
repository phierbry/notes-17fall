# is307 Introduction to Cryptography and Information Security

## acknowledgments
Reference book: *William Stallings - Cryptography and Network Security: Principles and Practice (5th Edition)*


## Number Theory basic 
*This part comes from book chapter 4 and chapter 8*
### Divisibility and the Division Algorithm 
**Term** 
- divide, divisor, factor 
- division algorithm, remainder, residue

### Euclidean algorithm 
**Term**
- relatively prime, gcd(greatest common divisor), 
gcd(a, 0)=a 

### Modular Arithmetic
**Term**
- modulus, congruent modulo n, modular arithmetic(add, sub, mul)
- $Z_n=\\{0, 1, ..., (n-1)\\}$, set of residue, residue classes (mod n).

If $ab \equiv ac \pmod n $ and $gcd(a, n)=1$, then $b \equiv c \pmod n$. 
- gcd(a,n)=1 implies the existence of the multiplicative inverse of $a$. Thus $(a^{-1}ab) \equiv (a^{-1}ac) \pmod n$

#### Extended Euclidean Algorithm 

### Groups, Rings, and Fields 
These are fundamental elements of a branch of mathematics known as abstract algebra or modern algebra. In abstract algebra, we are concerned with sets on whose elements we can operate algebraically; that is we combine two elements with an operation defined on this set to obtain a third elements of the set. 

#### Definition of Groups, Rings and Fields
![definition of groups, ring and field](./images/DefinitionOfGroupsRingField.JPG)

**Example of group**: $S_n$ to be the set of all permutations of $n$ distinct symbols.
**Additional Concepts** 
- finite group, order, infinite group 
- Cyclic group: exponentiation within a group, generate, generator of $G$

#### Finite Fields of the form $GF(p)$
The order of a finite field must be a power of a prime $p$
**Definition of GF(p)** $Z_p$ and modulo $p$. $p$ is a prime number.
Each elements of the set other than 0 has a multiplicative inverse.

### Prime Number 
Unique integer prime number factorization

### Fermat's Theorem and Euler's Theorem 
The two play important role in RSA public-key system.
**Fermat's Theorem**
If $p$ is prime and $a$ is a positive integer not divisible by $p$, then $a^{p-1} \equiv 1 \pmod p$.
Another relaxing form: $a^p \equiv a \pmod p$. This form does not require that gcd(a,n)=1.
**Euler's Totient Function**
$\Phi(n)$ is defined as the number of positive integers less than $n$ and relatively prime to $n$. 

### Testing for Primality
#### Miller-Rabin Algorithm 
Any prime number $a>2$ can be written as $a =1+2^kq $. $q$ is an odd number. Use two properties of a prime number:
1. Prime number $p$ and positive integer $a$ that $a < p$, then $a^2 \equiv 1 \pmod p$ if and only if $a \pmod p = 1$ or $a \pmod p = -1$.
2. $a^q \equiv 1 \pmod p$ . **Or** $\exists j, 1 \leq j \leq k$ such that $a^{2^{j-1}} \equiv -1 \pmod p$.

Each time running the algorithm, it will return a result either *composite* or *inconclusive*. P(p is not a prime but return is 'inconclusive') < 1/4. We can repeat the algorithm when it return *inconclusive*.

### Chinese Remainder Theory
Also called CRT. 
Let $M= \prod_{i=1}^k m_i$ where the $m_i$ are pairwise relatively prime. We can represent any integer $A$ in $Z_M$ by a k-tuple whose elements are in $Z_{m_i}$ using the following correspondence: $A \leftrightarrow (a_1, a_2, ...,a_k)$ where $A \in Z_M, a_i \in Z_{m_i}$, and $a_i=A \pmod m_i$ for $1 \leq i \leq k$. The CRT makes two assertions.
1. The mapping of $A \leftrightarrow (a_1, a_2, ...,a_k)$ is a one-to-one correspondence (bijection) between $Z_M$ and the Cartesian product $Z_{m_1} \times Z_{m_2} \times ... \times Z_{m_k}$. 
2. Operations performed on the elements of $Z_M$ can be equivalently performed on the corresponding k-tuples by performing the operation independently in each coordinate position in the appropriate system.

### Discret Logrithm
For $a, n$ gcd(a,n)=1, there is some number $m$, that $a^m \pmod p=1$. With Euler's Theorem, we know that $m$ can be $\Phi(p)$. 
However, $\Phi(p)$ is not always the least positive choice of $m$.
This least positive choice is called: the order of $a \ (\pmod p)$, the length of period(周期) generated by $a$.
**Primitive root**: If the least positive choice is exactly $\Phi(p)$, then $a$ is primitive root of $n$.
Not all integers have primitive roots. In fact, the only integers with primitive roots are those of the form $2, 4, p^\alpha, \ and \ 2p^\alpha$, where $p$ is any odd prime number.
**Discrete Logarithm**: For any integer $b$ and a primitive root $a$ of prime number $p$, we can find a unique exponent $i$ such that $b \equiv a^i (\pmod p)$ where $0 \leq i \leq (p-1)$. We denote this as $i = \mathrm{dlog_\mathcal{a,p}}(b)$
$\mathrm{dlog_\mathcal{a,p}}(xy) \equiv [\mathrm{dlog_\mathcal{a,p}}(x)+\mathrm{dlog_\mathcal{a,p}}(y)] \pmod {\Phi(p)}$

