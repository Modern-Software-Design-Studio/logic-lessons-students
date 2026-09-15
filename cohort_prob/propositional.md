# Propositional Logic Exercises

These exercises practise truth-table reasoning, logical entailment, and
natural-deduction proofs. Unless stated otherwise, use the inference rules
defined in `notes/propositional.md`.

## Exercise 1: Evaluation and Satisfaction

Given the truth assignment $p=1$ and $q=0$, evaluate:

$$
p \implies ((q \vee p) \wedge \neg q).
$$

Then determine whether the assignment satisfies the sentence.

## Exercise 2: Entailment by Truth Table

Verify the following entailment using a truth table:

$$
p \wedge (p \implies q) \vDash q.
$$

Explain why the rows in which the premises are satisfied are sufficient to
establish the entailment.

## Exercise 3: Logical Equivalence

Use a truth table to verify De Morgan's law:

$$
\neg(p \vee q) \iff (\neg p \wedge \neg q).
$$

State whether the biconditional is valid, satisfiable, or unsatisfiable.

## Exercise 4: Implication Chain

Using natural deduction, prove $r$ from the premises:

$$
\{p,\; p \implies q,\; q \implies r\}.
$$

Label every line with its justification.

## Exercise 5: Disjunction and Contradiction

Using natural deduction, prove $r$ from the premises:

$$
\{p \vee q,\; p \implies r,\; q \implies r\}.
$$

Then, separately, prove $\neg p$ from:

$$
\{p \implies q,\; p \implies \neg q\}.
$$

Identify the inference rule used for each conclusion.

## Exercise 6: Biconditional Transitivity

Using natural deduction, prove $p \iff r$ from the premises:

$$
p \iff q
\qquad
q \iff r.
$$

Use Biconditional Elimination to obtain the required implications and
Biconditional Introduction to construct the final conclusion. Label every
line with its justification.
