# Linear Algebra

*Benjamin Fry* - Notes from Bretscher Linear Algebra

### Chapter 1

###### Linear Systems of Equations

One important application of matrix algebra is solving linear systems of equations. The author introduces the following matrix:
$$
\begin{bmatrix}
x + 2y + 3z = 39 \\
x + 3y + 2z = 34 \\ 
3x + 2y + z = 26
\end{bmatrix}
\matrix{\textbf{1.} \\ \textbf{2.} \\ \textbf{3.}}
$$
To solve the matrix we subtract the rows from eachother to isolate the diagonal such that:
$$
\begin{bmatrix}
x = &&&...\\
&y = &&...\\
& & z = &...
\end{bmatrix}
$$
Solution (The Equation eg - 3. Updates as you go):
$$
\begin{bmatrix}
x + 2y + 3z = 39 \\
x + 3y + 2z = 34 \\ 
3x + 2y + z = 26
\end{bmatrix}
\matrix{ & \\ -1\times (1.) \\ - 3 \times (1.)} \\ \\
\Downarrow \\
\begin{bmatrix}
x + 2y + 3z = 39 \\ 
\ \ \ \ \ \  y - z = -5 \\ 
-4y - 8z = -91
\end{bmatrix}
\matrix{ -2 \times (2.) \\ & \\ +4 \times (2.)} \\
\Downarrow \\
\begin{bmatrix}
x + 5z = 49 \\ 
\ \ \ \ \ \  y - z = -5 \\ 
\ \  \ \ \ \ - 12z = -111
\end{bmatrix}
\matrix{ & \\ & \\ \div \ -12} \\
\Downarrow \\
\begin{bmatrix}
x + 5z = 49 \\ 
 \ \ \ \  y - z = -5 \\ 
\ \ z = 9.25
\end{bmatrix}
\matrix{-5\times(3.) \\ +1 \times (3.) \\ &} \\
\Downarrow \\
\begin{bmatrix}
x & & &= 2.75 \\ 
& y & &= -5 \\ 
& & z &= 9.25
\end{bmatrix}
$$
First step above eliminates the x from 2. and 3. using 1, then eliminates y from 1. and 3. using 2, then solves for z in 3. and uses z to eliminate z from 1. and 2.

The numbers substituted back into the original matrix checkout as expected.

Geometrically, this solution is the point of intersection of the three planes defined by the linear system in 3D space. It is the point in space at which all the equations are satisfied. There may be no such point or there may be an infinite number of points (a line) on which the equations are satisfied. 

If a line is the solution, both x and y are determined by z which can be freely chosen so long as x and y are bound by their constraints. 0 = 0 may appear after eliminating the trivial equation suggesting a line.



###### Matrices, Vectors, and Gauss-Jordan Elimination

A matrix is an arrangement of numbers in a rectangular array. A three by four matrix has 3 rows (n) and 4 columns (m). Rows are given then columns. The matrix is indexed as follows:
$$
\begin{bmatrix}
a_{11} & a_{12} & a_{13}\\
a_{21} & a_{22} & a_{23}
\end{bmatrix}
$$
When n == m, the matrix is a square matrix. The square matrix is diagonal if all indices above and below the left-right diagonal are zero (a_i,j = 0 where i != j). It is upper-triangular when the indices above are nonzero but below are and lower-triangular in the opposite case.

When a matrix is only one column or only one row it is a column or row vector respectively. The set of all column vectors with n elements in them is denoted
$$
\R^n
$$
which is considered a *vector space*. Generally only a column vector is referred to as a 'vector' while row vectors are otherwise specified. Typically vectors are represented as
$$
\vec{v} = \begin{bmatrix}x\\y\\z\end{bmatrix}
$$
when in
$$
\R^3
$$
Vectors can be moved around from the origin as long as their direction and magnitude is maintained. In linear algebra the geometric interpretation is ignored. Think about vectors as lists of numbers written in a column.



An easier way of representing polynomial coefficients is by only writing the coefficients and leaving the variables as implied by the rows. For example:
$$
\begin{bmatrix}
2x + 8y + 4z = 2 \\
2x + 5y + z = 5 \\ 
4x + 10y - 1z = 1
\end{bmatrix} \Rightarrow
\begin{bmatrix}
2 & 8 & 4 & 2 \\
2 & 5 & 1 & 5 \\ 
4 & 10 & -1 & 1
\end{bmatrix}
$$
The matrix on the right is known as the ***Augmented Matrix*** as it contains all of the numerical information in the system. If the right-most column is left out the matrix is known as the ***Coefficient Matrix***.

The augmented matrix can be used to solve the linear system. This is less writing than writing in all of the variables. You can divide the rows by scalars and add multiples of rows to other rows as you would in the equation matrix representation solved earlier.

**Matrix Solving Steps**

1. Try to simplify by dividing row by scalar if nicely divisible
2. Multiply 2nd row by some scalar and add to eliminate first column from 2.
   * Then multiply 3rd row and add to remove first column from 3.
3. Repeat step 2 with second row with goal of eliminating the second column in row 1. and 3. 
4. Once one row is solved for (all but one coefficient are zero) add that row times some scalar to other rows to eliminate that column from the other rows.
5. The matrix is solved when the matrix is an identity matrix (all zeroes and ones)

The solution of the matrix can be represented as a vector when solved from terms of x, y, and z.

The solving steps above can be extrapolated to matrices representing greater than 3 coefficients. Use the same algorithm: Start from first equation and gradually eliminate until you can solve for an identity matrix

Linear systems of any number of unknowns are easy to solve if they have three properties:

1. The leading coefficient in each equation is 1
2. The leading variable in each equation does not appear in any other equations
3. The leading variables appear in the natural order with increasing indices as we go down the rows.

If the system follows these properties, we can solve for the leading variables and then use arbitrary variables to represent the infinite solutions.