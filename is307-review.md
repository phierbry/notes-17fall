# is307 Introduction to Cryptography and Infomation Security
## lecture 1 Introduction

**What is information security?**
<li>ISO(not proper): confidentiality, integrity, availability of information.
<li>right definition: information security is the science of information system in the presence of adversary.


**Aspects of security:** 
<li>security attack
<li>security service
<li>security mechanism

**What should be kept in mind?**
Security is a part of information system 
Do not setuo security just for security's sake.

**Is there completely secure system?**
According to the definition, there is.

**Attack**
passive: interciption
active: modification, interruption, fabrication

**Service**
authentication, access control, data confidentiality, data integrity, non-repudiation
How can we distinguish access control and other things?
	- access control is not about cryptography.

**Mechanism**
The technique.

**Different from the general system** 
different goal, general ones want efficiency
security system have to be difficult to break. Find difficult problem: cryptography.


## Lecture 2
**What is the range we talk about in this lecture?** symetric encryption. Also secret key or conventional key. Popular before public key appeared.

**Shannon's model of secret communication** secure channel and cipher channel

**From the Shannon model, we get the cipher system definiion** Five elements are Key, Encrpt func, Decript func, plaintext, cipher text: 
$M,C,K,C=E_K(M),M=D_K(C)$ note that the $D_K(C)$'s $K$ is a inver of encrpt.

**Some simple example**
Transpositoin: seems like permutation 
Substitution: 
<li>alphabet shift(also a permutation), Caeser Cipher
<li>above is also monoalphabetic cipher - language redundacy, 
frequency analysis
<li>multiple substitution: frequency analysis do not work - Hill(make the alphabet longer) Vegenere. Polyalphabetic. Periodic.
<li> rotor machine in ww2: 3 rotor($26^3<<26!$ avoid repeat in design)

**These above are all easy to break, any thing better or ultimate?** Yes, there are provable perfect secret cipher. e.g. one-time-pad. Sadly, not practical. why

**not about cryptography but about confidentiality** - steganography




## Lec3 How to prove secrety
**Range we talk about** - confidentiality - about who can read what

**To achieve security, we first find out where the attackers are and what's their capability and knowledge.**

### about attacker's knowledge
**principle for design a secret system - Kerckhoff** Assume that attackers no all the details except the key. Security should no depend on the secrecy of the algorithm. Use standard cipher.
**Why standard cipher? (obey the intuition of hiding)** advantage of standard and secret. Idea about develop and use.
**classify:** ciphertext-only, known-plaintext, chosen-text (one try), adaptive chosen-text(no limitation)



### about attacker's capability
**classify** 
<li>unconditional security(only depend on knowledge)
	<li>perfect secrecy $P(Y|X)=P(Y),P(X|Y)=P(X)$
	<li>strongly ideal cipher: $P(K|X)=P(K)$
	<li>truly unbreakable: against chosen-text attacks
	**perfect secrecy** redundacy analysis do not work. entropy, redundacy, unicity distance
	**strongly ideal cipher** against ciphertext-only, compression, not practical.
	**truly unbreakable** remaining ciphertext and plaintext are stt-ind, random cipher.

- conditional security
- difficulty, complexity. Turing machine, gate.

**Two concepts** provable security < provably security.


## Lec4 BLock Cipher DES 
One way functions: one-way fucntion, keyed function, keyed one-way function, trapdoor functions

Block Cipher: Definition, idea of design: easy to use(encrypt and decrypt), hard break(to know key or partially).
Cipher parameters: block size $m$(64DES, 128AES), key size $k$. 

Design principle 
Software: the operation is simple, conduct on block, small look-up table(S)
Hardware: similarity of encryption and decryption. 
Security: confusion(hard to determine the key from known cipher and plain) diffusion(one-bit change in plain influence cipher a lot, for virtually all k, sometimes still some weak key) resist known attack 

Iterated block ciphers
$X, Y, K, r, f, Y_i, K_i$, key schedule, f is round function 
$Y_0 = X$, $K_i = key(K, i)$, $Y_i = f(Y_{i-1}, K_{i-1})$
Why iteration? It provides diffusion and confussion. $c^r,rc(f)$

DES 
What is DES? data encryption standard
Cipher parameters: $m=64, k=56+8$ 56 is random, 8 is parity check
Iteration parameters: 16 rounds, 32-bit word, 48-bit subkey.
$L_i = R_{i-1}$, $R_i = L_{i-1} \oplus f(R_{i-1}, k_i)$
注意得到L15 R15之后不再交换
Initial permutation: just for implementation consideration
Feistel Structure: Inversible! 
- Encryption: $L_i = R_{i-1}$, $R_i = L_{i-1} \oplus f(R_{i-1}, k_i)$
- Decryption: $R_{i-1} = L_i$, $L_{i-1} = R_i \oplus f(L_i, k_i)$
$f$ function: R 按照固定的套路expansion成48位 和 subkey等长，二者异或，得到48位=8\*6位，查sbox得到8个[0..15]的数每个是4位，一共8\*4=32位。
Key schedule: PC-1 (64bit key -> 56bit, remove 8,16...56,64 then permutation), CnDn始终是各28位, PC-2(56->48), left shift amount table

Encryption Decryption Similarity
Same process, only subkeys are different.

Key length: multiple encryption.
3-DES: Ek1 Dk2 Ek3
2-key 3-DES: Ek1 Dk2 Ek1
2-DES: Meet in the middle attack, still 56bit strength.
weak keys

## Lec5 IDEA and AES 
### IDEA  international data encryption algorithm 
64-bit block size, 128-bit key size.
**round function**
 16-bit subblock $\oplus, \odot, +$








## Lec9 Hash
## Reading the book
A hash function H accepts a variable-length block of data M as input and produces a fixed-size hash value h=H(M).
A good hash function has the property that the results of applying the function to a large set of inputs will produce outputs that are evenly distributed and apparently random.

cryptographic hash function

**preimage and collision** For a hash value $h=H(x)$, $x$ is the preimage of $h$. A collision occurs if we have $x /neq y$ and $H(x)=H(y)$.

Security requirements for cryptographic hash function 
variable input size
fixed output size 
efficiency 
**preimage resistant(one-way property)**
For any given hash value $h$ it is computationally infeasible to find $y$ such that $H(y)=h$
**second preimage resistant (weak collision resistant)**
For any given block $x$, it is computationally infeasible to find $y \neq x$ that $H(x)=H(y)$
**collision resistant (strong collision resistant)**
It is computationally infeasible to find any pair $(x, y)$ such that $H(x)=H(y)$

**preimage resistant**
**preimage resistant (one-way property)** it is easy to generate the hash code from given message but virtually impossible to generate a message from the hash code.
**second preimage resistant (weakly one-way)** it is impossible the find an alternative message with the same hash value as a given message.

### Brute force attack 
**Preimage and second preimage attacks** For an m-bit hash value, the adversary would have to try on average $2^{m-1}$ values of $y$ to find one that generates a given hash value $h$.

### Collision resistant attacks 
For collision resistant attack, and adversary wishes to find two messages or data blocks, x and y that $H(x)=H(y)$. With the result of birthday paradox, we can expect to find two data blocks with the same hash value within $\sqrt{2^m}$

### Cryptanalysis
The ideal hash algorithm will require a cryptanalytic effort greater than or equal to the bruteforce effort.

The overall structure of typical secure hash function - iterated hash function. 
The hash function takes an input message and partitions it into $L$ fixed-size blocks of $b$ bits each. If necessary, the final block is padded to $b$ bits. The final block also includes the value of the total length of the input. The inclusion of the length makes the job of opponent more difficult.
IV=$CV_0$=initial value, $CV_i$=chaining variable, $Y_i$=ith input block, f=Compression algorithm, L=Number of input blocks, b=length of block, n=length of hash code.


## slides
HASH FUNCTION
Definition of hash function: from message to hash code 
application: 
- modification detection code (MDC) require: second preimage resistant, also called one-way
- signature. To sign a message M, first h=H(M), then sign hash code h. s=S(H). motivation: can not use redundace attack. require: collision free 

RANDOM ORACLE
random oracle: random first answer, fixed later asked 
random oracle is not function 
random oracle model(ROM): a proving framework. If a system is security in ROM, we replace the RO with a fixed hash function. This is a flaw.

SECURITY OF HASH FUNCTION 
mentioned two requirement
one-way (second preimage resistance, weakly one-way) fixed target, complexity=$2^m$, 
collision free(collision resistance, strong one-way) arbitray pair, complexity=$2^{m/2}$
NOTE that as hash funciton map a large space to a smaller one, there are always collision, the keypoint is 'infeasible'
COMPLEXITY COMPUTATION: basic combinatorics and probability, birthday paradox(not intuitive) 


ITERATED HASH FUNCTION 
Components:
- compress funciton, also called round function, l-bit to m-bit
- initial value: initial hash $H_0$ m-bit 
- message: L blocks of l-bit $m$
- hash code: the final result, m-bit 
- chaining value: intermediate result m-bit

ATTACK (for iterated hash)
- Target attack (2nd preimage attack): given M, $H_0$ find M'
free-start target attack: find H', M' that $Hash(H_0', M)=Hash(H_0, M)$
message chosen attack: find a set $C$(in fact a set that can be partition because of equivalent class theorem) $\forall M \in C, \exists M' \ s.t. Hash(H_0, M)=Hash(H_0, M')$
- Collisoin attack: given $H_0$, find M, M'
semi free-start collision attack: find $H_0$ M, M', $Hash(H_0,M)=Hash(H_0, M')$
free-start collision attack: find $H_0', M, M'$, $Hash(H_0,M)=Hash(H_0', M')$
Complexity:
$C_{FS-target} \leq C_{target} \leq 2^m$, $C_{FS-collision} \leq C_{semi-FS-collision} \leq C_{collisoin} \leq 2^{m/2}$
From complexity we have these below relationships
relationship between target and collison attack: target -> collisoin 
relationship between free-start and usual: security against free-start attack -> security against usual
relationship between compress function and Hash chain: $h$ attack -> $H$ attack, ***chain may be weaker than link***

ATTACK on HASH(chian)
Trival free-start attack: find H_1, don't need to start at first block $Hash(H_0, M_1, M_2)=Hash(H_1, M_2)$
Trival semi free-start attack: find fixed point, still use the given $H_0$
Long-message target attack (n block in the given message)
n block can be used as n choice, any one is broken, we get the collision. So the complexity:
$C_{target}(Hash) \leq 2 \times 2^m/n, \ for \ n \leq 2^{m/2}$
$C_{target}(Hash) \leq 2 \times 2^{m/2}, \ for \ n > 2^{m/2}$

MD-STRENGTHENING 
Taking advantage that M' can have different length from M, one can break hash wiout break h. (add some prefix!)
Merkle-Damgaard strengthening: let the last block be the length of the original message.
Theorem: against free-start collisoin attack, Hash-MD is as secure as h. 
We can also say that free-start collision attack on HashMD <=> free-start collision on h.
Collision attack on HashMD implies free-start collision on h. inverse is unknown

Target attack when h is not one-way 
Theorem 3 $C_{target}(HashMD) \leq 2^{m/2}C_{FS-target}(h)^{1/2}$
Proof: given $HashMD(H_0, M_1, M_2, M_3,...)$ and given $H_2$. We use meet-in-the-middle-attack to show that the complexity is only $2^{(m+s)/2}$.
We try $2^{(m+s)/2}$ values of $M_1'$, and forward to compute $2^{(m+s)/2}$ values of $H_1'$. We try $2^{(m-s)/2}$ values of $M_2'$ and backward to compute $2^{(m-s)/2}$ values of $G_1$. Note that here we use $2^s$ cmplexity to compute each backward. Thus both forward and backward use $2^{(m+s)/2}$. 
With such much $H_1'$ and $G_1$, we get high probability to find collision which means that $HashMD(H_0, M_1', M_2', M_3,...)=HashMD(H_0, M_1, M_2, M_3,...)$

Meet-in-the-middle attack 
Theorem $A,B \subset S$ if $|A||B| \simeq S$, then $P(A \cap B \neq \emptyset) \simeq 1-e^{-1}=0.63$

Issue with MD construction. 
Don't understand why "one collision implies arbitrary many collision"
We can use random collision to generate useful and harmful collision. Document collision with MD. 

HashMD compress function 
free-start collision attacks on HashMD  <=> h 
collision attack on HashMD => free start collisoin of h 
free-start target attack on h => target attack on HashMD 
target attack on HashMD cannot achieve ideal security
Goal: find secure h against free-start collison attack 

Compress functions 
one-way, (m+l)-bit -> m-bit, l=m, 2m, 3m, 4m, ...
current construction - iteration + MD strengthening has some drawback. 
We have Sponge construction - absorbing and squeezing.





