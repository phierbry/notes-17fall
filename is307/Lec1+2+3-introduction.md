# is307 Introduction to Cryptography and Information Security

## acknowledgments
Reference book: *William Stallings - Cryptography and Network Security: Principles and Practice (5th Edition)*

## lecture 1 Introduction

**What is information security?**
- ISO(not proper): confidentiality, integrity, availability of information.
- right definition: information security is the science of information system in the presence of adversary.


**Aspects of security:** 
- security attack
- security service
- security mechanism

**What should be kept in mind?**
Security is a part of information system 
Do not setup security just for security's sake.

**Is there completely secure system?**
According to the definition, there is.

**Attack**
passive: interception
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
**What is the range we talk about in this lecture?** symmetric encryption. Also secret key or conventional key. Popular before public key appeared.

**Shannon's model of secret communication** secure channel and cipher channel

**From the Shannon model, we get the cipher system definition** Five elements are Key, Encrypt func, Decrypt func, plaintext, cipher text: 
$M,C,K,C=E_K(M),M=D_K(C)$ note that the $D_K(C)$'s $K$ is a inverse of encrypt.

**Some simple example**
Transposition: seems like permutation 
Substitution: 
- alphabet shift(also a permutation), Caesar Cipher
- above is also monoalphabetic cipher - language redundancy, 
frequency analysis
- multiple substitution: frequency analysis do not work - Hill(make the alphabet longer) Vegenere. Polyalphabetic. Periodic.
- rotor machine in WW-II: 3 rotor($26^3<<26!$ avoid repeat in design)

**These above are all easy to break, any thing better or ultimate?** Yes, there are provable perfect secret cipher. e.g. one-time-pad. Sadly, not practical. why

**not about cryptography but about confidentiality** - steganography



## Lec3 How to prove security
**Range we talk about** - confidentiality - about who can read what

**To achieve security, we first find out where the attackers are and what's their capability and knowledge.**

### about attacker's knowledge
**principle for design a secret system - Kerckhoff** Assume that attackers no all the details except the key. Security should no depend on the secrecy of the algorithm. Use standard cipher.
**Why standard cipher? (obey the intuition of hiding)** advantage of standard and secret. Idea about develop and use.
**classify:** ciphertext-only, known-plaintext, chosen-text (one try), adaptive chosen-text(no limitation)



### about attacker's capability
**classify** 
- unconditional security(only depend on knowledge)
	- perfect secrecy $P(Y|X)=P(Y),P(X|Y)=P(X)$
	- strongly ideal cipher: $P(K|X)=P(K)$
	- truly unbreakable: against chosen-text attacks
	**perfect secrecy** redundancy analysis do not work. entropy, redundancy, unicity distance
	**strongly ideal cipher** against ciphertext-only, compression, not practical.
	**truly unbreakable** remaining ciphertext and plaintext are stt-ind, random cipher.

- conditional security
- difficulty, complexity. Turing machine, gate.

**Two concepts** provable security < provably security.