# Unit 1 Review

## Discrete Mathematics

*Benjamin Fry*



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



#### Parity 

##### Even

Let x be an integer. x is even if $2|x$.

##### Odd

Let y be an integer. y is odd if $\exists \ b \in \mathbb{Z}$ such that $y = 2b + 1$





#### Prime and Composite

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

> Left for homework: what is a perfect square?



#### Floor and Ceiling

#### Floor

Let $x \in \mathbb{R}$. The floor of x, denoted $\lfloor{x} \rfloor$ is the largest integer n such that $n \le x$. If $n = \lfloor x \rfloor$ then $n \le x \lt n + 1$

##### Ceiling

Let $y \in \mathbb{R}$. The ceiling of y, denoted $\lceil{y} \rceil$ is the largest integer n such that $n \ge y$. If $n = \lceil y \rceil$ then $n -1 \lt y \le n$



### Theorem

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



#### If-Then Statements

