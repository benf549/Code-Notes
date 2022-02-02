# Sketching and Indexing For Sequences

Prof. Benjamin Langmead, Spring 2022.

## Reading Notes

### Week 1

#### Compact Data Structures Chapter 1 $\rarr$ 1.5

##### Introduction

Need ways to efficiently store and access huge datasets. We can have fast computation if we keep data in memory and not on disk. Main Techniques:

* Efficient Secondary Memory Algorithms
  * Because random access on disk is slow ($10^5$ times slower), subsequent reads only 100x slower than memory so these try to minimize random reads in favor of sequential ones.
* Streaming Algorithms
  * Only allow around 1 pass over the data while storing intermediate values in memory.
  * Often make approximations of information from the data
* Distributed Algorithms
  * Utilize multiple computers or cores to process large datasets in parallel while minimizing network data transfer (which is 10x slower than reading data from disk). 

**Compression** entails representing data with less space by utilizing tools from information theory to find the minimum theoretical space required to represent information. The data must be decompressed to allow random access so it is best for archival purposes rather than for managing data in memory unless you only need sequential access.

**Compact Data Structures** Maintain data with less space while allowing random access and queries without requiring decompression. Operate on large data in main memory, implementations lie at the intersection of data structures and information theory, data structures are **redundant** in that they can be used to reconstruct the original data and are constructed from it. They speed up information queries while minimizing the space they take up. May take more steps to work than traditional data structures but work on faster memory for a net speed increase. Chapters 1$\rarr$11 are static data structures and chapter 12 covers dynamic data structures.

Resources for some example implementations are this GitHub repo called: [*Succinct Data Structure Library*](https://github.com/simongog/sdsl-lite). There are several other example resources listed in chapter 1.4

##### Mathematics and Notation (1.5)

**Big O Notation** describes the asymptotic growth of functions. $O(f(n))$ is the set of functions $g(n)$ for which constants $c > 0$, $n_0 > 0$ such that for any $n > n_0$ we have that $|g(n)| \le c\times |f(n)|$. 

**Big $\Omega$ notation** is used to describe the lower bound of a function.  $\Omega(f(n))$ is the set of functions $g(n)$ for which constants $c > 0$, $n_0 > 0$ such that for any $n > n_0$ we have that $|g(n)| \ge c\times |f(n)|$. 

$g(n) \in \Theta(f(n))$ indicates that $g(n) \in O(f(n))$ and $g(n) \in \Omega(f(n))$. Meaning that the upper and lower bounds grow asymptotically at the same rate. 

 We use **little o** or $g(n) \in \hat o(f(n))$ notation to describe functions that are asymptotically negligeable compared to $f(n)$. Which formally means:
$$
\underset{n\rarr\infin}{\lim} \frac{g(n)}{f(n)} = 0
$$
So for example a function that uses $2n + \hat o(n)$ bits uses 2n bits plus a number that grows sub-linearly with $n$. $\hat o(1)$ indicates that as n approaches infinity, the contribution of this term tends to zero. 

The opposite of little o is **little omega**  where $g(n) \in \omega(f(n)) \iff f(n) \in \hat o(g(n))$

There are more details here about how to use little o, but I think I need to see the professor or TA work out examples to really get it.

#### Probability and Sets Review

For a random experiment where S consists of all possible outcomes and $s_o \in S$ is an actual outcome we use the following notation:

| **Probability**                | Sets                |
| ------------------------------ | ------------------- |
| Sample Space                   | $S$                 |
| A possible outcome s           | $s\in S$            |
| Event A                        | $A \sube S$         |
| The event A occurs             | $s_0 \in A$         |
| A or B occurs                  | $A \cap B$          |
| A and B occur                  | $A\cup B$           |
| not A occurs (complement)      | $A^c$               |
| A and B are Mutually Exclusive | $A \cap B = \empty$ |
| A implies B                    | $A \sube B$         |
| probability of A               | $P(A)$              |
| A and B are independent		 | $P(A\cap B) = P(A)P(B)$	|

#### Mitzenmacher & Upfal ($1.1 \rarr 1.3, 5.5.1$)

##### Randomized Algorithm Introduction

We can validate if an expression is true by independently evaluating and comparing the two sides. We could check polynomial expansion/monomial multiplication is correct by mutiplying / summing both sides and comparing, but this is essentially doing the same thing two different ways.

We can use randomness to do this a better way. Assume that the maximum degree term of two polynomials $F(x)$ and $G(x)$ is $d$. Choose an integer r uniformly at random between the range $\{1, ... , 100d\}$. Then compute the value of r in both the expansion and condensed formulas. Only if the two are equal are the polynomials equivalent. 

If the random number can be generated in constant time, we can compute the values of $F(r)$ and $G(r)$ in $O(d)$ time (because we need to perform d multiplications and additions?). It is still possible to get the wrong answer though as we have not checked all values of r and it is possible for the two functions to meet at any given r. This would occur if r is a root of the equation $F(x) - G(x) = 0$. There are only d roots of this d-degree equation by the fundamental theorem of algebra, so if we sample the range 1 to 100d, there is a 1/100 chance of returning a wrong answer.

##### Axioms of Probability

Formally, a probability space has 3 components

* a sample space $\Omega$ which is the set of all possible outcomes of a random process modeled by the probability space
* a family of sets $\mathcal{F}$ representing all allowable events where each set in $\mathcal F$ is a subset of the sample space
* a probability function $Pr: \mathcal F \rarr R$
  * Any function where for an event E, $0 \le Pr(E) \le 1$
  * $Pr(\Omega)$ = 1
  * for any finite or infinite sequence of <u>pairwise, mutually disjoint</u> events E1, E2, E3:
    * $Pr(\underset{i\ge 1}\bigcup E_i) = \underset{i \ge 1} \sum Pr(E_i)$
    * In other words, the probability of any of those events happening is the sum of those independent probabilities.

An element of $\Omega$ is an elementary or simple event. The sample space for the above example is the range $\{1, ..., 100d\}$. Each choice of an integer r in this range is a simple event.

We generally consider discrete probability spaces within which the sample space is finite or countably infinite and the family of allowable events consists of all subsets of $\Omega$. The probability function is uniquely defined by the probabilities of simple events. In the earlier example, the sample space had 100d simple events and the sum of probabilities of all simple events must be 1 so each event has a probability of 1/100d.

Events are sets so we can use set theory to describe them and their combinations. We use set subtraction to mean $E_1 - E_2$ is an event that is in $E_1$ but not in $E_2$. This book uses the notation $\bar E$ to denote the complement $\Omega - E$

For any two (non-mutually disjoint events) we have:
$$
Pr(E_1 \cup E_2) = P(E_1) + Pr(E_2) - Pr(E_1 \cap E_2)
$$
which implies that for any finite or infinite sequence of events $E_1, E_2, ... $
$$
Pr(\underset{i\ge 1}\bigcup E_i) \le \underset{i \ge 1} \sum Pr(E_i)
$$
since we have not subtracted out any event intersection probabilities in the sum for those that are not pairwise disjoint.

Review the inclusion-exclusion principle to recall the order of addition and subtraction for calculating probabilities of set unions.

**A randomized algorithm operates under a tradeoff between speed and correctness.** Increasing the sample space of the earlier example of $\{1, ..., 1000d\}$ increases the accuracy to 1/1000 chance of error though we may be limited to the precision of the machine. Another way to improve the answer of the algorithm is to repeat the algorithm multiple times using different, independent random tests. We can use this because the example algorithm is a one-sided error, it is only wrong when it claims equality despite the two not being equal. Any run that gives $F(r) \ne G(r)$ tells us that the two are not equal. They must be equal across all independent runs.

Repeatedly choosing a random number according to a given distribution is referred to as sampling. Sampling with replacement means we don't remember the previous sample. Without replacement means once we have chosen a number in the range, we can't choose that number again. With replacement gives probability of finding a root over k trials is $(1/100)^k$
$$
Two\ events\ are\ independent \iff Pr(E \cap F) = Pr(E)\times Pr(F)
$$
Now, if we consider the case where sampling is done without replacement. In this case, the probability of choosing a given number is **conditioned** on the events of previous iterations.
$$
P(E|F) = \frac{Pr(E\cap F)} {Pr(F)}
$$
which is well defined only if probability of event F is greater than 0. We are looking for thee probability of E and F within the set of events defined by F occurring which restricts the sample space. When E and F are independent the intersection becomes product of probabilities and the probability of E given F becomes just the probability of F.

The probability of a wrong answer from the example algorithm when sampling multiple times without replacement gives:
$$
\prod_{j=1}^k \frac{d - (j - 1)}{100d - (j - 1)} \le (\frac {1}{100})^k
$$
which is better than with replacement but harder to code and analyze.

**Matrix Multiplication Randomized Algorithm Example** To validate if an $n \times n$ matrix C is the product of the same sized matrices A and B is done exhaustively in $\Theta (n^3)$ for the multiplication and comparison. We can improve this with a randomized algorithm by generating a random vector in the vector space of the matrices and multiplying this vector like so:
$$
AB\bar r = C\bar r
$$
Considering only {0,1} as possible values for the matrices and vectors, we find that each of the two options for an index in the vector is picked independently so there are $2^n$ possible vectors. So each value in the vector is equivalent to choosing each r independently and uniformly in {0,1}.

If $D = AB - C \ne 0$ then $AB\bar r = C\bar r$ implies that $D\bar r =0$. There must be a non-zero entry in D.

Continued unraveling reveals the **principle of deferred decisions** when there are several random variables such as a single element of a random vector $\bar r$, it often helps to think of some of them as being set at one point in the algorithm with the rest being random (deferred) until a future point in the analysis.

**Law of Total Probability** states that for E1 .. En mutually disjoint events in the sample space which compose the entire sample space:
$$
Pr(B) = \sum_{i=1}^{n} Pr(B\cap E_i) = \sum_{i=1}^{n} Pr(B|E_i)Pr(E_i)
$$
find that $Pr(AB\bar r = C \bar r) = \frac{1}{2}$
**Bayes' Law**: Assume that $E_1, E_2, ..., E_n$ are mutually disjoint sets such that $\bigcup_{i=1}^{n} E_i = E$
$$
Pr(E_j | B) = \frac{Pr(E_j \cap B)}{Pr(B)} = \frac{Pr(B | E_j)Pr(E_j)}{\sum_{i=1}^n Pr(B|E_i)Pr(E_i)}
$$
starts with a prior model and refines it with new observations to build a posterior model that captures the new information. 

### Week 2

#### M&U Chapter 2 - Discrete Random Variables and Expectation

(Skip Chapter 2.3 and skim 2.5)

##### Random Variables and Expectation

A **Random Variable** X on a sample space $\Omega$ is a real valued function on $\Omega$ which means it maps from Omega to a real number. A **discrete random variable** is a random variable that takes on only a finite or countably infinite number of values. 

Random variables are functions so we use capital letters to denote them while samples or real numbers are lowercase. 

$X = a$ is all basic events in which the random variable X assumes the value $a$ meaning the set: $\{s \in \Omega | X(s) = a\}$ and we define the probability of this/these event(s):
$$
Pr(X = a) = \sum_{s \in \Omega : X(s) = a} Pr(s)
$$
If X is a random variable representing the sum of two dice, then the event $X = 4$ corresponds to the set of basic events $\{(1,3), (2,2), (3,1)\}$ so $Pr(X = 4) = 3/36 = 1/12$
$$
Two\ random\ variables\ are\ independent \iff Pr((X = x) \cap (Y = y)) = Pr(X = x) \times Pr(Y = y)
$$
in other words, the probability of the intersection of independent random variables is the product of the probabilities of the events occurring independently. This extends to any number of random variables. 

**Expectation** is a weighted average of the values a random variable assumes where each value is weighted by the probability the R.V. assumes that value.
$$
E[X] = \sum_i i \times Pr(X = i)
$$
sometimes this series may not converge in which case, the expectation is unbounded.

###### Linearity of Expectation

The expectation of the sum of random variables is equal to the sum of their expectations:
$$
E[\sum_{i=1}^{n} X_i] = \sum_{i=1}^{n}E[X_i]
$$
which holds for any RVs with finite expectations. This holds even for random variables that are not independent. 

We also have the fact that $E[cX] = cE[X]$

###### Jensen's Inequality

A function $f: \mathbb{R} \to \mathbb{R}$ is **convex** if for any $x_1, x_2$ and $0 \le \lambda \le 1$:
$$
f(\lambda x_1 + (1 - \lambda)x_2) \le \lambda f(x_1) + (1 - \lambda) f(x_2)
$$
graphically, this means that if you connect two points on the graph by a straight line, the line will lie on or above the graph of the function. Furthermore, if $f$ has a second derivative:
$$
f\ convex \iff f''(x) \ge 0
$$
Jensen's inequality states that for a convex function f:
$$
E[f(X)] \ge f(E[X])
$$

##### Bernoulli and Binomial Random Variables

Suppose we run an experiment that either succeeds or fails with probability $p$ and fails with probability $1-p$. If $Y$ is a random variable such that it is 1 when the experiment succeeds and 0 when the experiment fails, then Y is a Bernoulli random variable (also known as an indicator random variable).
$$
E[Y] = p\times 1 + (1-p)\times 0= p = Pr(Y=1)
$$
If $X$ represents the number of successes over $n$ samples from $Y$, then $X$ has a **binomial distribution** abbrev. $B(n, p)$:
$$
Pr(X=j) = {n \choose j} p^j (1 - p)^{n-j}
$$
and $E[X] = np$ which can be solved for from the distribution or with linearity of expectation of the sum of $n$ Bernoulli random variables.

##### The Geometric Distribution

Suppose we flip a coin until it lands on heads, what is the distribution of the number of flips required? This is a **geometric distribution** which appears when we perform a sequence of independent trials until the first success where each trial succeeds with a probability p.
$$
Pr(X = n) = (1 - p)^{n - 1} p
$$
for this random variable to equal $n$, there must be $n-1$ failures before the success so you just multiply these probabilities since they're independent. 

These RVs are **memoryless** since the probability that you reach your first success $n$ trials from now is independent of the number of failures that have been experienced so far. Each trial is completely independent of the others. 
$$
E[X] = \frac{1}{p}
$$

###### Coupon Collector's Problem

Suppose that each box of cereal contains one of $n$ different coupons. How many boxes do you need to open to have at least one of each coupon assuming each coupon is in each box independently and uniformly at random from the $n$ possibilities?

Let $X$ be the number of boxes bought until at least one of every type of coupon is obtained. We want to find $E[X]$. Let $X_i$ be the number of boxes bought when you had $i - 1$ different coupons. Then $X = \sum_{i=1}^n X_i$. 

Each $X_i$ is a geometric random variable. When $i-1$ coupons are found, the probability of obtaining a new coupon is:
$$
p_i = 1 - \frac{i - 1}{n}
$$
 so we can write $E[X_i] = 1/p_i = \frac{n}{n-i+1}$

an applying linearity of expectations we have $E[X] = \sum_{i=1}^n E[X_i]$ which gives $\sum_{i=1}^n \frac{n}{n-i+1} = n\sum_{i=1}^n \frac{1}{i}$ somehow....

define the **Harmonic Number**:
$$
H(n) = \sum_{i=1}^n \frac{1}{i}
$$
which we can show has the property: $H(n) = ln(n) + \Theta (1)$ which means $ln(n) \le H(n) \le ln(n) + 1$

and furthermore, WRT the example problem, $E[X] = nln(n) + \Theta(n)$

We can apply this example to the world of computer science by considering the example: suppose there is a chain of routers that all randomly and uniformly add an identification number to an information packet, but only one ID number is added to each packet. The expected number of packets that will arrive before the destination router has "seen" all of the routers in the chain is  $nln(n)+ \Theta(n)$.

#### M&U Chapter 5 - Balls in Bins

One of the most simple random processes is throwing m balls into n bins with each ball landing into a bin independently and uniformly. 

##### The Birthday Paradox

How likely is it that two people in a group of size k share a birthday? To do this you can compute the probability that no two people share a birthday.
$$
\frac{365_{k}} {365^k}
$$
where I'm using falling factorial notation rather than $365_k = {365 \choose k} \times k!$

When k is 30, there is over a 70% chance that two share the same birthday. To generalize:
$$
Pr(all\ different\ birthday) = \prod_{j=1}^{m-1}(1 - \frac{j}{n}) \approx e^{-m^2 /2n}
$$
when there are m people and n possible birthdays. We can approximate with the fact that $1 - \frac{k}{n} \approx e^{-k/n}$ when k is small compared to n.

Furthermore, when there are $2 \lceil \sqrt n \rceil$ people the probability is at most $1/e$ that all birthdays are distinct. I'm not typing out the proof. 

##### Balls In Bins

When we have m balls thrown into n bins independently and uniformly, what does the distribution of the balls look like? We could ask several questions like how many bins are empty, how many balls are in the fullest bin and more. For some  $m = \Omega(\sqrt n)$ at least one of the bins is likely to have more than one ball in it. What is the maximum number of balls in a bin (maximum load)?

When $m = n$, the number of balls equals the number of bins and the average load is 1. The maximum possible load is n, but this is unlikely. What is the upper bound with probability tending to 1 as n grows large?

When n balls are thrown independently and uniformly at random into n random bins, the probability that the maximum load is more than $3ln(n) / ln(ln(n))$ is at most $1/n$ for sufficiently large n.

The probability that any bin receives at least M balls is bounded above by 1/n

##### Bucket Sort

A sorting algorithm that under certain assumptions breaks the $\Omega (n lg n)$ lower bound on comparison based sorting.

Given a set of $n = 2^m$ elements to be sorted and that each element is an integer chosen independently and uniformly at random from the range [0, $2^k$) where $k \ge m$. We can sort the numbers in expected O(n) time with this method. 

Works in two stages, first place elements into n buckets. The jth bucket holds all elements whose first m binary digits correspond to the number j. For example when n = 2^10, the third bucket is all elements whose first 10 binary digits are 0000000011 (which is 3). When j < l, the elements of the jth bucket all come before the elements in the lth bucket in sorted order. If you can place each element into its bucket in O(1) time, you only need O(n) time to execute this stage. If elements to be sorted are chosen uniformly, the number of elements that land in a specific bucket follow a binomial distribution $B(n, 1/n)$.

The second stage of the sort applies a quadratic sort algorithm to order each bucket appropriately. We then concatenate the sorted buckets. The expected time spent on the second stage is at most $cnE[X_1^2]$ where the time to sort the jth bucket is at most $cX_j^2$ for some constant c. As stated above $X_1$ is a binomial random variable so $E[X_1^2] = \frac{n(n-1)}{n^2} + 1= 2 - 1/n \lt 2$ which is at most 2cn and expected time for the whole sort is constant. 

##### Bloom Filters (5.5.3)

A bloom filter is an array of n bits. A[0] to A[n - 1] which is initially all set to 0. We use k independent random hash functions $h_1, h_2, ..., h_k$ which map inputs to a range of $\{0, ..., n-1\}$ 

Assume these hash functions map each element to a random number uniformly over that range. For each element in the input set, the bits $A[h_i(s)]$ are set to 1 for $1 \le i \le k$. We allow bits to be set to 1 multiple times, but only the first flip does anything. To check if an element x is in S, we check whether all array locations $A[h_i(x)]$ for $1 \le i \le k$ are set to 1 or not. If not, then x is not a member of S.  If they are all 1, it is still possible that x is not in the set and thus Bloom filters may return false positives. 

The probability of a false positive for an element not in the set can be calculated easily. Given the hash functions are random, after all elements of S are hashed into the bloom, filter, the probability that a specific bit is still 0 is:
$$
(1 - \frac{1}{n})^{km} \approx e ^ {-km/n}
$$
if we define $p = e^{-km/n}$ and assume that a fraction p of the entries in the Bloom filter are still 0 after all elements of S are hashed and inserted, the <u>probability of a false positive</u> is:
$$
(1 - (1 - \frac{1}{n})^{km})^{k} \approx (1 - e^{-km/n})^k = (1 - p)^k \hat = f
$$
Want to optimize the number of hash functions k in order to minimize the false positive probability f. Using more hash functions gives more chances to find a 0-bit for an element that is not a member of S, but fewer hash functions increases the fraction of 0-bits in the array after inserting the set. 

The derivative of f gives this optimum which we find is $k = ln(2)\times (n/m)$ which corresponds to a false-positive probability of $(1/2)^k \approx (0.6185)^{n/m}$ which falls exponentially with $n/m$ the number of bins used per item. In practice, k must be an integer so the best possible choice of k leads to a slightly higher false positive rate.

Overall, a Bloom Filter is like a hash table, but instead of storing set items we use a single bit to keep track of whether an item was hashed to that location. Essentially tracks whether an item is in a set or not, probably can't recapitulate what elements were inserted (hash-set?).

The assumption that the fraction of bins which are still 0 after inserting S is shown to be a good approximation using content that have not yet covered.
