## Review Session

#### Exam Format

 Exam posted on blackboard and uploaded on Gradescope. Exams are open note but can't use google. 

#### Definitions, Theorems, Proofs, and Logic

If p then q

can be written $p \to q$

The converse is written If q then p or $q \to p$

The inverse is written if not p then not q or $\lnot p \to \lnot q$

The contrapositive is if not q then not p or $\lnot q \to \lnot p$



##### Number Sets:

The smallest natural number is zero and it is the set of positive numbers. The zero is the smallest natural number thing is a popular exam motif for the professor. 

$\mathbb{Z}$ are the integers

$\mathbb{Q}$ are the rationals which can be written as a ratio of integers

$\mathbb{R}$ are the reals.



##### Parity

The property of an integer of being even or odd. An integer is even if there exists an integer k such that x = 2k. An integer is odd if there exists an integer y such that y = 2k + 1

##### Divisibility

We say that a divides b if there exists some integer k such that ak = b

##### Floor and Ceiling (castello loves these!)

Floor of x is the largest integer n such that n $\le$ x

 Inequality is given by $n \le x \lt n+1$

Ceiling is the smallest integer m such that m is greater than or equal to x

Inequality is given by $m - 1 \lt n \lt m$

#### Direct Proof

 Proving an if A then B statement with definitions, theorems, algebra, etc...

> prove that the product of two odd integers is also odd.
>
> Start by giving names to two arbitrary integers:
>
> If x and y are odd integers, then xy is also odd
>
> > Let x, y be odd integers, given x is odd, there exists an integer a such that $a, b \in \mathbb{Z}$ st. $x = 2a+1$ and $y = 2b+1$. Thus xy = (2a+1)(2b+1) which can be written 4ab+ 2a + 2b + 1. We can write this as 2(2ab + a + b) +1. We know that ab + a + b is an integer due to closure of the integers under addition and multiplication. Therefore, xy = 2c +1 where x is an integer equal to 2ab + a + b



> prove that the product of two integers with different parities will be even
>
> in this proof, you have two cases to prove the case where x is even and y is odd and the case where y is even and x is odd. To avoid writing the same proof twice, we can let x be even and y be odd WLOG. We can do this if swapping the variable names gives the same proof. 
>
> > WLOG let x be even and y be odd. Then there exists integers k and l such that x = 2k and y = 2l + 1. Then 2k (2l_1) = 2(2kl + k) which inside is an integer, so this is even. 



> Prove that the floor of negative x is equal to the negative of the ceiling of x. 
>
> Grab the inequalities from above for ceiling and floor. 
>
> Let m = ceil x. Then m-1 < x$\le$ m $\implies$ $-m+1 \gt -x \ge -m$ which we can rewrite $-m \le x \lt -m +1$ which takes the form of the floor inequality. Thus, -m = floor(-x) = -ceil(x)

Disproving a statement, is done by providing a single example in which the statement doesn't apply. 

##### Counting

List problems: Apply the multiplication rule

A list is an ordered collection of objects as in (2, 3, 4, 5, 6). Repeats are allowed and order matters. 

The number of ways to create lists is just the product of the number of options for each element of the list. 

> a 6 letter string of letters. how many are possible:
>
> (_, _, _, _, _, _) given 26 letter options, there are 26^6^ possibilities,

> If the first character must be a p:
>
> there are 1 * 26^5^

> The number of string that do not have an x
>
> 25^6

> The number of strings that have at least one x
>
> The total number of strings - strings with no xs
>
> (this is the technique of complementary counting):
>
> ​	takes the total number of strings then remove the number of strings we don't want. 

> How many strings have no repeats?
>
> $(26)_5$

A anagram/rearrangement problem where repeats are not allowed:

there are $n!$ ways to arrange the letters of a word. 

When there are repeated elements, you have to divide out the repeated elements:

> Anagrams of Castello
>
> For every anagram of Castello, there is an equivalent option where the l's are swapped. There are 2 factorial ways to arrange L1 and L2. To account for the overcounting, the total number of ways to arrange the elements is 8!/2!

> Anagrams of ABCDE where AB are next to eachother
>
> There are 2! ways to arrange the block AB - AB or BA
>
> Rearrange AB with CDE had 4! arrangements
>
> Thus, the total number of ways to arrange are 2!*4!

### Summation and Products

Treat sums like loops in CS. 

### Sets

This was the largest and most difficult unit. Sets are the most fundamental unit of discrete math and thus this chapter is the most important in the class.

A set is an unordered collection of distinct objects.  Order does not matter and repeats are not allowed. 

Set builder notation is a way to indicate which elements are in the set

ex: A = $\{x \in \mathbb{N} : x \le 5\}$

##### Operations

A union B is the set of both A or B

A intersect B is the set of all objects in A and B

A - B  is the set of all objects in A but not B

$ A \Delta B$ is the union of A-B and B-A which is also the XOR

##### The Universe Set

The set of all objects we are considering in a particular problem. Usually a number set of sorts. 

The complement can be defined when we have a universe set. The complement of the set A is the $U - A$

##### Cartesian Product

Gives a set of ordered pairs. 

If A = {1, 2} and B = {7,8}

$ A \times A = \{(1, 1), (1, 2), (2, 1), (2, 2)\}$

$A \times B = \{(1, 7), (1, 8), (2, 7), (2, 8)\}$

##### Subsets

We say A is a subset of B if every element in A is also in B

A is a proper subset of B if A is a subset of B and A$\not =$ B. To prove that A is a proper subset of B need to show that some element of B is not in A **could be on exam**

##### Powerset

Defined as the set of all subsets for a particular set. There are 2^|A|^ such elements for the powerset of A. 

If A = {1, 2, 3}, then 2^A^ = {\null, {1}, {2}, {3}, {1,2}, {2, 3}, {1, 3}, {1, 2, 3}}

1 is not an element of the powerset

{1} is an element of the powerset

{1} **IS NOT** subset of the powerset

however, {{1}} **IS** a subset of the powerset

##### Cardinality

The cardinality of a set is the number of elements in the set.

##### Inclusion Exclusion Principle

$|A| + |B| = |A \cup B| + |A \cap B|$

$ |A \cup B \cup C|=|A| + |B| - |A \cap B|- |B \cap C|-|A \cap C| + |A\cap B \cap C|$



**Cardinality + PIE CROSSOVER**

**THIS WILL BE ON THE EXAM**

Let S = $\{x \in \mathbb{Z}: 1 \le x \le\}$ Let A = $\{x \in S: 2|x\}$ and Let B =  $\{x \in S: 3|x\}$

> Find $|A\cup B|$.
>
> To do this, use the PIE so we need to find the cardinality of A, the cardinality of B and the cardinality of the intersection. 
>
> The floor function gives the number of elements between 1 and n that are multiples of k when used like so: floor(n/k) = number of steps. **SHE COULD TEST x $ \le $ 0 in which case you have to add the case where k is 0** so the total number of steps is floor(n/k) + 1
>
> > |A| = floor(100/2) = 50
> >
> > |B| = floor(100/3) = 33
> >
> > $|A\cap B|$ IF 2|x and 3|x then 6|x and = floor(100/6)
> >
> > which we can use to solve for the union of sets.

##### Set Proofs

>  To prove that $A - (A\cap B) \sube A \cap \overline{B}$
>
>  Let x in A - AintB so x not in A int B and is in A. This, A in A int B complement because x is not in B. 
>
>  Reverse:
>
>  Let y in A and B complement. Then y in A and y in Bcomplement so y is not in B therefore, y is not in A int B but y is in A so y in A - AintB
>
>  Because both are subsets, they are equal. 



Generally to prove set equality, we have to show that A subsets B and that B subsets A and **YOU WILL LOSE HALF OF THE POINTS FOR ANY SET EQUALITY PROOFS IF YOU FORGET THIS**

You have to show both directions when the two sets are equal and in IFF proofs. 

#### Relations

A relation R is a set of ordered pairs. 

A relation can be on a set A: $R \sube A\times A$

A relation can also be from A to B: $R \sub A\times B$

Usually, there is some shared "quality" between the related elements. 

> Let R be the same parity relationship over the natural numbers
>
> > This relationship is reflexive because evbery number has the same parity as itself
> >
> > Irreflexive: (1, 1)  is an element of R since both 1 and 1 have the same parity this R is not irreflexive. 
> >
> > Symmetric: suppose (x,y) in R, x and y have the same parity so (y,x) have the same parity and thus (y, x) is also in R
> >
> > Antisymmetric (3, 5) have same parity and (5,3) also have the same parity but $5\not = 3$
> >
> > Transitive if (x, y) have the same parity, and (y,z) have the same parity, then (x, z) have the same parity.



##### Special Relations

If R is reflexive, antisymmetric, and transitive, then R is a partial order relation. 

If R is reflexive, symmetric, and transitive, then R is an equivalence relation

##### Equivalence Class [$\alpha$]

The equivalence class is the set of elements that are related to $\alpha$

> for the parity example, [0] is the set of all even numbers
>
> [1] is the set of all odd numbers. 



#### Exam Tricks

People think Castello's exams are really hard because they are super long. 

Her exam rubrics are extremely lenient. It is better to attempt every question just write some garbage and you can get partial credit. 

