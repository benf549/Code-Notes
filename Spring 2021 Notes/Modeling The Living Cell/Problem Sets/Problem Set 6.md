# Problem Set 6 Written Answers

## Modeling The Living Cell - Spring 2021

### *Benjamin Fry - bfry2*

*04/23/21*

### Problem 1 - Non-Linear Fitting

Completed in MATLAB script. Below is plot for `part c` and  `part d`:

![fig1](C:\Users\benfy\Desktop\Modeling\PS6\fig1.png)

the optimal values of the parameters are summarized as follows

|                             | $V_{max}$     | $K_m$         |
| --------------------------- | ------------- | ------------- |
| Initial Guess               | 6             | 0.5           |
| Optimized Params (± 95% CI) | 3.9910±0.0402 | 0.0899±0.0108 |



### Problem 2 - K-Means Clustering

Below is the plot of the clustered data:

![fiig2](C:\Users\benfy\Desktop\Modeling\PS6\fig2.png)



### Problem 3 - Clustered Markov State Model

I set the `rng(100)`  at the beginning of this section in my script to get reproducible results. 

###### Part A

The matrix of squared pairwise distances for the 7 desired distances at each time point is defined in my code as `sq_dist_mtx`.   

###### Part B

I clustered the data and stored the resulting indices in `idx` and the cluster means in `c`.

###### Part C

The transition matrix is created and named `transitionmtx` in my data. I did this by iterating through each data point in the `sq_dist_mtx` that had a valid vector 50 time-points after it and counting the each transition from i to i+50 in the 6x6 matrix where the rows represent the initial cluster at $t=i$ and the columns represent the cluster at $t=i+50$.

The transitions with the highest probabilities are those that do not change classification. It was most likely that the time point's classification did not change between  $t=i$ and $t=i+50$. The most probable non-self transition at `rng(100)` was the transition from cluster 3 to cluster 6 which had a probability of around 9.55%. Here I present some plots of the first 100 distance vector values identified by `kmeans` for each cluster:

![image-20210423215318579](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210423215318579.png)

as I mentioned above, the transition from cluster 3 to cluster 6 was the most probable non-self transition. In the above plot, we see the order of the data points in the cluster. Clusters 3 and 6 are similar in that they both generally have the dark blue point with the highest value followed by purple with the rest varying but generally, light blue is towards the bottom. The transition from cluster 3 to cluster 1 pictured in the third figure never occurred in my data and thus had a 0% probability of happening in 50 steps. This makes sense as generally we see light blue or red with higher values in cluster 1 than they have in either cluster 3 or 6. When plotting the structure from the original coordinates, this trend wasn't immediately obvious.

Considering cluster 4, this was the smallest cluster by number of data points classified as it and thus must have been relatively distinct from the other states had `29897` data points classified as cluster 4 with 2,649 of those being transitions from cluster 4 to cluster 3 and exactly 0 transitions from cluster 4 to cluster 1 I generated the 3D plot of the structure of the first members of these clusters in figure 6 below (it is easier to see interactively in matlab) but it is clear that this structure from cluster 4 and the structure from cluster 3 plotted below are more similar to eachother than to the structure from cluster 1. Thus, given 50 time steps we would expect to see more transitions between these two than from cluster 4 to cluster 1 which we never saw.

![image-20210423222206509](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210423222206509.png)

###### Part D

The probability of each of the transitions mentioned above is logged to the console as `prob_mtx`

###### Part E

`prob_mtx2` is logged to console and reports the probabilities of each transition for the transition from $t=i$ to $t=i+100$. 

Squaring any of the members of the previous `prob_mtx` gives a pretty close approximation for its corresponding value in `prob_mtx2` and I have provided `expected_prob_mtx_2` for visual comparison of the similarity between the two. The most similar to the predicted values are the highest probabilities in the original `prob_mtx` which makes sense as they will be less susceptible to random error.

Also observe all generated probability matrices have rows that sum to 1.



### Problem 4 - Gradient Descent

The convergence criteria I used was whether the difference in calculated potential energy between steps was less than $10^{-6}$

The energy at the minimum was $-65.445$

Below is the plot of my final configuration:

![fig7](C:\Users\benfy\Desktop\Modeling\PS6\fig7.png)