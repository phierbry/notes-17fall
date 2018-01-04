# Lec4 Church-Turing Thesis 

2017-10-30
## Turing machine
#### Schematic of a Turing Machine
- A infinite tape, input initialization, other blank
- A tape head(read, write, move left or right, not go left at the very left)
- output means halt(accept or reject), no output forever(loop)

#### The difference between finite automata and Turing machine 
write and read, left and right, infinite tape(if not, down to FA), halt take effect immediately(no following stack operation)

#### Formal definition of a Turing machine 
*Why do we need formal and strict things? To disprove!*
7-tuple $M=(Q, \Sigma, \Gamma, \delta, q_0, q_{accept}, q_{reject})$
$\Sigma$ input alphabet, not containing $\sqcup$
$\delta:Q \times \Gamma \rightarrow Q \times \Gamma \times \\{R, L\\}$

#### Configuration
$uqv$: $q$ current state, $v$ whose first symbol is the current head
**E.g.** $\delta(q_i, b)=(q_j, c, L)$: $uaq_ibv \rightarrow uq_jacv$  
$\delta(q_i, b)=(q_j, c, R)$: $uaq_ibv \rightarrow uacq_jv$
left hand end but move left $q_ibv \rightarrow q_jcv$
right hand end but move right $uaq_i \rightarrow ua \sqcup q_j$

#### Formal definition of computation
......
The collection of strings that $M$ accepts is the language of $M$, or the language recognized by $M$ denoted $L(M)$.

**Decide** If $M$ always accepts or rejects.
**Turing-recognizable** A language is turing recognizable if a Turing machine recognize it.
Also called **semi-decidable** and **enumerate**.
**Turing-decidable** A language is Turing-decidable or decidable if some Turing machine decides it.

Decidable can be represented by this function: f(x)=accepts if x in L, f(x)=reject otherwise
Semidecidable can be represented as: f(x)=accepts if x in L, f(x)=? otherwise reject or loop.

### Example
*The best way to see the differences and the ability: look at examples.*
$A= \\{ 0^{2^n} | n \geq 0 \\}$  
$B= \\{ w \\# w | w \in \\{ 0,1\\}^{\star} \\}$   
$C= \\{ a^ib^jc^k | i,j,k \geq 1 and k=ij \\}$    
$E= \\{ \\# x_1 \\# ... \\# x_l | each\ \ x_i \in \\{ 0,1 \\}^{\star} \ \ and \ \ \forall i \neq j \ \ x_i \neq x_j  \\}$   

## Variants of Turing Machines
- Multitape Turing Machines 
- Nondeterministic Turing Machines 
- Enumerators: a Turing machine with an attached printer

	

