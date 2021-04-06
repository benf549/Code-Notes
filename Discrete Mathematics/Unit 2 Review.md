# Unit 2 Review

Benjamin Fry - 03/04/21



## Chapter 3 - Counting and Relations

### 16- Partitions

An important corollary from the equivalence relations introduced in the previous unit is that the <u>equivalence classes of R are non-empty pairwise disjoint subsets of A whose union is A</u>. 

Because the various equivalence classes divide A, we can say that they are partitions of A. 

###### Partition

Let A be a set, <u>a partition of (or on) A is a set of nonempty, pairwise disjoint sets whose union is A.</u> 

A <u>partition is a set of sets, where each member of the partition is a subset of A and can be called a part</u>. The parts of a partition are always nonempty. The empty set is never a part of a partition. The parts of a partition are pairwise disjoint: no two parts of a partition may share an element and not be identical and thus the same element. The union of the parts is the original set. 

> Let $A = \{1,2,3,4,5,6\}$
>
> $\{ \{1,2\}, \{3\}, \{4,5,6\}\}$ is a valid subset and $\{\{1,2,3,4,5,6\}\}$ and $\{\{1\}, \{2\}, \{3\}, \{4\}, \{5\}, \{6\}\}$ is as well. 

If R is an equivalence relation on A, <u>the equivalence classes of R form a partition of the set A</u>. Given a relation P for which a is related to b if a is in the same partition as b, then P is an equivalence relation. The equivalence classes of the relation are exactly the partitions. 

###### Counting Equivalence Classes / Parts

We relate the problem of number of possible anagram finding to the concept of equivalence classes by considering the anagrams of the word HELLO. We define the relation R on A the set of all anagrams. a R b if a and b give the same arrangement of letters when the repeated letters go from being distinguishable to indistinguishable. 

The number of unique ways to arrange HELLO is therefore, the exact number of equivalence classes that there are. Since each equivalence class has exactly two elements in it, there are 5!/2 possible equivalence classes. 

For the arrangements of AARDVARK, there are now duplicated A's and R's. To count the elements of a hypothetical equivalence class, we simply count the number of possible arrangements of repeated letters for a particular anagram. Picking the original, there is one way to have the non-repeated letter and 3! ways for distinguishable As to be distributed and 2! ways for the distinguishable R's to be distributed. Therefore the equivalence class is of size $3! \times 2!$. Because all of the equivalence classes have the same size, we can divide the total number of arrangements by the size of each equivalence class to get the number of distinguishable anagrams. 

As a general rule, the total number of equivalence classes **when they are all of size $m$** is simply:
$$
\frac {|A|}{m}
$$
though equivalence classes always being the same size is not a given and is problem dependent. 

### Binomial Coeffiecients

Binomial coefficients are the coefficients of a binomial of the form $(x+y)^4$ once expended - ex: $1x^4 + 4x^3y+6x^2y^2 + 4xy^3 + 1y^4$ 

These can be used to find the **number of subsets of size k that an n-element set has**. The notation for this question is given by $n\choose k$.

Thus, the number of 0 element subsets of a n element set is 1 - the empty set. The number of 1 element subsets of an n element sets is exactly n - each element individually. Higher order subsets are harder to count see below.



Furthermore, the number of subsets of size k that can be formed from n element set is equal to the n-k subsets of the n element set. This is because we can think about inclusion in the k subsets as exclusion in the n-k subsets. Thus:
$$
{n\choose k} = {n\choose n-k}
$$
There are zero ways to form subsets with $k > n$.

The binomial formula is given by:
$$
(x + y)^n = \sum_{k=0}^n{n\choose k}x^{n-k}y^k
$$
the connection between binomial coefficients and subset counting is made when we consider that the expansion of the binomial is counting the frequencies of n-element lists of x's and y's. The number of n element lists with exactly k y's and n-k x's is given by the binomial coefficient where we consider the y's being in a given subset and the x's being excluded from the subset. Interchanging the y positions for elements with numerical values changes the question to a list counting problem (see pg 94). 

The coefficients of $(x + y)^n$ also form  the  $n$th row of pascal's triangle. The k's correspond to the diagonals on the triangle. This gives us the relationship that:
$$
{n\choose k} = {n-1 \choose k-1} + {n-1 \choose k}
$$
which is obtained from observing the previous row above in the triangle. If we mark one of the elements, the total number of k possible subsets either includes the marked element or it does not. 

Finally, the book reasons that the general formula for a coefficient is given by:
$$
{n\choose k} = \frac{n!}{k!(n-k)!}
$$
