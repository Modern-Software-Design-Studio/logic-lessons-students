# 50.057 Propositional Logic

## Learning Outcomes 

* Analyse the syntax of propositional statements
* Apply truth-table to analyse the semantics of the propositional statements
* Evaluate propostional statements
* Perform satisfaction check given propostional statements
* Explain logical equivalence
* Explain logical consistency
* Explain logical entailment
* Apply inference rules to devise propositional proofs


## Propositional Logic

Propositional Logic is to reason about connection between propositions. Each proposition is a statement denoting something is true or false. From this point onwards, we use the terms "proposition", "statement" and "sentence" interchangeably.

In propositional logic, there are two kinds of sentences. 

* A simple sentence or a simple statement form by an atomic symbols, such as $p$, $q$, $it\_is\_raining$. As a convention of this class, we use a sequence lowercase alphabets to denote an atmoic symbol.
* A complex sentence (statement) can be constructed from a set of simple sentences connected by logical connectives (AKA logical operators), e.g. 
    * $rain \wedge thunder$, 
    * $bitter \vee sweet$, 
    * $boy\_older\_than\_18 \implies boy\_goes\_to\_NS$,
    * $\neg floor\_is\_wet \implies \neg it\_has\_rained$.

### Syntax of Propositional Logic


1. Conjunction $p \wedge q$
1. Disinjection $p \vee q$ 
1. Negation $\neg p$ 
1. Implication $p \implies q$
1. Biconditional $p \iff q$, it's a short hand for $(p \implies q) \wedge (q \implies p)$.

The order of predence among the operators are arranged from strongest to weakest.


1. $\neg$
1. $\wedge$
1. $\vee$
1. $\implies$  
1. $\iff$

$\wedge$ and $\vee$ are left associative and $\implies$ and $\iff$ are right associative.

For example, 

1. $\neg p \vee q$ is parsed as $(\neg p) \vee q$.
1. $p \wedge q \wedge r$ is parsed as $(p \wedge q) \wedge r$.
1. $p \implies q \implies r$ is parsed as $p \implies (q \implies r)$.
1. $p \implies q \wedge q \implies p$ would be parsed as $p \implies ((q \wedge q) \implies p)$, which is quite different from $(p \implies q) \wedge (q \implies p)$.


### Semantics of Propositional Logic

The meaning of propositional logic statements are representated as the relation between the truth assignment of the atomic proposition and the truth values of complext statements.

We have studied them in our earlier school years, under the name "truth table".

| $p$ | $q$ | $\neg p$ | $p \wedge q$ | $p \vee q$ | $p \implies q$ | 
|-----|-----|----------|--------------|------------|----------------|
| 1   | 1   | 0        | 1            | 1          | 1              | 
| 1   | 0   | 0        | 0            | 1          | 0              | 
| 0   | 1   | 1        | 0            | 1          | 1              | 
| 0   | 0   | 1        | 0            | 0          | 1              | 
  

Without confusing ourselves with the propositions, we use 1 to denote true and 0 to denote false. 

We leave the semantics of biconditional statement as an exercise. 


### Evaluation
With the semantics of the logical connectives defined, we can evaluate the truth value of any compound statements given a truth-value assignment of all the atomic propositions. 

For example, given $p$ is 1 and $q$ is 0, we find 

$$
\begin{array}{c}
p \implies ((q \wedge q) \implies p) \\
p \implies ((0 \wedge 0) \implies p) \\ 
p \implies (0 \implies p) \\ 
1 \implies 1 \\
1
\end{array}
$$

### Satisfaction

Satisfaction is the opposite of evaluation. Given a complex statement $\psi$, we find the set (or subset) of the truth-assignments to the atomic propositions such that the $\psi$ is evaluated to 1.

One working but not scaling well approach is to construct the truth table over all the atomic propositions in $\psi$ and filter out those rows that makes $\psi$ evaluate to 0.

For example given statement $(p \implies q) \wedge (q \implies p)$,

| $p$ | $q$ |  satisfying $(p \implies q) \wedge (q \implies p)$ | 
|-----|-----|:-----------:|
|  1  | 1   | yes         |
|  1  | 0   | no          | 
|  0  | 1   | no          |
|  0  | 0   | yes         |

It shows that the 1st and the 4th rows of truth-assignments satisfy $(p \implies q) \wedge (q \implies p)$.

Clearly there exists proposition which is *unsatisfiable* i.e. there exists no  the truth-assignment to make it evaluate to 1. And there exists propsition that is *valid* i.e. there exists no truth-assignment make it evaluate to 0. Those propositions that are "in-between" (just like the above) are considered *contingent*.

A proposition is *satisfiable* if it is valid or contingent. A proposition is *falsifiable* if it is unsatisfiable or contingent.

### Logical Equivalence and Logical Consistency

We say two propositions, $\psi$ and $\phi$, are logically *equivalent* if for all truth-assignments, they yield the same evaluation results. For example $\neg (p \vee q)$ and $\neg p \wedge \neg q$ are logically equivalent.

If $\psi$ and $\phi$ are logically equivalent, we can use $\psi$ in the context where $\phi$ is expected, which is called *substitution*.

We say two propositions, $\psi$ and $\phi$, are logically *consistent*, if there exists some truth-assignment, under which  $\psi$ and $\phi$ are evaluated to 1.

##### Logical Schema : Sentences with greek letters
In the above we use $\psi$ and $\phi$ instead of $p$ and $q$ to highlight that we are refering to any general proposition, not by choice nor cherry-picking. This is useful for arguing something that valid in general, not for a specific instance. We often use the term "schema", instead of sentence, to refer to a (compound) proposition that contains greek symbols, because they are not referring to a specific sentence.

### Logical Entailment Formally

Given two propositions, $\psi$ and $\phi$, if all the truth-assignments satisfying $\psi$ also satisfy $\phi$, we say $\psi$ logically entails $\phi$, written as $\psi \vDash \phi$.

For example, we find $p \vDash (p \vee q)$, but $p \not\vDash (p \wedge q)$.

#### Exercise
Verify $p \vDash (p \vee q)$ using truth-table.

### Logical Equivalence vs biconditional, Entailment vs implication

#### Equivalence Theorem: $\psi$ and $\phi$ are logically equivalent if and only if $\psi \iff \phi$ is valid.

This theorem enables us to rewrite larger (complex) sentences into alternative forms via subsituttion so that we could apply some other result to prove it.

#### Deduction Theorem: $\psi$ logically entails $\phi$ if and only if $(\psi \implies \phi)$ is valid. 

More generally, a finite set of sentences $\{ \psi_1, ... , \psi_n\}$ logically entails $\phi$ if and only if the compound sentence $(\psi_1 \wedge ... \wedge \psi_n \implies \phi)$ is valid.

This theorem enables us to use logical implication to make "progress" towards the goal of the proof.

#### Unsatisfiability Theorem: A set of sentences, $\{  \psi_1, ... , \psi_n \}$ logically entails a sentence $\phi$ if and only if $\psi_1 \wedge ... \wedge \psi_n \wedge (\neg \phi)$  is unsatisfiable.


This theorem unlocks one possible proof strategy for proving entailment, i.e. proof by contradiction.

#### Consistency Theorem: $\phi$ is logically consistent with $\psi$ if and only if the sentence $(\psi \wedge \phi)$ is satisfiable. 

More generally, a sentence $\psi$ is logically consistent with a finite set of sentences $\{\psi_1, ... , \psi_n \}$ if and only if the compound sentence $(\psi_1 \wedge ... \wedge \psi_n \wedge \phi)$ is satisfiable.


### Proof System - Natural Deduction

The process of proving something in propositional logic is to start from a set of premises, (each premise is a proposition which is assumed to be true), and check that the given conclusion (which is our goal proposition) is entailed.

As highlighted earlier one could construct the truth-table, which won't scale when the set of premises and the conlusion is complicated.

Alternatively, we can make use of some rewriting rules. We call them *inference rules*. These rules are not part of the propositional syntax. Although we could also prove their validity by constructing the truth-tables. having them stated as inference rules speed up our proof process (by shortenning the proof). 

> One way to understand the inference rules is to think of them as the "builtin" library for our proof system.

Let's consider the list of inference rules as follows



#### Implication Elimination ($\implies$Elim)

$$
\begin{array}{c} 
\phi \implies \psi \\ 
\phi \\ 
\hline
\psi
\end{array}
$$

In this rule, the two sentences above the horizontal line are the premises. The one below is called the conclusion. 

> Since the rule itself can also be proven valid, we could restore the rule back into an implication statement $(\phi \implies \psi) \wedge \phi \implies \psi$ and use truth-table to prove its validity. This is just for understanding, we will apply this rule directly without going through its validity proof. 

When given a context containing $it\_rain \implies the\_floor\_is\_wet$ and $it\_rain$, we could apply the implication elimination rule to show that $the\_floor\_is\_wet$.


#### Implication Introduction ($\implies$Intro)

$$
\begin{array}{c} 
\phi \vdash \psi \\ 
\hline
\phi \implies \psi
\end{array}
$$

This rule is to support "sub-proof". 

The notation $\phi \vdash \psi$ means that there is a way to we can verfiy $\psi$ given $\phi$ .  The implication introduction rule discharges
that temporary assumption and concludes that $\phi \implies \psi$ given a sub proof from $\phi$ to show $\psi$..

A more detailed example will be given later.




#### And Elimination ($\wedge$Elim) 

$$
\begin{array}{c} 
\phi_1 \wedge \phi_2 \wedge ... \wedge \phi_n \\ 
\hline 
\phi_i
\end{array}
$$

This rule says that given a conjuction of predicates is true, then the individual predicate must be true.

For example, from

$$
rain \wedge cold
$$

we may derive 

$$
rain 
$$

we may also derive

$$
cold
$$

The rule can select any one of the conjuncts in the larger conjunction.

#### And Introduction ($\wedge$Intro)

$$
\begin{array}{c} 
\phi_1 \\ 
\phi_2 \\ 
... \\
\phi_n \\ 
\hline
\phi_1 \wedge \phi_2 \wedge ... \wedge \phi_n
\end{array}
$$

This rules says that if a set of predicates is true, then the conjunction of them must be true.

For example, if we have separately established that it is raining and that the
floor is wet, we may combine them to derive 

$$
rain \wedge floor\_is\_wet
$$

Both premises are required. Having only $rain$ would not be enough to apply
this rule and conclude $rain \wedge floor\_is\_wet$.

#### Or Elimination ($\vee$Elim) 

$$
\begin{array}{c} 
\phi_1 \vee \phi_2 \vee ... \vee \phi_n \\ 
\phi_1 \implies \psi \\ 
\phi_2 \implies \psi \\ 
... \\ 
\phi_n \implies \psi \\ 
\hline
\psi  
\end{array}
$$

This rule says that if a disjunction of predicates is true, and all the predicates in the disjunction leads to the same consequence, then the consequence must be true. 

For example, if we know that either $tom\_eats\_all\_the\_candies$ or $jane\_eats\_all\_the\_candies$ is true,
and $tom\_eats\_all\_the\_candies \implies no\_candies\_left$ and $jane\_eats\_all\_the\_candies \implies no\_candies\_left$. We can conclude that $no\_candies\_left$.


#### Or Introduction ($\vee$Intro) 

$$
\begin{array}{c} 
\phi_i \\ 
\hline
\phi_1 \vee \phi_2 \vee ... \vee \phi_n
\end{array}
$$

This rule says that once one alternative has been established, it is valid to
state that at least one of several alternatives holds. The chosen conclusion
may contain the known proposition in any position.

For example, from $rain$ we may derive:

$$
rain \vee snow
$$

Similarly, from $snow$ we may derive $rain \vee snow$. We do not need to prove
that both alternatives are true; proving one of them is sufficient.



#### Negation Elimination ($\neg$Elim)

$$
\begin{array}{c} 
\neg\neg\phi \\ 
\hline
\phi
\end{array}
$$

This rule removes two consecutive negations. For example given 
$$
\neg\neg rain
$$

we can verify 

$$
rain
$$

The rule does not allow us to infer $rain$ from $\neg rain$; the premise must
contain the double negation $\neg\neg rain$.


#### Negation Introduction ($\neg$Intro)

$$
\begin{array}{c} 
\phi \implies \psi \\ 
\phi \implies \neg \psi \\ 
\hline
\neg \phi
\end{array}
$$

This rule is a proof by contradiction. If assuming $\phi$ leads both to
$\psi$ and to $\neg\psi$, then the assumption $\phi$ cannot be true.

For example, if

$$
p \implies q
\qquad\text{and}\qquad
p \implies \neg q,
$$

then we may conclude:

$$
\neg p.
$$


#### Biconditional Elimination ($\iff$Elim)


$$
\begin{array}{c} 
\phi \iff \psi \\ 
\hline
\phi \implies \psi \\ 
\psi \implies \phi
\end{array}
$$

This rule extracts the two directional implications contained in a
biconditional. For example, from

$$
student\_passes \iff credits\_sufficient
$$

we may derive both

$$
student\_passes \implies credits\_sufficient
$$

and

$$
credits\_sufficient \implies student\_passes.
$$



#### Biconditional Introduction ($\iff$Intro)


$$
\begin{array}{c} 
\phi \implies \psi \\ 
\psi \implies \phi \\ 
\hline
\phi \iff \psi 
\end{array}
$$

This rule combines two implications into a biconditional. For example, if we
have proved both

$$
even \implies divisible\_by\_two
\qquad\text{and}\qquad
divisible\_by\_two \implies even,
$$

then we may conclude:

$$
even \iff divisible\_by\_two.
$$




### An example
Suppose given 
$$\{ p, (p \implies q) , ((p \implies q) \implies (q \implies r))\}$$ 

as the set of premises, we want to show that $r$ is the conclusion.


$$
\begin{array}{|r|c|l|}
\hline
1. & p & {\tt Premise} \\ \hline
2. & p \implies q  & {\tt Premise} \\ \hline
3. & ((p \implies q) \implies (q \implies r)) & {\tt Premise} \\ \hline
4. & q & \implies{\tt Elim}: 2, 1 \\ \hline
5. & q \implies r & \implies{\tt Elim}: 3, 2 \\ \hline
6. & r & \implies{\tt Elim}: 5, 4 \\ \hline
\end{array}
$$


### Provability

Let $R$ be a set of inference rules, $\Delta$ be a set of propositional premises, and $\phi$ denotes a conclusion. We write $\Delta \vdash_{R} \phi$ iff there exists a sequence of rewriting steps that leads us to $\phi$ starting from $\Delta$. Sometimes we omit the subscript $R$ to just write $\Delta \vdash \phi$. 



### Sub-proof (Conditional Proof)

As we mentioned earlier, we want sub-proof to be supported in our system so that we can prove something like the following


Given 

$$
\{ p , p \implies q , q \implies r \}
$$

We want to show $r$. 

In the absence of the implication transitivity rule, we can develop the proof as follows,

$$
\begin{array}{|l|c|l|}
\hline
1. & p & {\tt Premise} \\ \hline
2. & p \implies q  & {\tt Premise} \\ \hline
3. & q \implies r & {\tt Premise} \\ \hline
4.1. & p & {\tt Reiterate}: 1 \\ \hline
4.2. & q & \implies{\tt Elim}: 2, 4.1 \\ \hline
4.3. & r & \implies{\tt Elim}: 3, 4.2 \\ \hline
4. & p \implies r & \implies{\tt Intro}: 4.1 - 4.3 \\ \hline
5. & r & \implies{\tt Elim}: 1, 4 \\ \hline
\end{array}
$$

In the above proof, steps 4.1 - 4.3  is a sub proof $p \vdash r$ (i.e. $p$ entails $r$). We can use the rule $(\implies{\tt Intro})$ to create an implication predicate $p \implies r$ into our proof context.

One may argue that the above proof can be established without  sub-proof as we already have $r$ in 4.3. The above example is to show that the possibility of using the $(\implies{\tt Intro})$, not the necessity. In many situations sub-proof is useful, i.e., we might need to reuse the fact that $p \implies r$ multiple times to prove something else.


### Soundness 

Our proof system stated above is sound.

Let $\Delta$ be a set of propositional premises, and $\phi$ denotes a conclusion, we have $\Delta \vdash \phi$ implies $\Delta \vDash \phi$.

The meaning of the above statement is that if there exists a proof that brings us from $\Delta$ to $\phi$, then $\Delta$ entails $\phi$ (can be verified using truth-table).

### Completeness 
Our proof system stated above is complete.

Let $\Delta$ be a set of propositional premises, and $\phi$ denotes a conclusion, we have $\Delta \vDash \phi$ implies $\Delta \vdash \phi$.

The meaning of the above statement is that if $\Delta$ entails $\phi$ (can be verified using truth-table), then there exists a proof that brings us from $\Delta$ to $\phi$.




## Other proof systems

There is some other proof system that makes our propositional proof less structural hence more suitable for proving meta theory; while there is other that focuses on canonicalizing the premises and intermediate propositions. We leave them out here as further readings.


## Further Readings


* http://intrologic.stanford.edu/chapters/chapter_04.html
* http://intrologic.stanford.edu/chapters/chapter_05.html (what we covered)
* http://intrologic.stanford.edu/chapters/chapter_06.html
