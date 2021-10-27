# Unit 1 Review

**Discrete Mathematics**

*Benjamin Fry*

## Chapter 1

### Definitions

#### Sets

A set is an unordered collection of distinct objects. Some common sets are

The **Natural Numbers** $\mathbb{N} = \{0, 1, 2, ...\}$

> The smallest natural number is **zero** for the purposes of this class. 

The **Integers** $\mathbb{Z} = \{..., -3, -2, -1, 0 , 1, 2, 3, ...\}$

> Integers strictly greater than zero are the **positive integers**
>
> Integers strictly less than zero are the **negative integers**

The **Rational Numbers** $\mathbb{Q}$ are the set of all numbers that can be written in the form $\frac{a}{b}$ where a and b are integers and $b \ne 0$

The **Real Numbers** $\mathbb{R}$ are the set of all rational and irrational numbers.

> We have not defined the irrational numbers, but the definition of irrationals cannot be the non-rational reals because the definition of real would be circular. 
>
> The imaginary numbers also were left up to us to define. 



#### Divisibility

Let  a and b be integers. We say that a is divisible by b and write $a|b$ (read a divides b or b is a factor of a) if there exists an integer c such that a = bc.

We are allowed to write division only if the divisor is irrefutably nonzero.



#### Parity 

The state of being even or odd. We may assume every integer is even or odd.

##### Even

Let x be an integer. x is even if $2|x$.

##### Odd

Let y be an integer. y is odd if $\exists \ b \in \mathbb{Z}$ such that $y = 2b + 1$

For integers, we know that:

even + even = even

even + odd = odd

odd + odd = even

even * even = even

odd * odd = odd

even * odd = even

#### Prime and Composite

Every integer greater than one is either prime or composite. 

##### Prime

Let p be an integer. p is prime if $p > 1$ and the only positive factors of $p$ are $1$ and $p$



##### Composite

Let x be an integer. x is composite if $x > 1$ and $\exist \ y \in \mathbb{Z}$ such that $1 \lt y \lt x$ and $y|x$





#### Absolute Value and Square Roots

##### Absolute Value

Let $x \in \mathbb{R}$. The absolute value of x, denoted  $|x|$, is the distance x is from zero. That is
$$
|x| = \begin{cases} x : x>0 \\ -x : x<0 \end{cases}
$$

##### Square Root

Let $y \in \mathbb{R}$. A square root of y, denoted $\sqrt{y}$ is a number z such that $y = z^2$.

This does not imply we only use nonnegative roots. 



#### Floor and Ceiling

#### Floor

Let $x \in \mathbb{R}$. The floor of x, denoted $\lfloor{x} \rfloor$ is the largest integer n such that $n \le x$. If $n = \lfloor x \rfloor$ then $n \le x \lt n + 1$

##### Ceiling

Let $y \in \mathbb{R}$. The ceiling of y, denoted $\lceil{y} \rceil$ is the largest integer n such that $n \ge y$. If $n = \lceil y \rceil$ then $n -1 \lt y \le n$

If x is an integer, then $\lfloor x \rfloor = \lceil x\rceil$



### Theorem

A theorem is a declarative statement for which there is a proof - a proof is an essay that incontrovertibly shows a statement is true.

#### Useful Axioms

Let  $x, y, z \in \mathbb{R}$

##### Closure

$x + y$ and $xy$ are also real numbers

##### Commutative

$x + y = y + x$

$xy = yx$

##### Associative

$(x + y) + z = x + (y + z)$

$(xy)z = x(yz)$

##### Substitution

If $x = y$ and $x = z$, then $y = z$

##### Transitivity

If $x \le y$ and $y \le z$, then $x \le z$

##### Others

If $xy = 0$, then at least one of x and y equals 0.

If $x,y \gt 0$ then $xy \gt 0$. 



#### Logic Statements

##### If-Then

Take the form if [statement A] then [statement B]. 

The contrapositive takes the form If (not B), then (not A). The contrapositive is always true if the original statement is true. It is logically equivalent to the original statement and can be proven so with a truth table. 

The converse takes the form If B then A which is true in if and only if statements but might not be otherwise. 

The inverse takes the form if not A then not B which generally is not true. 

A is said to be a **sufficient condition** for B 

B is said to be a **necessary condition** for A

To disprove an if then statement, only the case where A occurs and B does not occur shows a violation of the statement. 

| A     | B     | is possible? |
| ----- | ----- | ------------ |
| True  | True  | Possible     |
| True  | False | Impossible   |
| False | True  | Possible     |
| False | False | Possible     |

Essentially if-then says whenever A is true, B is also true. If A is not true, we make no claim about how B should be. 

##### If and Only If (IFF)

An if then statement that takes the for: If A then B and If B then A. 

| A     | B     | is possible? |
| ----- | ----- | ------------ |
| True  | True  | Possible     |
| True  | False | Impossible   |
| False | True  | Impossible   |
| False | False | Possible     |

Only the cases where both occur or neither occur are possible. 

##### And/Or/Not

Exactly the same as in programming. OR is inclusive OR so both can be true and still be valid. 

##### Vacuous Truths

We can be tempted to call things false when they are ridiculous, however if they take the form of an If-Then statement, we can only prove them impossible if they fall into an impossible row of the tables above. 

> If an integer is both a perfect square and prime, then it is negative.
>
> There are no prime perfect squares, so there are no cases in which A and not B so there is no way to disprove in if statement form. Thus, this is a vacuous truth - it is meaningless. 



### Proof

Since we cannot prove something is true by exhaustion for an infinite set of numbers, we have to be able to show that it is true in the general case. 

#### IF-Then Direct Proof

To write a direct proof:

1. Convert the given statement to If-Then form
2. Write the beginning of the proof (what you're given) then write the end of the proof (where you want to go)
3. Unravel the definitions of what you've been given at BOTH ENDS. 
4. Think what we know and what we need to show and connect the unraveled definitions. 

#### IFF Direct Proof

A is said to be a necessary and sufficient condition for B and the same for B for A.

To prove an if and only if statement, we need to prove both the statement and its converse: prove $A\implies B$ and that $B \implies A$

### Counterexample

A statement can be irrefutably proven false with only one counterexample that contradicts the statement. The easiest way to disprove an $A \implies B$ is to find an example of $A$ occurring in the absence of $B$. 

### Boolean Algebra

There are 3 main operations in Boolean Algebra: 

Logical AND, OR, and NOT and they can be combined. A tautology is a statement that is always true. 

$True \ \and False = False$

$True \or False = True$

$True \and \lnot False = True$

To prove logical statements like this, we can prove by exhaustion of all possibilities. If you're proving something equals something else,  you can just construct a truth table that has all combinations of the input variables and show that in every case the left side and the right size of the expression are the same. 



## Chapter 2

### Lists

A list is an ordered sequence of objects written with numbers comma separated between parentheses:
$$
(1, 2, 3)
$$
the elements can repeat as in $(1, 2, 3, 3)$ and the number of elements in the list is its length. A list of length 2 is called and ordered pair and a list of k elements is called a k-tuple. A list of zero elements is denoted $()$. 

Two lists are equal provided they have the same length and elements in the corresponding positions: 

Lists $(a, b, c)$ and $(x,y,z)$ are equal IFF $a = x, b=y, c=z$

**Counting Lists**

When counting the number of possible lists we can make, we use the multiplication rule which states that the number of possible lists is:
$$
\prod_{i = 1}^n w_i
$$
where i is the i^th^ element of the list, and $w_i$ is the number of possibilities that can take that position in the list, and n is the number of list elements. 

When the number of options for each element is the same for each index and the length of the list is $k$, then the total number of lists can be written $n^k$

When the pool of things to select from decreases every time an element is filled in the list (repetitions are forbidden), we can use *falling factorial* to count the number of possible lists:
$$
(n)_k = n(n-1)(n-2)...(n-k+1)
$$
where n is the number of elements to choose and k is the length of the list. 

When solving these problems, draw out a list of boxes and fill the boxes to visualize, when there are weird rules try drawing a tree diagram. 

When repetitions are forbidden and every option will be used ($k = n$), we can write the number of possibilities with factorial notation:
$$
n! = (n)_n = n(n-1)(n-2)...(1)
$$
Additionally, we define $0! = 1$ because it is useful when multiplying factorials and it as a result of defining the empty product as 1. 

The triangular numbers are the numbers that take the form of the factorial but are added rather than multiplied as they describe the number of points in a triangle dot diagram:
$$
T_n = n + (n-1) + (n - 2) + ... + 2 + 1
$$
and in this case we define $T_0 = 0$ rather than 1 because the empty sum evaluates to zero. (recall the number factory example in week 3)

### Sum and Product Notation

We often use summation notation which takes the form: 
$$
\sum _{k=m}^n a_k
$$
where k is the index of summation, m is the lower limit and n is the upper limit. The upper limit is inclusive. If k is not less than n, then this is the empty sum and it evaluates to zero. 

Geometric sequences are useful when dealing with sums. A sequence is a list of numbers. A geometric sequence takes the form $a, ar, ar^2, ar^3 ...$ which can be written the nth term is found by multiplying the (n-1)^st^ term by r where we call r the common ratio such that $r \not =0$

Sum of a finite geometric sequence:

![image-20210224223421799](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210224223421799.png)

we can prove this by setting the LHS equal to S, multiplying both sides by r, and rearranging the sum to get S to show up again which we can then solve for. The two cases would have to be done separately.

Similarly, we use the product notation:
$$
\prod _{k=m}^n a_k
$$
when k > n similar to the empty sum this is the empty product and nothing is multiplied, however we have established that the empty product always evaluates to 1.

Useful properties:

![image-20210224224019567](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210224224019567.png)

The index of the sum can be decreased by subtracting the first summand, the upper limit of the sum can be decreased by adding the last value back. 

### Sets I

A set is by definition repetition free and unordered. An object is either in or out and thus cannot be in it multiple times. We have already seen the sets $\mathbb{Z}$, $\mathbb{R}$, and $\mathbb{Q}$. A multiset is an unordered collection of objects that aren't necessarily unique. 

When an object belongs to a given set, it is an element of that set. 

We define the *cardinality* of a set to be the number of objects in it and it is denoted $|A|$ for the set $A$. If the cardinality is an integer, the set is finite, otherwise it is an infinite set. 

The empty set $\empty$ is the set that has no elements and is a subset of all other sets. 

We use set builder notation to denote the elements of a list which takes the form {dummy variable : conditions} for example:


$$
\{x : x \in \mathbb{Z}, x\ge 0\}
$$
which is the set of all objects x such that x is an element of the integers and x is greater than or equal to zero.

To prove set equality, we have to show that every element in A is in B and that every element of B is also in A. 

We say A is a subset of B if every element of A is also in B. This is denoted $A \sube B$. Every set is a subset of itself and the null set is a subset of every set because every element of it (nothing) passes being in the set. When a set is a proper or strict subset of another, it is not equal to that set and can be denoted $A \sub B$. 

To prove a set is a subset of the other, we just need to prove that every element of that set is in the other set. 

If A is a set, then $x \in A$ IFF $\{x\} \sube A$ which is proven in the text. 

We define a Pythagorean Triple as the set of lists of integers such that:
$$
\{(a,b,c):a,b,c\in \mathbb{Z}\ and \ a^2 + b^2 = c^2\}
$$
Counting subsets, a nice visual way to do this is by drawing a tree diagram where each split in the branches breaks into a branch where an element is included or excluded an example is on page 48 of the text. However, there is a general solution since each element can either be in or out of the subset so each element has two options and thus, the number of possible subsets is simply:
$$
no. subsets = 2^{|A|}
$$
Proving this introduces the idea of proof by bijection which mean explaining that two counting problems have the same answer because they use different forms of the same idea. The explanation is done more verbally than direct proof.

Sets can be elements of other sets. We define the power set to be the set of all subsets of A. For example, the powerset of $A = \{1,2,3\}$ is:
$$
2^{A}=\{\empty, \{1\},\{2\},\{3\},\{1,2\},\{1,3\},\{2,3\},\{1,2,3\}\}
$$
because we know the general formula for the number of subsets, we know that the cardinality of a powerset is given by 2^|A|^ and  because of this fact, we abbreviate the powerset of A with 2^A^

Because the powerset is a set of sets, only sets are elements of the powersets and sets of sets are subsets of the powerset. 

By transitivity, if $A\sube B$ and $B \sube C$, then $A \sube C$

### Quantifiers

We need to be able to convert speech to mathematical statements so need to clarify meanings. The main distinguishing thing is the difference between there exists and every. 

We use there exists to imply that at least one such example exists. More may exist but there is at least one. It is written: $\exists x\in \mathbb{Z}$ for there exists an integer x. To prove a statement of existence, we simply have to provide an example that fits the given definitions. 

The other main quantifier is the $\forall x \in A$ this is a statement that for every single possible x, the statement holds. This is called the universal qualifier. To prove universal statements like these, we need to show that the statement is true in the general case or by exhaustion. 

The negation of quantified statements usually flips the quantifier and adds a $\lnot$ to the right side of the statement. Saying that not even a single element exists that satisfies the statement is the same as saying all elements do not satisfy the statement. The logical not can be written around the entire statement and then we can flip the quantifier and negate the inside of the statement. 

We can prove combination statements by showing something is true in the general case. The order matters in these kinds of statements, for example:
$$
\forall x,\exist y, x + y = 0
$$
which is true because for any x, we can chose -x to equal zero. However, the statement:
$$
\exist y, \forall x, x + y = 0
$$
is false because it implies that there exists a $y$ such that anything added to it equals zero which is not true. The statements are clearer if you add parentheses around the second statement. 

### Sets II

A useful thing to know proved in lecture is that for integers n and k such that k is between 1 and n inclusive, the number of multiples of k in this interval is floor(n/k)

##### Union and Intersection

The most basic operations. The union of two sets is the set of all elements that are in A or B or both for $A$ and $B$ it is denoted $A\cup B$ and is defined symbolically as:
$$
A \cup B = \{x : x \in A \or x\in B\}
$$
The intersection of two sets is the set of all elements that are in both A and B. The intersection is denoted $A \cap B$ 
$$
A \cap B = \{x : x\in A \and x\in B\}
$$
We can visualize these operations with Venn diagrams.

##### Properties of Set Operations

The commutative property: 

$A\cup B = B \cup A$ 

$A\cap B = B \cap A$

The associative property:

$A\cup (B\cup C) = (A\cup B)\cup C$

$A\cap (B\cap C) = (A\cap B)\cap C$

The identity? property:

$A \cup \empty = A$

$A \cap \empty = A$

$A \cap A = A$

$A \cup A = A$

The Distributive Property:

$A\cup (B\cap C) = (A\cup B)\cap (A\cup C)$

$A\cap (B\cup C) = (A\cap B)\cup (A\cap C)$

##### The Size of Unions

The general formula for the size of the union of finite sets is:
$$
|A| + |B| = |A\cup B| + |A\cap B|
$$
which we can rearrange to solve for the size of the union or the intersection given we know one or the other via the inclusion-exclusion principle. It is useful to subtract the intersection over to solve for the union when finding the cardinality of the intersection, A and B is easier than finding their union. 

We can prove statements like this similar to the bijective proof but call it a combinatorial proof which shows that an equation is true by creating a question and arguing that both sides of the equation answer that question. If both sides correctly answer the question, then they must be equal.

When the sets are disjoint or mutually exclusive, the intersection between them is the null set and the cardinality of their union is the sum of their individual cardinalities.

A and B are disjoint sets provided $A \cup B = \empty$ given a collection of sets, these sets are all pairwise disjoint if the intersection between each of them is the null set or in other words, no two of them have an element in common. 

##### Set Difference and Symmetric Difference

If A and B are sets, the set difference $A - B$ is the set of all elements of A that are not in B which we can write:
$$
A-B = \{x:x\in A \ and \ x\not\in B\}
$$
We define the symmetric difference of A and B as the set of all elements in A but not in B OR in B but not in A which we can express as the union of the differences:
$$
A \Delta B = (A- B)\cup(B-A)
$$
we can think of this as the logical XOR of the two sets. Another way to write this is as the union minus the intersection:
$$
A \Delta B = (A\cup B) - (A\cap B)
$$
When we prove things with unions in the general case, we will probably have to consider the case where our dummy variable is an element of either side separately and conclude the desired result in each separate case. The book really emphasizes unravelling the definitions as far as possible and then working up from where you want to go by what you need to show to find the connection even in subcases. 

When the two cases are just reversals of the variables we can write WLOG (without loss of generality) or by the same argument as above but this is risky and you should only do it when you're absolutely sure the two cases evaluate the same way. This is particularly useful when an equation is the same and variables are interchangeable. 

De Morgan's Laws: 

$A - (B\cup C) = (A-B)\cap (A-C)$

$A - (B\cap C) = (A-B) \cup (A-C)$

##### Complement

We define the complement of the set A which is a subset of the set universe U as:
$$
\overline A = U - A
$$
the properties of which are:

$\overline {\overline A} = A$

$\overline{A\cup B} = \overline {A} \cap \overline {B}$

$\overline{A\cap B} = \overline {A} \cup \overline {B}$

Sometimes, it is easier to count with complements, we may know the total number of sets with a property and the total number of sets with another, the set with both of those properties is the difference. 



##### Cartesian Product

We denote the cartesian produce of seta A and B as $A\times B$ and and we think of it as the set of all ordered pairs formed by taking an element from A together with an element of B in all possible ways:
$$
A \times B = \{(a, b) : a\in A, b\in B\}
$$
When A and B are not the same set, $A \times B$ might not be equivalent to $B \times A$

The times operator is used because the product of the individual cardinalities is equal to the cardinality of the cartesian product:
$$
|A\times B| = |A| \times|B|
$$

### Relations

A relation is a comparison between two objects. The objects are other in or out of the relation based on the rule that defines it. Examples include greater than, divisibility, and equality. Mathematically, we define a relation as simply a set of ordered pairs, however this makes the connection between the ordered pairs unclear. Rather, we think of the relation as a test. If x and y pass that test, then we can write $x R y$ and we find the ordered pair (x, y) as an element of the relation. 

We can use $xRy$ to express the fact that $(x, y) \in R$. 

For example, we could define the less than or equal to relation as the set of integers as follows:
$$
R = \{(x,y) : x,y \in \mathbb{Z} \ and \ y-x \in \mathbb{N}\}
$$

##### Relation On vs From

We define a relation R on the set A provided $R \sube A\times A$

We define a relation R from the set A to the set B provided $R \sube A \times B$ which recall means the first element of the ordered pair will be an element of A and the second element of the ordered pair will be an element of B.

Since relations are also sets, we can apply whatever set operations we want to them such as intersection, difference etc... We say the relation $R \cap (A\times A)$ is the relation R restricted to the set A and call the relation $R \cap (A\times B)$ the relation is restricted from A to B.

##### Inverse Relation

The inverse relation of $R$ is denoted $R^{-1}$ which is the relation formed by reversing the order of all the ordered pairs in R:
$$
R^{-1} = \{(x,y):(y,x)\in R\}
$$
If R is on A, then R^-1^ is also on A. If R is from A to B, then R^-1^ is from B to A.

The inverse of the inverse relation is just the relation. To prove relation equality, we just use the same proof algorithm as for set equality (basically the IFF proof).

##### Properties of Relations

Reflexive:

​	If for all $x \in A, (x,x)\in R$ then R is called Reflexive.

Irreflexive:

​	If for all $x\in A, (x,x)\not\in R$, then R is Irreflexive.

Symmetric:

​	If for all $x, y \in A$ we have $(x,y)\in R \implies (y,x)\in R$, then R is symmetric.

Antisymmetric:

​	If for all $x, y \in A$, we have $((x,y)\in R \and (y,x)\in R) \implies x = y$ then R is antisymmetric

Transitive:

​	 If for all $x, y, z \in A$, we have $((x,y)\in R \and (y,z)\in R) \implies x = z$, then R is transitive.

To show a relation has a given property, you have to write a proof unless otherwise stated and to disprove a relation having a prove provide a counterexample. 

For example, the equality relation is reflexive because any integer is equal to itself, it is symmetric because if x equals y, then y equals x, it is antisymmetric because x equaling y and y equaling x does imply that x equals y, and it is transitive, because if x equals y and y equals z, the x equals z. The relation is not irreflexive because x equals x is by definition in the relation. 

Another example is the < operator, which is not reflexive because x < x is never true. It is irreflexive for that reason though. It is not symmetric because x < y does not imply that y < x. The relation is **antisymmetric but vacuously so** because there are no cases in which x and y could simultaneously satisfy x < y and y < x and thus there is no way to disprove that such a case occurring would not imply equality. Be careful not to just assume the relation is not one of these properties because it cannot happen!! Finally, x < y is transitive because a < b and b < c does imply that a < c.

The antisymmetric property is tricky. For example the division relation x|y, if x and y are natural numbers, given x|y and y|x, then x = y, however for the integers, -3|3 and 3|-3, however, the two are not equal so the division operator would not be antisymmetric in that universe. 

Furthermore, not being symmetric does not imply antisymmetry or vice versa neither does not being irreflexive imply being reflexive or vice versa (shown with the empty set).

##### Partial Order Relation

A partial order relation is a relation R on the set A such that R is reflexive, antisymmetric, and transitive. The ordered pair $P = (A, R)$ is called a partially ordered set or poset.

A total order on a set A is a partial order relation R that also satisfies the following requirement: For every pair $a, b \in A$ either $(a, b)\in R$ or $(b, a) \in R$ or both. This is also known as Totality/Completeness. 

##### Empty Relation

The empty relation on a nonempty set A is a relation for which no elements of A satisfy it. Many of the relation properties are satisfied vacuously by the empty set because no counterexamples exist and any hypothetical element of R may satisfy the conditions required by the relations. 

##### Equivalence Relations

Used to convey a sense of equality though generally outside the context of number equality.

A relation R on a set B is an equivalence relation if R is symmetric, reflexive, and transitive. The Relation may have more properties than this, but it may not have fewer. 

##### Equivalence Class

If R is an equivalence relation on a set A and $a \in A$, then the equivalence class of a, denoted [a], is the set of all elements of A related by R to a:

$[a] = \{x\in A: (x, a)\in R\}$

In the simplest terms, the subset of R that relates any element of A to a. Here a is just another element of A. This seems complicated for some reason but all its saying is that the equivalence class is the set of all elements that are 'equivalent' through the equivalence relation R to a.

Some properties of the equivalence class is that there is always at least one element in each equivalence class because R is by definition reflexive, a must be in its own equivalence class as $aRa$.

Furthermore, if $a,b \in A$ and $aRb$ then [a] = [b] which was proven in lecture. 

Even furthermore, if [a] and [b] are not disjoint, then [a] = [b] which was also proven in lecture. 

These statements make sense because recalling the definition of an equivalence class, these are things we are claiming to be "equal" to the class in some sense, if b is in a's equivalence class, then a must be in b's equivalence class and all the other elements should be too. These are statements of equality that are extended beyond the equality of integers. 

Proof of equivalence class statements are generally done by manipulating the statements that define the equivalence relation. 

