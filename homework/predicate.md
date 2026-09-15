# Predicate Logic Homework

These exercises use the Peano terms, equality predicate, quantifiers, and
induction principles from `notes/predicate.md`.

## Truncated Subtraction

Introduce a binary function $monus(\_,\_)$, called **monus** or truncated
subtraction. It behaves like subtraction on natural numbers, except that the
result is never negative.

Use the following axioms:

$$
\forall y.\,eq(monus(zero,y),zero)
$$

$$
\forall x.\,eq(monus(suc(x),zero),suc(x))
$$

$$
\forall x.\forall y.\,
eq(monus(suc(x),suc(y)),monus(x,y)).
$$

You may use symmetry and transitivity of equality, as well as equality
replacement inside a larger term.

## Exercise 1: Monus by Deduction

Use Universal Elimination and equality reasoning to prove:

$$
eq(monus(suc(suc(suc(zero))),suc(zero)),suc(suc(zero))).
$$

Show every intermediate equality and identify the axiom used at each step.

## Exercise 2: Monus with Zero

Prove by linear induction that

$$
\forall x.\,eq(monus(x,zero),x).
$$

Your proof should include:

1. The base case $x=zero$.
2. The inductive case from $x$ to $suc(x)$.

## Exercise 3: Monus Cancels Equal Successors

Prove by linear induction on $y$ that

$$
\forall x.\forall y.\,eq(monus(suc(x),suc(y)),monus(x,y)).
$$

Explain why the displayed statement is already an axiom, and instead prove the
following non-trivial consequence:

$$
\forall x.\,eq(monus(x,suc(x)),zero).
$$

You may use Exercise 2 and the Monus axioms.

## Exercise 4: Zero Result and Ordering

Define a relation $leq(x,y)$ by

$$
leq(x,y) \quad\equiv\quad eq(monus(x,y),zero).
$$

Prove by multidimensional induction that

$$
\forall x.\,leq(x,x).
$$

Then prove the stronger statement

$$
\forall x.\forall y.\,
\big(eq(monus(x,y),zero) \vee eq(monus(y,x),zero)\big)
$$

for all pairs of natural numbers. Explain the base, mixed, and successor pair
cases.

## Exercise 5: Monus and Addition

Assume the addition axioms from the notes:

$$
\forall x.\,eq(x,add(zero,x))
$$

$$
\forall x.\forall y.\,eq(add(suc(x),y),add(x,suc(y))).
$$

Prove by induction on $y$ that

$$
\forall x.\,eq(monus(add(x,y),y),x).
$$

In the inductive case, use the AddSuc and Monus successor axioms to expose the
induction hypothesis.

## Exercise 6: Structural Induction with Monus

Consider the extended term grammar

$$
Term \;::=\; zero \mid suc(Term) \mid add(Term,Term)
\mid monus(Term,Term).
$$

Define $num(t)$ to mean that $t$ is a Peano numeral. Prove by structural
induction that every closed term can be reduced to a numeral:

$$
\forall t.\,\exists n.\,(num(n) \wedge eq(t,n)).
$$

Your proof must include a separate $monus$ case. State and prove the auxiliary
lemma that the monus of two numerals is a numeral.

## Exercise 7: A Monus Identity

Prove the identity

$$
\forall x.\forall y.\,
eq(monus(add(x,y),x),y).
$$

You may use multidimensional induction or a suitable combination of structural
and linear induction. Clearly state any auxiliary lemmas about $add$ and
$monus$ that your proof requires.
