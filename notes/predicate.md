---
title: '50.057 Predicate Logic'
author:
- ISTD, SUTD
header-includes:
  - \usepackage{newunicodechar}
  - \newunicodechar{ℕ}{\ensuremath{\mathbb{N}}}
  - \newunicodechar{∀}{\ensuremath{\forall}}
---


# 50.057 Predicate Logic

## Learning Outcomes

1. List the difference between predicate logic and propositional logic
1. List the syntax elements of predicate logic
1. Apply deduction proof in simple predicate logic

## Predicate Logic


Predicate Logic is an altnerative to the propostional logic that supports variables and their quantification. 

Let's begin a motivating example. 

Suppose we want to use logic to express the system that if person A knows person B, then B knows A. To do that in propositional logic, we have to encode this requirement by enumerating 

$$
ada\_knows\_beatrice \\ 
beatrice\_knows\_ada \\ 
ada\_knows\_cara \\ 
cara\_knows\_ada \\ 
...
$$

It is simply an inadequate representation. It would be nice if we could say

$$ 
\forall x\in Obj . (\forall y \in Obj . (knows(x,y) \implies knows(y,x)))
$$ 


Where $Obj$ defines a **finite** set of objects. 


$$
Obj = \{ ada, beatrice, cara, daphne \} 
$$

### Syntax of Predicate Logic

In predicate logic, instead of using "hard-coded" atom as simple predicate, we define a 
set of objects, Variables such as $x$, $y$ and $z$ are quantified from their domains. 
In this case, their domain must be $Obj$. "$\forall$" reads as "for all". An universal quantifier followed by a variable declares a universally quantified sentence. (For brevity, we drop the domain of variable when there is no confusion arises.) For example 


$$ 
\forall x . (\forall y. (knows(x,y) \implies knows(y,x)))
$$ 

introduce two universally quantified variables $x$ and $y$, where $x$'s scope is 

$$
\forall y. (knows(x,y) \implies knows(y,x))
$$

and $y$'s scope is 

$$
(knows(x,y) \implies knows(y,x))
$$

Besides universal quantifier, the existential quatifier is supported in predicate logic. 

$$
\exists z. (knows(ada, z) \wedge knows(cara, z))
$$

which says there exists a person whom both Ada and Cara know.

On the other hand, $knows(\_,\_)$ is a predicate. A predicate cannot be an object and vice versa. A predicate defines some association between objects. Note that predicates can be unary, and n-ary too.

There are three non-syntactical implicit restrictions (for the time-being).

1. Objects must be finite, violating which leads us to first-order logic
1. Predicate's argument must be a **simple objects** or variable, violating which leads us to first-order logic.
1. A variable's domain must be objects, violating which leads us to higher-order logic. 


#### Precedence level

The precdence level of predicate logic is the same as the one of propositional logic, 
except that the universal and exitential quantifiers have the strongest prcedence level. For example, $\exists x. good(x) \wedge \exists y. bad(y)$ is parsed as $(\exists x. good(x)) \wedge (\exists y. bad(y))$.




#### A quick summary

These are the summary of Predicate Logic's syntax.

1. Variables: $x$, $y$, $z$ we will mostly use these 3 alphabets to represent variables, if we need more, we will mention explicitly.
1. Objects: $ada$, $cat$, $rain$, ... any lower case term that is not $x$, $y$ or $z$ and there is not followed by open and close paranethesis.
1. Predicates: $works(\_,\_)$, $knows(\_,\_)$, $good(\_)$.
1. Connectives: $\neg$, $\wedge$, $\vee$, $\implies$, $\iff$. 
1. Quantifiers: $\forall$ and $\exists$.


### Semantic of Predicate Logic

#### Free variables
A sentence is *grounded* iff there is no free variable in it. The set of free variables appearing a sentence is defined as follows

$$
\begin{array}{rcl}
 fv(x) & = & \{ x \} \\ 
 fv(object) & = & \{ \} \\ 
 fv(p(\psi_1,...,\psi_n)) & = & fv(\psi_1) \cup ... \cup fv(\psi_n) \\ 
 fv(\psi \wedge \phi) & = & fv(\psi) \cup fv(\phi) \\ 
 fv(\psi \vee \phi) & = & fv(\psi) \cup fv(\phi) \\ 
 fv(\psi \implies \phi) & = & fv(\psi) \cup fv(\phi) \\ 
 fv(\psi \iff \phi) & = & fv(\psi) \cup fv(\phi) \\ 
 fv(\neg \psi ) & = & fv(\psi) \\ 
 fv(\forall x.\psi) & = & fv(\psi) - \{x\} \\ 
 fv(\exists x.\psi) & = & fv(\psi) - \{x\} 
\end{array}
$$

$fv(\psi)$ denotes a meta function that extracts the free variables from a sentence $\psi$. 

For instance, consder

$$
\begin{array}{rcl}
fv(\exists z.(knows(ada,z)\wedge knows(cara,z))) & = \\
fv((knows(ada,z)\wedge knows(cara,z))) - \{ z \} & =  \\ 
(fv(knows(ada,z)) \cup fv(knows(cara,z))) - \{ z \} & = \\
(\{z\} \cup \{z\}) - \{ z \} & = \\ 
\{\}
\end{array} 
$$

Therefore $\exists z.(knows(ada,z)\wedge knows(cara,z))$ is a ground sentence.

On the other hand, $good(x)$ is not a ground sentence.


#### Unquantified ground sentences

The semantics for this subset is the same as the one for propositional logic, i.e. we can evaluate a non-quantified ground sentence based a particular truth-assignment. For instance if $knows(ada, cara)$ is 1 and $knows(cara, daphne)$ is 0, then evaluating $knows(ada, cara) \vee knows(cara, daphne)$ returns 1.

> Note: Recall in propositional logic, a truth assignment maps atom sentences to 0 or 1 thus we can evaluate compound sentences to either 0 or 1. In preidcate logic, a truth assignment maps grounded non-compound relational predicates to 0 or 1 thus we can evaluate compound sentences to eitehr 0 or 1.

#### Quantified ground sentences

To understand the semantic of the quantified ground sentences, we need an additional definition.

##### Instantiation

An instance of a sentence is a version in which all free variables are replaced by ground terms. In the current version the only possible ground terms are objects. For example an instance of $knows(ada,z)$ is $knows(ada, cara)$.


##### Evaluation 

A universal quantified sentence is evaluated to 1 for a truth assignment if and only if every instance of the scope of the quantified sentence is 1 for that assignment. 

An existentially quantified sentence is evaluated to 1 for a truth assignment if and only if some instance of the scope of the quantified sentence is 1 for that assignment.

For example, let $Obj = \{ada, beatrice, cara, daphne\}$ and suppose the
truth assignment contains

$$
knows(ada, cara) = 1, \qquad knows(cara, cara) = 0,
$$

with the remaining values determined by the assignment. Then

$$
\exists z. knows(ada,z)
$$

is evaluated to 1, because the instance $knows(ada,cara)$ is 1. In contrast,

$$
\forall z. knows(cara,z)
$$

is evaluated to 0 because at least one instance, namely $knows(cara,cara)$, is 0. Evaluation therefore asks whether a quantified sentence is true under one particular truth assignment.

Another example, consider the truth assignment

$$
knows(ada, cara) = 1, \qquad knows(cara, betraice) = 1, \\
knows(beatrice, daphne) = 1, \qquad knows(daphne, ada) = 1 
$$

under which the following sentence stating "every one knows some one"

$$
\forall x. \exists y. knows(x, y)
$$

evaluates to 1.

##### Satisfaction

* A truth assignment satisfies a sentence with free variables if and only if it satisfies every instance of that sentence. 

* A truth assignment satisfies a set of sentences if and only if it satisfies every sentence in the set.

For example, consider the sentence with one free variable

$$
knows(x,cara).
$$

A truth assignment satisfies this sentence only if every instance is true. In particular, it must satisfy all of

$$
knows(ada,cara),\quad knows(beatrice,cara),\quad
knows(cara,cara),\quad knows(daphne,cara).
$$

If even one of these instances is 0, the assignment does not satisfy $knows(x,cara)$. 

Similarly, an assignment satisfies the set

$$
\{knows(x,cara),\;\exists z. knows(ada,z)\}
$$

only when it satisfies both sentences: every instance of the first sentence must be 1, and at least one instance of the second sentence must be 1. Satisfaction therefore describes whether a truth assignment meets a sentence or a collection of sentences.


#### Defining new predicate from the existing predicates

One very cool idea of predicate logic is to allow new predicates to be defined in terms of the existing ones. 

For example, if we want to define a predicate "connector". A person is a connector if she knows everyone. Instead of enumerating how a connector person knows another person via the $knows(\_,\_)$ predicate, we could 

$$
\forall x. (connector(x) \iff (\forall y. knows(x,y)))
$$

> Comparing the terminology used here with the one mentioned in the Stanford's course: In Stanford's course, this version of predicate logic is called the **Relational Logic**. The semantics in this writeup is largely adopted from the one introduce in the Stanford's course.


### Proof System - Natural Deduction


The Natural Deduction proof system for predicate logic is a natural extension to the propositional logic. Besides ($\implies$Elim), ($\implies$Intro),  ($\wedge$Elim), ($\wedge$Intro), ($\vee$Elim), ($\vee$Intro), ($\neg$Elim), ($\neg$Intro), ($\iff$Elim), ($\iff$Intro), we have the following additional rules

The propositional rules keep the same meaning when their propositions are
predicate-logic formulas. For example, each of the following is a valid use of
the corresponding rule.

##### Implication Elimination ($\implies$Elim)

From $knows(ada,cara) \implies trusts(cara,ada)$ and
$knows(ada,cara)$, derive $trusts(cara,ada)$.

##### Implication Introduction ($\implies$Intro)

If a sub-proof temporarily assumes $knows(x,y)$ and derives
$knows(y,x)$, the assumption can be discharged to derive
$knows(x,y) \implies knows(y,x)$.

##### Conjunction Elimination ($\wedge$Elim)

From $knows(ada,cara) \wedge knows(ada,daphne)$, derive
$knows(ada,cara)$ or derive $knows(ada,daphne)$.

##### Conjunction Introduction ($\wedge$Intro)

From $knows(ada,cara)$ and $knows(cara,daphne)$, derive
$knows(ada,cara) \wedge knows(cara,daphne)$.

##### Disjunction Elimination ($\vee$Elim)

From $knows(ada,cara) \vee knows(ada,daphne)$, together with

$$
knows(ada,cara) \implies connected(ada)
$$

and

$$
knows(ada,daphne) \implies connected(ada),
$$

derive $connected(ada)$. Both alternatives lead to the same conclusion.

##### Disjunction Introduction ($\vee$Intro)

From $knows(ada,cara)$, derive
$knows(ada,cara) \vee knows(ada,daphne)$. It is enough to establish one
disjunct.

##### Negation Elimination ($\neg$Elim)

From $\neg\neg knows(ada,cara)$, derive $knows(ada,cara)$.

##### Negation Introduction ($\neg$Intro)

If assuming $follows(ada,ada)$ leads both to $p$ and to $\neg p$, derive
$\neg follows(ada,ada)$. The contradictory consequences show that the
assumption cannot hold.

##### Biconditional Elimination ($\iff$Elim)

From

$$
connector(x) \iff \forall y. knows(x,y),
$$

derive either direction:

$$
connector(x) \implies \forall y. knows(x,y)
$$

or

$$
(\forall y. knows(x,y)) \implies connector(x).
$$

##### Biconditional Introduction ($\iff$Intro)

If both directions have been proved,

$$
connector(x) \implies \forall y. knows(x,y)
$$

and

$$
(\forall y. knows(x,y)) \implies connector(x),
$$

then derive

$$
connector(x) \iff \forall y. knows(x,y).
$$


#### Universal Elimination ($\forall$Elim)

$$
\begin{array}{c} 
\forall x. \psi  \\ 
\tau\ {\tt is\ ground} \\ 
\hline
\left[\tau/x\right]\psi
\end{array}
$$


Where $[\tau/x]\psi$ reads as "substituting all occurrences of the free variable $x$ in $\psi$ by $\tau$. The substitution operation is defined as follows.

$$
\begin{array}{rcll}
\left[\tau / x \right]x & = & \tau \\ 
\left[\tau / x \right] \psi \wedge \phi & = & (\left[\tau / x \right] \psi) \wedge (\left[\tau / x \right]\phi)  \\ 
\left[\tau / x \right] \psi \vee \phi & = & (\left[\tau / x \right] \psi) \vee (\left[\tau / x \right]\phi)  \\ 
\left[\tau / x \right] \neg \psi  & = & \neg (\left[\tau / x \right] \psi)  \\ 
\left[\tau / x \right] \psi \implies \phi & = & (\left[\tau / x \right] \psi) \implies (\left[\tau / x \right]\phi)  \\ 
\left[\tau / x \right] \psi \iff \phi & = & (\left[\tau / x \right] \psi) \iff (\left[\tau / x \right]\phi)  \\ 
\left[\tau / x \right] \forall y . \psi & = & \forall y.(\left[\tau/x\right]\psi) & {\tt if}\ x \not= y \wedge y\not\in fv(\tau) \\ 
\left[\tau / x \right] \exists y . \psi & = & \exists y.(\left[\tau/x\right]\psi) & {\tt if}\ x \not= y \wedge y\not\in fv(\tau) 
\end{array}
$$

In the last two cases, we have a side condition ${\tt if}\ x \not= y \wedge y\not\in fv(\tau)$; when the side condition is not met, we have to rename $y$ consistently in $\psi$ so that it won't clash with $x$ and free variables in $\tau$.

The above subsitution operation is (overly) generalized to handle scenarios where $\tau$ might contain free variable. In the current context, $\tau$ is always grounded. 

So the Universal Elimination rule say that if $\forall x. \psi$ is true, $\psi$ should remain true regardless what ground instance we give to $x$.

For example, from

$$
\forall x. knows(x,cara)
$$

we may instantiate $x$ with any ground object in $Obj$. In particular, we may
derive

$$
knows(ada,cara), \qquad knows(beatrice,cara), \qquad
knows(daphne,cara).
$$

The chosen term must be ground. Thus, Universal Elimination does not permit us
to replace $x$ with another free variable when the rule requires a ground instance.

Let's consider another example (adopted from Stanford's course), suppose we have 

$$
\forall y.\exists z.follows(y,z)
$$

and

$$
\forall x.\forall y.(\exists z.follows(y,z) \implies  follows(x,y))
$$

as premises. We want to verify that 

$$
follows(ada, cara)
$$


The first premise means "each person must follow someone". 
The second premise means "for a person to follow a followee, that followee must follow someone also".

We establiash the proof as follows

$$
\begin{equation*}
\begin{array}{|r|l|l|}
\hline
1. &    \forall y.\exists z.follows(y,z)	& {\tt Premise} \\ \hline
2. &	\forall x.\forall y.(\exists z.follows(y,z) \implies  follows(x,y))	& {\tt Premise} \\ \hline
3. &	\exists z.follows(cara,z)	 & \forall {\tt Elim}: 1 \\ \hline
4. &	\forall y.(\exists z.follows(y,z) \implies  follows(ada,y))	& \forall {\tt Elim}: 2 \\ \hline
5. &	\exists z.follows(cara,z) \implies  follows(ada,cara)	& \forall {\tt Elim}: 4 \\ \hline
6. &	follows(ada,cara)	& \implies {\tt Elim}: 5,3 \\ \hline
\end{array}
\end{equation*}
$$

At step 3, we substitute the universal quantified variable $y$ by $cara$.
At step 4, we substitute the universal quantified variable $x$ by $ada$.
At step 5, we substitute the universal quantified variable $y$ by $cara$.
At step 6. we apply implication elimination to derive the conclusion.


#### Universal Introduction ($\forall$Intro)

$$
\begin{array}{c} 
\psi  \\ 
\tau\ {\tt is\ not\ used\ in\ any\ active\ assumption} \\ 
\hline
\forall x. \left[x/\tau\right]\psi
\end{array}
$$

The premise $\tau\ {\tt is\ not\ used\ in\ any\ active\ assumption}$ means that the sub predicate $\tau$ inside $\psi$ is not used as premises nor a substitution in any preceeding step on the current level and parent level of the proof. 


For example, let $a$ be a fresh object symbol that does not occur in any active
assumption. If a sub-proof derives

$$
knows(a,cara),
$$

without using any fact that is special to $a$, then we may generalize the
fresh symbol and conclude:

$$
\forall x. knows(x,cara).
$$

The freshness condition is essential. From the assumption $knows(ada,cara)$,
we may derive that same fact, but we may not conclude
$\forall x. knows(x,cara)$, because the proof used a fact specifically about
Ada rather than an arbitrary object.


Let's consider another example, we start from the same premises as the last example appeared in the $\forall {\tt Elim}$ rule. We want to verify a stronger conclusion

$$
\forall x.\forall y.follows(x,y)
$$

$$
\begin{equation*}
\begin{array}{|r|l|l|}
\hline

1. &	\forall y.\exists z.follows(y,z)	                                    & {\tt Premise} \\ \hline
2. &	\forall x.\forall y.(\exists z.follows(y,z) \implies  follows(x,y))	& {\tt Premise} \\ \hline
3. &	\exists z.follows(d,z)	                                            & \forall {\tt Elim}: 1 \\ \hline
4. &	\forall y.(\exists z.follows(y,z) \implies  follows(c,y))	        & \forall {\tt Elim}: 2 \\ \hline
5. &	\exists z.follows(d,z) \implies  follows(c,d)	                    & \forall {\tt Elim}: 4 \\ \hline
6. &	follows(c,d)	                                                    & \implies {\tt Elim}: 5,3 \\ \hline
7. &	\forall y.follows(c,y)	                                            & \forall {\tt Intro}: 6 \\ \hline
8. &	\forall x.\forall y.follows(x,y)	                                & \forall {\tt  Intro}: 7  \\ \hline
\end{array}
\end{equation*}
$$

At step 3, we eliminate the $\forall$ quantified variable by introducing a *placeholder* object $d$. $d$ is a reserved (yet universally quantified) object to denote the follower of the $follows(\_,\_)$ predicate.  However it does not refer to a specific object (person). 
At step 4, we apply the same trick to eliminate $x$ with a placeholder object $c$.
At step 6, we apply the implication elimination to derive $follows(c,d)$.
Since $c$ and $d$ are placeholder objects, they are not appearing in any active assumption, they can be any object, hence at steps 7-8, we apply $\forall {\tt Intro}$ to generalize the predicate into a universally quantifed predicate. 

#### Existential Introduction ($\exists$Intro)

$$
\begin{array}{c}
\psi \\
\tau\ {\tt is\ ground} \\
\hline
\exists x. \left[x/\tau\right]\psi
\end{array}
$$

This rule says that if a predicate holds for one particular ground term, then
there exists an object for which the predicate holds. The term used in the
premise becomes the witness for the existential statement.

For example, from

$$
knows(ada,cara)
$$

we may use $ada$ as a witness and conclude:

$$
\exists x. knows(x,cara).
$$

The rule does not require us to identify every object satisfying the predicate;
one valid witness is sufficient.


#### Existential Elimination ($\exists$Elim)

$$
\begin{array}{c}
\exists x. \psi \\
\left[\tau/x\right]\psi \vdash \phi \\
\tau\ {\tt is\ not\ used\ in\ any\ active\ assumption\ or\ in\ }\phi \\
\hline
\phi
\end{array}
$$

This rule allows us to reason about an object whose existence is guaranteed,
without needing to know which object it is. We introduce a fresh ground term
$\tau$ as a temporary name for an arbitrary witness, derive the desired
conclusion, and then discharge that temporary name.

For example, suppose we have the following premises

$$
\exists x. knows(x,cara)
$$

and

$$
\forall x. (knows(x,cara) \implies connected(cara)).
$$

We want to show that 

$$
connected(cara)
$$


Using a fresh witness $a$, the sub-proof is:

$$
\begin{equation*}
\begin{array}{|r|c|l|}
\hline
1. & \exists x. knows(x,cara) & {\tt Premise} \\ \hline
2. & \forall x. (knows(x,cara) \implies connected(cara)) & {\tt Premise} \\ \hline
3.1. & knows(a,cara) & a\ {\tt is\ not\ used\ in\ any\ active\ assumption\ or\ in\ }connected(cara) \\ \hline
3.2. & knows(a,cara) \implies connected(cara) & \forall{\tt Elim}\ 2 \\ \hline
3.3. & connected(cara) & \implies{\tt Elim}\ 3.1, 3.2 \\ \hline
3. & connected(cara) & \exists\ {\tt Elim}: 1, 3.1 - 3.3 \\ \hline
\end{array}
\end{equation*}
$$


At step 3.1, we find a placeholder object $a$ which is not mentioned in any active assumption, it is also no in the conclusion $connected(cara)$. 
At step 3.2, we apply ($\forall$Elim) to the step 2.
At step 3.3, we apply implication elimination to derive $connected(cara)$.
At step 3, we apply existential eliminiation to the sub-proof 3.1-3.3. 


> Comparing with the Existential Elimination rule in the stanford course `http://intrologic.stanford.edu/chapters/chapter_10.html`. The version defined here is "equivalent" to the version in the stanford course yet simpler. The trick is to use the sub-proof in the premise, while the version mentioned in the stanford course uses direct proof without sub-proof in the premise. 


#### Further readings 

http://intrologic.stanford.edu/sections/section_07.html?section=6
http://intrologic.stanford.edu/sections/section_07.html?section=7
http://intrologic.stanford.edu/sections/section_07.html?section=8

