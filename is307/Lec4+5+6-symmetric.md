# is307 Introduction to Cryptography and Information Security

## acknowledgments
Reference book: *William Stallings - Cryptography and Network Security: Principles and Practice (5th Edition)*


## Lec4 BLock Cipher DES 
One way functions: one-way function, keyed function, keyed one-way function, trapdoor functions

Block Cipher: Definition, idea of design: easy to use(encrypt and decrypt), hard break(to know key or partially).
Cipher parameters: block size $m$(64DES, 128AES), key size $k$. 

Design principle 
Software: the operation is simple, conduct on block, small look-up table(S)
Hardware: similarity of encryption and decryption. 
Security: confusion(hard to determine the key from known cipher and plain) diffusion(one-bit change in plain influence cipher a lot, for virtually all k, sometimes still some weak key) resist known attack 

Iterated block ciphers
$X, Y, K, r, f, Y_i, K_i$, key schedule, f is round function 
$Y_0 = X$, $K_i = key(K, i)$, $Y_i = f(Y_{i-1}, K_{i-1})$
Why iteration? It provides diffusion and confusion. $c^r,rc(f)$

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

**TODO TODO**