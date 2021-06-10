# Problem Set 1 Written Answers

## Modeling The Living Cell - Spring 2021

### *Benjamin Fry - bfry2*

 

### Problem 1:

`randn` is a function in MATLAB that generates pseudorandom numbers sampled from the normal distribution. It can take in 1 integer as in `randn(N)` as its input in which case it will output an $N\times N$ matrix of these numbers. If passed two integers as inputs as in `randn(A, B)` it will output an $A \times B$ matrix of these random numbers where $A$ is the number of rows and $B$ is the number of columns of the output matrix.



### Problem 2:

 The size of the `data_prob2` matrix is $50 \times 2$.

Therefore, there are 50 rows and 2 columns.  



### Problem 3:

The dimensions of the `magic(5)` output is a $5 \times 5$ matrix.

Each row sums to 65.



### Problem 4:

The function takes in two general numeric inputs corresponding to the frequency and damping constant for a damped oscillator. The third input is a positive integer corresponding to the figure number for the generated plot.

When we try to run the script without fixing anything, the error message tells us that matrix `f1` and matrix `f2` are the wrong shape for matrix multiplication.

Because the two matrices are the same shape and we want to multiply them, we can do this by using the elementwise multiplication operator `.*` rather than the normal multiplication operator.



### Problem 5:

 Completed in MATLAB script.



### Problem 6:

 Completed in MATLAB script.



### Problem 7:

The matrix contained in`datapts3.dat` is $1000 \times 1$ (1000 rows by 1 column).

The mean of the data is $0.1911$ 

The standard deviation of the data is $5.7164$

The Standard Error of the Mean (SEM) for the first 10 data points is $1.7001$

The mean of the first 10 data points is $-1.5777$

The rest of the SEMs and Means are in the vectors in the MATLAB script as instructed which are then visualized in the plot.



### Problem 8:

Here is the image I took after loading the VMD script:

![vmdscene](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\vmdscene.bmp)



### Problem 9:

![image-20210202212514569](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210202212514569.png)

![image-20210202212533810](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210202212533810.png)

