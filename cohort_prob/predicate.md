# Predicate Logic Exercises

These exercises use the syntax, quantifier rules, Peano axioms, and induction
principles described in `notes/predicate.md`. Show the intermediate formulas
and label each inference step.

## Exercise 1: Universal Elimination

Given the premises:

$$
\forall y.\,\exists z.\,follows(y,z)
$$

and

$$
\forall x.\forall y.\,(\exists z.\,follows(y,z) \implies follows(x,y)),
$$

prove:

$$
follows(ada,cara).
$$

Use Universal Elimination and Implication Elimination only.

## Exercise 2: Universal Introduction

Given:

$$
\forall x.\forall y.\,(\exists z.\,loves(y,z) \implies loves(x,y)),
$$

and the fact that every person loves someone:

$$
\forall y.\,\exists z.\,loves(y,z),
$$

use placeholders and Universal Introduction to prove:

$$
\forall x.\forall y.\,loves(x,y).
$$

Explain why the placeholders may be generalized.

## Exercise 3: Existential Introduction

Given:

$$
p(c,d),
$$

derive each of the following using Existential Introduction:

1. $\exists y.\,p(c,y)$
2. $\exists x.\,p(x,d)$
3. $\exists x.\exists y.\,p(x,y)$

The same ground term may be used as a witness in more than one application.

## Exercise 4: Existential Elimination

Given:

$$
\exists x.\,p(a,x)
$$

and

$$
\forall x.\,(p(a,x) \implies q(a)),
$$

prove:

$$
q(a).
$$

Use the sub-proof version of Existential Elimination. Make the witness fresh
and explain why it does not occur in the conclusion.

## Exercise 5: Peano Deduction

Use the following Peano axioms to prove that $3$ is odd:

$$
even(zero)
$$

$$
\forall x.\,(odd(suc(x)) \iff even(x))
$$

$$
\forall x.\,(even(suc(x)) \iff odd(x))
$$

Your target is:

$$
odd(suc(suc(suc(zero))))
$$

Use Universal Elimination, Biconditional Elimination, and Implication
Elimination.

## Exercise 6: Linear Induction

Use linear induction and the Peano parity axioms to prove:

$$
\forall x.\,\big((even(x) \implies even(suc(suc(x))))
\wedge (odd(x) \implies odd(suc(suc(x))))\big).
$$

Your proof should include the following cases:

1. The base case $x=zero$.
2. The base case $x=suc(zero)$.
3. The inductive case from $x$ to $suc(x)$.

Explain why two base cases are needed for this statement.

## Exercise 7: Structural Induction

Consider the term grammar

$$
Term \;::=\; zero \mid suc(Term) \mid add(Term,Term).
$$

Assume the equality and addition axioms from the notes:

$$
\forall x.\,eq(x,add(zero,x))
$$

and

$$
\forall x.\forall y.\,eq(add(suc(x),y),add(x,suc(y))).
$$

Prove by structural induction that every term is equal to a Peano numeral. In other words, prove:

$$
\forall t.\,\exists n.\,(num(n) \wedge eq(t,n)),
$$

where the predicate $num$ is defined recursively by

$$
num(zero)
$$

and

$$
\forall n.\,(num(n) \implies num(suc(n))).
$$

For the $add$ case, state and prove the auxiliary lemma that the sum of two numerals is equal to a numeral.

## Exercise 8: Multidimensional Induction

Prove the following statement by induction over the pair $(x,y)$:

$$
\forall x.\forall y.\,
\big(eq(x,y) \implies
((even(x) \wedge even(y)) \vee (odd(x) \wedge odd(y)))\big).
$$

Use the parity axioms and the equality axioms NEqBase and NEqRec. Your proof should include:

1. The base case $(zero,zero)$.
2. The mixed cases $(zero,suc(y'))$ and $(suc(x'),zero)$.
3. The successor case $(suc(x'),suc(y'))$.

In the successor case, explain how the parity of both components changes and how NEqRec relates equality of the successor pair to equality of the predecessor pair.
