# 50.057 Predicate Logic

## Learning Outcomes

1. List the difference between predicate logic and propositional logic
1. List the syntax elements of predicate logic
1. Apply deduction proof in simple predicate logic
1. List the difference between simple predicate logic and first order logic
1. Apply linear induction proof in first order logic

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

\begin{equation*}
\begin{array}{|r|c|l|}
\hline
1. & \exists x. knows(x,cara) & {\tt Premise} \\ \hline
2. & \forall x. (knows(x,cara) \implies connected(cara)) & {\tt Premise} \\ \hline
3.1. & knows(a,cara) & a\ {\tt is\ not\ used\ in\ any\ active\ assumption\ or\ in\ }connected(cara) \\ \hline
3.2. & knows(a,cara) \implies connected(cara) & \forall{\tt Elim}\ 2 \\ \hline
3.3. & connected(cara) & \implies{\tt Elim}\ 3.1, 3.2 \\ \hline
3. & connected(cara) & \exists\ {\tt Elim}: 3.1 - 3.3 \\ \hline
\end{array}
\end{equation*}

At step 3.1, we find a placeholder object $a$ which is not mentioned in any active assumption, it is also no in the conclusion $connected(cara)$. 
At step 3.2, we apply ($\forall$Elim) to the step 2.
At step 3.3, we apply implication elimination to derive $connected(cara)$.
At step 3, we apply existential eliminiation to the sub-proof 3.1-3.3. 


> Comparing with the Existential Elimination rule in the stanford course `http://intrologic.stanford.edu/chapters/chapter_10.html`. The version defined here is "equivalent" to the version in the stanford course yet simpler. The trick is to use the sub-proof in the premise, while the version mentioned in the stanford course uses direct proof without sub-proof in the premise. 


#### Further readings 

http://intrologic.stanford.edu/sections/section_07.html?section=6
http://intrologic.stanford.edu/sections/section_07.html?section=7
http://intrologic.stanford.edu/sections/section_07.html?section=8


## First-Order Logic 

Recall that we impose the following syntax restriction to the predicate logic.


1. Objects must be finite
1. Predicate's argument must be a simple objects or variable

In this section we start to consider an extension to our predicate logic where the above two restrictions are lifted. We call it First-Order Logic.


> In the stanford course, such an extension is called Term Logic or Herbrand Logic, which has some subtle difference between the actual first-order logic. In this course, we treat first-order logic and hebrand logic are the same for the ease of understanding.

After lifting the two syntax restrictions, we are allowed to write sentence such as 

$$loves(father(cara), mother(cara))$$

In the above, we have a some nesting predicate. In the presence of the complexity, we divide the predicates into three types of **terms**.

1. Atom objects (AKA simple terms), $cara$, $ada$, ...
1. Function, which takes a term and returns a term., e.g. $father(\_)$, father of Cara is a person is not a true or false value.
1. Relation, which takes a term and returns a truth-value, e.g. $loves(\_,\_)$

The sentence above means "Cara's father loves Cara's mother".


Let's consider another example.

#### Peano Arithmetic

Suppose we want to model natural number arithematics. In our system we have the following language

1. Atom: $zero$ ( which stands for the number 0 instead of the logical false value.)
1. Function: $suc(\_)$ return the next natural number, for instance, $suc(zero)$ is 1 (the number 1, not the logical true value.), $suc(suc(zero))$ is 2, ... 
1. Relations: $even(\_)$ and $odd(\_)$. $even(zero)$, $odd(suc(zero))$, ... 

Now the cool thing is that without the need to enumerating all the $even$ and $odd$ relations with ground terms, we can define them recursively as follows


* Base cases (EvenZero) and (NegOddZero)

$$
even(zero) \\ 
\neg odd(zero)
$$

* Recursive cases (EvenSuc) and (OddSuc)

$$
\forall x. (odd(suc(x)) \iff even(x)) \\ 
\forall x. (even(suc(x)) \iff odd(x))
$$

The above definitions are called **axioms**. We can think of axioms are the "global" premises, which are assumed to be valid.


Before getting into more complex operation with the peano numbers. Let's go back to discusss the semantics of the first-order logic for a short while.


### Semantics

The semantic of first-order logic is a faithful extension to the one we explained earlier. 

Truth values are assigned to all the ground predicates (i.e. relation being applied to ground terms). 

However evaluation and satisfaction using truth-table becomes immediately infeasible because of the infinite number of ground terms.

The only practical approach is via proof.


### Proof System

The good news is that there is almost no change to the proof system. All the rules that we defined earlier are still applicable. 



#### Peano Arithmetic (Cont'd) - a simple proof

Our goal is to make use of the axioms (EvenZero), (NegOddZero), (EvenSuc) and (OddSuc), to 
verify the following

$$
    even(suc(suc(zero)))
$$

i.e. "2 is an even number".


To make our proof easier, let's derive some sub lemmas from the axioms.

#### Lemma 1:  "the successor of an even number is odd"

$$
\forall x. (even(x) \implies odd(suc(x)))
$$

The proof goes as follows

$$
\begin{array}{|r|c|l|}
\hline
1.  & \forall x. (odd(suc(x)) \iff even(x)) & {\tt Axiom (OddSuc)} \\ \hline
2.  & odd(suc(n)) \iff even(n) & \forall {\tt Elim}: 1 \\ \hline
3.  & even(n) \implies odd(suc(n)) & \iff {\tt Elim}: 2 \\ \hline
4.  & \forall x. (even(x) \implies odd(suc(x))) & \forall {\tt Intro}: 3 \\ \hline
\end{array}
$$

#### Lemma 2: "the successor of an odd number is even"


$$
\forall x. (odd(x) \implies even(suc(x)))
$$

The proof goes as follows

$$
\begin{array}{|r|c|l|}
\hline
1.  & \forall x. (even(suc(x)) \iff odd(x)) & {\tt Axiom (EvenSuc)} \\ \hline
2.  & even(suc(m)) \iff odd(m) & \forall {\tt Elim}: 1 \\ \hline
3.  & odd(m) \implies even(suc(m)) & \iff {\tt Elim}: 2 \\ \hline
4.  & \forall x. odd(x) \implies even(suc(x)) & \forall {\tt Intro}: 3 \\ \hline
\end{array}
$$

##### Main proof of "2 is an even number"

$$
\begin{array}{|r|c|l|}
\hline
1.  & even(zero) & {\tt Axiom (EvenZero)} \\ \hline
2.  & \forall x. (even(x) \implies odd(suc(x))) & {\tt Lemma 1} \\ \hline
3.  & \forall x. (odd(x) \implies even(suc(x))) & {\tt Lemma 2} \\ \hline
4.  & even(zero) \implies odd(suc(zero)) & \forall {\tt Elim}: 2 \\ \hline
5.  & odd(suc(zero)) & \implies {\tt Elim}: 1, 4 \\ \hline
6.  & odd(suc(zero)) \implies even(suc(suc(zero))) & \forall {\tt Elim}: 3 \\ \hline
7.  & even(suc(suc(zero))) & \implies {\tt Elim}: 5, 6 \\ \hline
\end{array}
$$

Steps 1-3 are re-iterating the relevant axiom and lemmas.
Steps 4-7, we apply ($\forall$ Elim) and ($\implies$ Elim) to conclude the goal. 

From steps1 - 5, we also verified "1 is an odd number".


If we continue from the above proof, we can also prove  "3 is an odd number" 

$$
\begin{array}{|r|c|l|}
\hline
8.  & even(suc(suc(zero))) \implies odd(suc(suc(suc(zero))) & \forall {\tt Elim}: 2 \\ \hline
9.  & odd(suc(suc(suc(zero)))) & \implies {\tt Elim}: 7, 8 \\ \hline
\end{array}
$$

### Limitation of the proof by deduction

However the deduction proof can only prove ground predicate. We can't use it to prove a general term.
Suppose we want to verify that "adding 2 to an even number gives us an even number; adding 2 to an odd number givus an odd number."
Formally, our goal is to show that 

$$
\forall x. ( (even(x) \implies even(suc(suc(x)))) \wedge (odd(x) \implies odd(suc(suc(x)))) )
$$

It is impossible to enumerate all the objects in the natural numbers.
We need to consider a sound-and-complete version of the induction. 


#### Linear Induction

Linear Induction works when the domain of term consists of an atom object $o$ and a unary function $f$ that takes a term returns the next term. 

$$
\begin{array}{c}
\psi(o) \\ 
\forall x. (\psi(x) \implies \psi(f(x))) \\ 
\hline  
\forall x. \psi(x)
\end{array}
$$

The first premise in the above inference rule is called tbe *base case* and the 2nd premise is called the *inductive case*.
The antecedent of the inductive case is called the *inductive hypothesis*, and the consequent is called the *inductive conclusion*.


Let's apply the above inference rule to the sentence that being considered. 


\begin{equation*}
\begin{array}{c}
even(zero) \implies even(suc(suc(zero))) \wedge 
odd(zero) \implies odd(suc(suc(zero))) \\
even(suc(zero)) \implies even(suc(suc(suc(zero)))) \wedge 
odd(suc(zero)) \implies odd(suc(suc(suc(zero)))) \\
\forall x. \left ( \begin{array}{rcl}
             ( (even(x) \implies even(suc(suc(x)))) & \wedge &
               (odd(x)  \implies odd(suc(suc(x)))) ) \\ 
             & \implies &  \\
             ( (even(suc(x)) \implies  even(suc(suc(suc(x))))) & \wedge &
               (odd(suc(x))  \implies  odd(suc(suc(suc(x)))))
             )
             \end{array}
            \right ) \\  
\hline  
\forall x. ( (even(x)  \implies  even(suc(suc(x)))) \wedge (odd(x)  \implies  odd(suc(suc(x)))) )
\end{array}
\end{equation*}

##### Base Case: zero 

The proof of the predicate 

$$
even(zero) \implies even(suc(suc(zero)))
$$

is identical to the above "simple proof", except that $even(zero)$ is a premise instead of an axiom.


The proof of the predicate 

$$
odd(zero) \implies odd(suc(suc(zero)))
$$

is obviously valid because $odd(zero)$ is false. 


##### Base Case: suc(zero)

To finish this base case we first record that $1 = suc(zero)$ is not even.

$$
\begin{array}{|r|c|l|}
\hline
1.  & \neg odd(zero) & {\tt Axiom (NegOddZero)} \\ \hline
2.  & \forall x.  even(suc(x)) \iff odd(x) & {\tt Axiom (EvenSuc)} \\ \hline
3.  & even(suc(zero)) \iff odd(zero) & \forall {\tt Elim}: 2 \\ \hline
4.  & even(suc(zero)) \implies odd(zero) & \iff {\tt Elim}: 3 \\ \hline
5.1. & even(suc(zero)) & {\tt Assumption} \\ \hline
5.2. & odd(zero) & \implies {\tt Elim}: 4, 5.1 \\ \hline
5.3. & \neg odd(zero) & {\tt Axiom (NegOddZero)} \\ \hline
5.  & \neg even(suc(zero)) & \neg {\tt Intro}: 5.1 - 5.3 \\ \hline
\end{array}
$$

From $\neg even(suc(zero))$ the antecedent of $even(suc(zero)) \implies even(suc(suc(suc(zero))))$ is false, so that implication holds vacuously and
the first conjunct of the base case at $suc(zero)$ is discharged.

The predicate $odd(suc(zero)) \implies odd(suc(suc(suc(zero))))$ is valid
because we have verified "1 is an odd number" and "3 is an odd number" in the earlier section.







##### Inductive case

Let $x$ be arbitrary. The induction hypothesis is not needed explicitly here:
the two parity lemmas, instantiated at successive terms, directly establish
the required successor implication.

$$
\begin{array}{|r|c|l|}
\hline
1.  & \forall y. (even(y) \implies odd(suc(y))) & \text{Lemma 1} \\ \hline
2.  & \forall y. (odd(y) \implies even(suc(y))) & \text{Lemma 2} \\ \hline
3.  & even(suc(x)) \implies odd(suc(suc(x))) & \forall \text{Elim}: 1 \\ \hline
4.  & odd(suc(suc(x))) \implies even(suc(suc(suc(x)))) & \forall \text{Elim}: 2 \\ \hline
5.1. & even(suc(x)) & \text{Assumption} \\ \hline
5.2. & odd(suc(suc(x))) & \implies \text{Elim}: 3, 5.1 \\ \hline
5.3. & even(suc(suc(suc(x)))) & \implies \text{Elim}: 4, 5.2 \\ \hline
5.  & even(suc(x)) \implies even(suc(suc(suc(x)))) & \implies \text{Intro}: 5.1 - 5.3 \\ \hline
6.  & odd(suc(x)) \implies even(suc(suc(x))) & \forall \text{Elim}: 2 \\ \hline
7.  & even(suc(suc(x))) \implies odd(suc(suc(suc(x)))) & \forall \text{Elim}: 1 \\ \hline
8.1. & odd(suc(x)) & \text{Assumption} \\ \hline
8.2. & even(suc(suc(x))) & \implies \text{Elim}: 6, 8.1 \\ \hline
8.3. & odd(suc(suc(suc(x)))) & \implies \text{Elim}: 7, 8.2 \\ \hline
8.  & odd(suc(x)) \implies odd(suc(suc(suc(x)))) & \implies \text{Intro}: 8.1 - 8.3 \\ \hline
9.  & \begin{array}{c} 
        (even(suc(x)) \implies even(suc(suc(suc(x))))) \wedge \\ 
        (odd(suc(x)) \implies odd(suc(suc(suc(x))))) 
      \end{array} & \wedge \text{Intro}: 5, 8 \\ \hline
10.1. & \begin{array}{c} 
           (even(x) \implies even(suc(suc(x)))) \wedge \\ 
           (odd(x) \implies odd(suc(suc(x)))) 
        \end{array} & \text{Assumption} \\ \hline
10.2. & \begin{array}{c}
        (even(suc(x)) \implies even(suc(suc(suc(x))))) \wedge \\
       (odd(suc(x)) \implies odd(suc(suc(suc(x))))) 
        \end{array} & \text{Reiteration}: 9 \\ \hline
10.  & \begin{array}{c} 
        ((even(x) \implies even(suc(suc(x)))) \wedge 
       (odd(x) \implies odd(suc(suc(x))))) \\ 
       \implies \\ 
       ((even(suc(x)) \implies even(suc(suc(suc(x))))) \wedge
       (odd(suc(x)) \implies odd(suc(suc(suc(x)))))) 
       \end{array}
       & \implies \text{Intro}: 10.1 - 10.2 \\ \hline
11. & \forall x.\left( \begin{array}{c} 
        ((even(x) \implies even(suc(suc(x)))) \wedge
        (odd(x) \implies odd(suc(suc(x))))) \\ 
        \implies \\
        ((even(suc(x)) \implies even(suc(suc(suc(x))))) \wedge
        (odd(suc(x)) \implies odd(suc(suc(suc(x)))))) 
        \end{array} \right)
       & \forall \text{Intro}: 10 \\ \hline
\end{array}
$$

Thus the inductive case is established. Together with the two base cases,
linear induction proves the desired statement for every Peano number.



#### Tree Induction

Linear induction works because the Peano numerals form a **chain**: one base object $zero$ and one unary function $suc$ that steps from a number to its successor, so the inductive premise $\psi(x) \implies \psi(suc(x))$ moves along a single spine.

The family terms of the earlier example, $loves(father(cara),\ mother(cara))$, do not form a chain. From any person $p$ there are *two* parents, $father(p)$ and $mother(p)$; from each of those there are two more; and so on. The ancestry of a person is therefore a **tree**:

$$
p,\quad father(p),\ mother(p),\quad father(father(p)),\ mother(father(p)),\ father(mother(p)),\ mother(mother(p)),\ \dots
$$

What matters is that this tree is *regular*: there is a single type (persons), and every node has exactly two successors (the father and the mother). That regularity is precisely what separates this case from its two neighbours. It has more than one successor, so it lies beyond **linear** induction; but its branching is uniform, so it is more restricted than **structural** induction, where different constructors have different arities. Induction over such a regular tree is **tree induction**, the intermediate form.

To keep the induction well founded, let the domain be the family of a base person $r$: $r$ and everyone obtained from $r$ by repeatedly applying $father$ and $mother$. Every such person is finitely many steps from $r$, so the induction is well founded. The principle is: to prove a property $P$ of every person in this family, it suffices to prove the base case and the two branches, i.e. that the property is inherited from a person to their father and from a person to their mother:

$$
\begin{array}{c}
P(r) \\
\forall p.  P(p) \implies P(father(p)) \\
\forall p.  P(p) \implies P(mother(p)) \\
\hline
\forall p.  P(p)
\end{array}
$$

The first line is the *base case*; the second and third are the *paternal* and *maternal* *branches*. This is the intermediate position: linear induction has one branch (a unary successor); tree induction has a fixed number of same-typed branches (here two, the parents); structural induction has one case per constructor with a variable number of recursive sub-terms.

Now take $P(p)$ to be $loves(father(p), mother(p))$ — "the parents of $p$ love each other" — and suppose the following axioms, where the second and third record the distinction between the paternal and the maternal side:

* **Base.** $loves(father(r), mother(r))$. The base person's own parents love each other.
* **Paternal.** $\forall p.  loves(father(p), mother(p)) \implies loves(father(father(p)), mother(father(p)))$. If a person's parents love each other, so do the paternal grandfather and the paternal grandmother.
* **Maternal.** $\forall p.  loves(father(p), mother(p)) \implies loves(father(mother(p)), mother(mother(p)))$. If a person's parents love each other, so do the maternal grandfather and the maternal grandmother.

Our goal is the general claim, for every $p$ in the family,

$$
P(p)\ \equiv\ loves(father(p), mother(p)),
$$

"every father loves every mother, provided they are the parents of a common child." We verify it by tree induction.

* **Base case.** $P(r) = loves(father(r), mother(r))$ holds by the Base axiom.
* **Inductive case.** Fix an arbitrary $p$ and assume $P(p)$; both branches then follow from the axioms:

\begin{equation*}
\begin{array}{|r|c|l|}
\hline
1.  & loves(father(p), mother(p)) & \text{Assumption } P(p) \\ \hline
2.  & \forall q.  loves(father(q), mother(q)) \implies loves(father(father(q)), mother(father(q))) & \text{Axiom (Paternal)} \\ \hline
3.  & loves(father(p), mother(p)) \implies loves(father(father(p)), mother(father(p))) & \forall \text{Elim}: 2 \\ \hline
4.  & loves(father(father(p)), mother(father(p))) & \implies \text{Elim}: 3, 1 \\ \hline
5.  & \forall q.  loves(father(q), mother(q)) \implies loves(father(mother(q)), mother(mother(q))) & \text{Axiom (Maternal)} \\ \hline
6.  & loves(father(p), mother(p)) \implies loves(father(mother(p)), mother(mother(p))) & \forall \text{Elim}: 5 \\ \hline
7.  & loves(father(mother(p)), mother(mother(p))) & \implies \text{Elim}: 6, 1 \\ \hline
\end{array}
\end{equation*}

Step 4 is $P(father(p))$, discharging the paternal branch; step 7 is $P(mother(p))$, discharging the maternal branch. Both are derived from the single hypothesis $P(p)$.

Since the base case and both branches hold, tree induction gives $P(p)$ for every person $p$ in the family: every father loves every mother, provided they share the same child. This is the intermediate form — more branching than linear induction, but more regular than the structural case that follows.



#### Structural Induction  

Tree induction handles *regular* trees, where every node has the same number of successors of the same type, as in the family example above. The most general terms are less regular: they are built by *several different constructors*, some with no recursive sub-terms and some with several, and the recursive sub-terms may even be of different types. 


Suppose we introduce a new binary function $add(\_,\_)$ and a binary predicate $eq(\_,\_)$ to our Peano system. The following axioms describe equality and addition.

* Equal case (Eq)

$$
    \forall x. eq(x, x)
$$


*  Not Equal base case (NEqBase)

$$
    \forall x.(\neg eq(zero,suc(x)) \wedge \neg eq(suc(x),zero))
$$

* Not Equal recursive case (NEqRec)


$$
    \forall x.\forall y.(\neg eq(x,y) \implies \neg eq(suc(x),suc(y)))
$$

* Add base case: zero is a left identity of $add$ (AddZero)

$$
    \forall x. eq(x, add(zero,x))
$$

* Add recursive case (AddSuc)

$$ 
    \forall x. \forall y. (eq(add(suc(x), y), add(x, suc(y))))
$$

## The Structural-Induction Principle

The terms of this arithmetic system are generated by

$$
Term \;::=\; zero \mid suc(Term) \mid add(Term,Term)
$$

The term zero is a base constructor. The constructors suc and add contain recursive sub-terms: suc has one sub-term, while add has two. The term

The example term is `add(suc(zero), add(suc(suc(zero)), zero))`.

contains an addition node with two independently constructed sub-terms. This is exactly the situation for which structural induction is needed.

Let $P(t)$ be a property of terms. To prove that $P$ holds for every term generated by this grammar, it is enough to establish one case for each constructor:

$$
\begin{array}{c}
P(zero) \\
\forall x. (P(x) \implies P(suc(x))) \\
\forall x.\forall y. ((P(x) \wedge P(y)) \implies P(add(x,y))) \\
\hline
\forall t. P(t)
\end{array}
$$

The first premise is the base case. The second is the inductive case for the unary constructor $suc$. The third is the inductive case for the binary constructor $add$; it supplies **two** induction hypotheses, one for each recursive argument.

## A Normalisation Property

We use $eq(t,u)$ to mean that the two terms denote the same natural number. The equality and addition axioms above allow us to rewrite additions of numeral terms. In particular, AddSuc moves one successor from the left argument to the right argument:

$$
add(suc(x),y) \quad\longrightarrow\quad add(x,suc(y)),
$$

and AddZero removes the zero left argument:

$$
add(zero,y) \quad=\quad y.
$$

Let a **numeral** be a term of the form

$$
zero,\quad suc(zero),\quad suc(suc(zero)),\quad \ldots
$$

Define $P(t)$ to mean:

> There is a numeral $n$ such that $eq(t,n)$.

Concretely we can define $P(t)$ as follows

* Base case numeral axiom

$$
        num(zoro) 
$$

* Recursive case numeral axioms

$$
        \forall x. (num(x) \implies num(suc(x)))
$$

Then $P(t)$ is 

$$
        P(t) \equiv \exists x. (eq(t, x) \wedge num(x))
$$

In words, $P(t)$ says that the term $t$ can be reduced to a Peano numeral. We prove $\forall t. P(t)$ by structural induction.

## Normalisation: Base Case

The base term is $zero$. It is already a numeral. Therefore $P(zero)$ holds by choosing $zero$ as the numeral. This is witnessed explicitly by the Eq axiom:

$$
eq(zero,zero).
$$

## Normalisation: Successor Case

Assume the induction hypothesis $P(x)$. Then there is a numeral $n$ such that $eq(x,n)$.

By equality replacement, $eq(suc(x),suc(n))$. Since $suc(n)$ is a numeral, $P(suc(x))$ follows.

The induction hypothesis is about an arbitrary term $x$; we do not need to inspect the internal shape of $x$ again.

## Normalisation: Addition Case

Assume the two induction hypotheses

$$
P(x) \wedge P(y).
$$

Then there are numerals $m$ and $n$ such that

$$
eq(x,m) \qquad\text{and}\qquad eq(y,n).
$$

By equality replacement, it is enough to normalise $add(m,n)$. We use the following auxiliary lemma:

> For every pair of numerals $m$ and $n$, there is a numeral $k$ such that $eq(add(m,n),k)$.

The lemma is proved by linear induction on $m$. For the base case, AddZero gives $eq(add(zero,n),n)$. For the inductive case, assume the lemma for $m$ and instantiate it with $suc(n)$:

$$
eq(add(m,suc(n)),k).
$$

AddSuc and transitivity of equality then give

$$
eq(add(suc(m),n),add(m,suc(n)))
\quad\text{and}\quad
eq(add(suc(m),n),k).
$$

Thus the lemma holds for every pair of numerals. Repeated applications of AddSuc move all successors from the left numeral to the right numeral; when the left argument reaches $zero$, AddZero removes it. Therefore, for some numeral $k$,

$$
eq(add(m,n),k).
$$

Therefore $add(m,n)$, and hence $add(x,y)$, is equal to a numeral. This proves $P(add(x,y))$.

## The Complete Structural Proof

The three cases can be displayed as follows:

$$
\begin{array}{|r|l|l|}
\hline
1. & P(zero) & \text{Base case: } zero \text{ is a numeral} \\ \hline
2. & P(x) \implies P(suc(x)) & \text{Successor case} \\ \hline
3. & (P(x) \wedge P(y)) \implies P(add(x,y)) & \text{Addition case} \\ \hline
4. & \forall t. P(t) & \text{Structural induction}: 1,2,3 \\ \hline
\end{array}
$$

The proof has one case for each constructor in the grammar. In the $add$ case, both sub-term hypotheses are available simultaneously. A linear induction rule would provide only one hypothesis and would therefore be insufficient for this term language.

## A Worked Term

Consider

$$
t = add(suc(zero), add(suc(suc(zero)),zero)).
$$

The right sub-term is normalised first:

$$
add(suc(suc(zero)),zero)
\quad\longrightarrow\quad
add(suc(zero),suc(zero))
\quad\longrightarrow\quad
add(zero,suc(suc(zero)))
\quad=\quad suc(suc(zero)).
$$

Then the whole term becomes

$$
add(suc(zero),suc(suc(zero)))
\quad\longrightarrow\quad
add(zero,suc(suc(suc(zero))))
\quad=\quad suc(suc(suc(zero))).
$$

Thus $P(t)$ holds. The proof of this one term follows the same three constructor cases used by the general structural-induction proof.

## Structural Induction Compared

The three forms of induction now have a clear relationship:

* **Linear induction** walks a chain: one base constructor and one unary successor, as with Peano numerals.
* **Tree induction** walks a regular tree: a fixed number of same-typed branches, as with the two parents in the family example.
* **Structural induction** handles a grammar with several constructors and varying arities. Here, $zero$ has no recursive sub-terms, $suc$ has one, and $add$ has two.

Structural induction is the appropriate principle whenever the recursive structure is determined by a grammar rather than by one fixed successor operation.

## Multidimension Induction



The equality axioms also support a useful parity theorem. 



### Theorem: Opposite Parity Implies Inequality

Prove

$$
\begin{aligned}
\forall x.\forall y. \big(&((even(x) \wedge odd(y)) \implies \neg eq(x,y)) \\
                         &\wedge ((odd(x) \wedge even(y)) \implies \neg eq(x,y))\big).
\end{aligned}
$$

The proof may use the following axioms:

$$
even(zero)
\qquad
\neg odd(zero)
$$

$$
\forall x. (odd(suc(x)) \iff even(x))
\qquad
\forall x. (even(suc(x)) \iff odd(x))
$$

and the equality axioms NEqBase and NEqRec.

However we need some multidmension induction as the conclusion (the goal) of the proof contains multiple nested universal quantifers. 

### The Multidimension Principle

For a property $P(x,y)$ of two natural numbers, we can induct on $x$ while keeping $y$ arbitrary. Define

$$
Q(x)\ \equiv\ \forall y. P(x,y).
$$

Then it is enough to prove $Q(zero)$ and

$$
\forall x. (Q(x) \implies Q(suc(x))).
$$

The induction hypothesis $Q(x)$ is stronger than a statement about one particular $y$: it gives $P(x,y)$ for every $y$. In the successor case, we may then analyse the arbitrary $y$ by its two constructors, $zero$ and $suc(y')$. This combination of induction and case analysis is often called **multidimension induction**.

### Defining the Property

Let

$$
\begin{aligned}
D(x,y)\ \equiv\ &((even(x) \wedge odd(y)) \implies \neg eq(x,y)) \\
                  &\wedge ((odd(x) \wedge even(y)) \implies \neg eq(x,y)).
\end{aligned}
$$

We prove $\forall x.\forall y. D(x,y)$ by induction on $x$, with $y$ universally quantified in the induction predicate.

### Base Case: $x = zero$

We must prove $D(zero,y)$ for an arbitrary $y$.

* The second implication is immediate because $odd(zero)$ is false.
* For the first implication, suppose $even(zero) \wedge odd(y)$. Since $y$ is a natural number, consider its two cases.
    * If $y=zero$, then $odd(y)$ contradicts $\neg odd(zero)$.
    * If $y=suc(y')$, then NEqBase gives $\neg eq(zero,suc(y'))$.

Therefore $D(zero,y)$ holds for every $y$.

### Inductive Case: $x = suc(x')$

Assume the induction hypothesis

$$
\forall y. D(x',y).
$$

We must prove $D(suc(x'),y)$ for an arbitrary $y$. Again, split on the shape of $y$.

#### Subcase: $y = zero$

Both implications in $D(suc(x'),zero)$ have the same conclusion:

$$
\neg eq(suc(x'),zero),
$$

which follows immediately from NEqBase. Hence $D(suc(x'),zero)$ holds.

#### Subcase: $y = suc(y')$

For the first implication, assume

$$
even(suc(x')) \wedge odd(suc(y')).
$$

By the parity axioms,

$$
even(suc(x')) \implies odd(x')
\qquad\text{and}\qquad
odd(suc(y')) \implies even(y').
$$

The second conjunct of the induction hypothesis $D(x',y')$ therefore gives

$$
\neg eq(x',y').
$$

Applying NEqRec yields

$$
\neg eq(suc(x'),suc(y')).
$$

For the second implication, assume

$$
odd(suc(x')) \wedge even(suc(y')).
$$

The parity axioms now give $even(x') \wedge odd(y')$. The first conjunct of $D(x',y')$ gives $\neg eq(x',y')$, and NEqRec again gives

$$
\neg eq(suc(x'),suc(y')).
$$

Thus $D(suc(x'),suc(y'))$ holds.

### Conclusion

The base case and the inductive case establish

$$
\forall x.\forall y. D(x,y).
$$

Unfolding $D$ gives the desired result: two Peano numbers with opposite parity cannot be equal. The proof is multidimensional because the induction predicate quantifies over $y$, and the inductive step must reason about the structure of both $x$ and $y$.

### Direct Pair-Induction Form

The same proof can be presented as induction over the pair $(x,y)$. Define the stronger property

$$
P(x,y) \equiv
((even(x) \wedge odd(y)) \vee (odd(x) \wedge even(y)))
\implies \neg eq(x,y).
$$

The required conclusion is the conjunction of the two implications in the exercise. The pair-induction proof has three kinds of cases.

* **Base case: $(zero,zero)$.** Since $\neg odd(zero)$, both parity combinations in the antecedent of $P(zero,zero)$ are false. Therefore $P(zero,zero)$ holds.
* **Mixed cases.** If $x=zero$ and $y=suc(y')$, NEqBase gives $\neg eq(zero,suc(y'))$. If $x=suc(x')$ and $y=zero$, NEqBase gives $\neg eq(suc(x'),zero)$. Thus both mixed cases hold.
* **Successor case.** Assume $P(x',y')$. The parity axioms give

  $$
  even(suc(x')) \iff odd(x')
  \qquad
  odd(suc(y')) \iff even(y').
  $$

  Hence

  $$
  even(suc(x')) \wedge odd(suc(y'))
  \implies odd(x') \wedge even(y'),
  $$

  so the induction hypothesis gives $\neg eq(x',y')$. NEqRec then gives $\neg eq(suc(x'),suc(y'))$. The other parity combination similarly reduces to $even(x') \wedge odd(y')$, and the same induction hypothesis and NEqRec apply.

Therefore the base, mixed, and successor cases establish

$$
\forall x.\forall y.\left(
((even(x) \wedge odd(y)) \implies \neg eq(x,y)) \wedge
((odd(x) \wedge even(y)) \implies \neg eq(x,y))
\right).
$$

### Further Reading 

1. http://intrologic.stanford.edu/chapters/chapter_11.html
2. http://intrologic.stanford.edu/chapters/chapter_12.html
3. http://intrologic.stanford.edu/chapters/chapter_13.html
