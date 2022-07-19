# Network Data Science

Intersession 2022 - Benjamin Pedigo (bpedigo@jhu.edu) 

Course Website - https://bdpedigo.github.io/networks-course

Zoom - [https://JHUBlueJays.zoom.us/j/98136520563?pwd=WStFbVNJbkJSaW00V1pBZ0dsOWtqZz09](https://jhubluejays.zoom.us/j/98136520563?pwd=WStFbVNJbkJSaW00V1pBZ0dsOWtqZz09)

## Week 1

He does work in the neuro-data lab at Hopkins which uses these network models to study brain connectomes (neural wiring). He has worked on developing the python package `graspologic` with Microsoft Research where he did some internships. 

Goals for the course are to give us an introduction to network science, overview of the techniques to further explore the field, to code and analyze a product to add to our portfolio.

We will build familiarity with Python, git/GitHub, and communicating technical content via Jupyter notebooks.

He will be unavailable for the class tomorrow, and there is a short assignment to work on in the meantime. 

**The final project is due Jan 20th and we need to present the project on Jan 21st**. I need to contact him because I'm pretty sure I'll need to miss these days :(

A description of the final project notebook is in the first day (welcome) powerpoint. 

#### Datasets Of Interest

Looked at maggot brain connections which changed as a function of genotype in the maggot brain connections.

Enron anomaly predictions, tracked the network of email communication and identified anomalous behavior which tracked with fraudulent behavior

Organizational communication can be modelled with a network. Modularity measures how isolated into different communities a given network is (higher is more isolated community).

Looked at faculty hiring at other universities as a directed graph, see that <u>a lot</u> of MIT faculty move to work at Carnegie Mellon for computer science and a lot of Stanford and Berkeley move to MIT.  Need ways to rank nodes by edge weights. 

Protein-Protein interaction networks are a common application of these models which is done for diseases where the causative agent is not clear. 

#### Nomenclature

Networks represent **dyadic** relationships (interactions between only two things at once). For example, an email between two people. A **Polyadic** relationship would be an interaction between more than two things. We often can just ignore this and continue using a network. A **Hypergraph** is a mathematical way to represent general polyadic relationships. This comes up in neuroscience since you might throw away information by representing everything as a dyadic relationships.

A **Multigraph** is a node that allows multiple edges between nodes. Graphs must strictly have only one edge between node i and node j. 

#### Representing Networks

A common way to represent a network mathematically is with an **adjacency matrix**. This is an $n \times n$ matrix where if there is an edge between node i and node j, there is a nonzero element at the i, jth element of A. For an **unweighted** network, the connection is 1 and 0 otherwise. For a **weighted** network the non-zero value at that network represents the weight of the edge and there is no edge if the weight associated with that edge is zero.

For an undirected network, we are only interested if there is a relationship between node i and node j and we don't care if there is a directionality. To represent this in an adjacency matrix, if there is an edge from i to j, there is also an edge between j and i. The adjacency matrix is symmetrical. 

For a directed network, node i -> node j does not imply that node j -> node i. Convention is for rows to denote source and column to denote target.

These distinctions are important for selecting the algorithms we can use and are dependent on the data that we have.

```python
import numpy as np
n_nodes = 5
A = np.zeros((n_nodes, n_nodes))

A[0, 1] = 1 #From node 0 to node 1
A[1, 2] = 1 #From node 1 to node 2 ...
A[1, 4] = 1
A[2, 1] = 1
A[2, 3] = 1
A[4, 1] = 1
```

We can check if a network is directed by:

```python
is_Symmetric = (A == A.T).all()
```

or by using graspologic

```python
from graspologic.utils import symmetrize, is_symmetric
print(is_symmetric(A))
A_sym = symmetrize(A) #Force symmetry
```

The symmetrize function averages the edge weights between edges of i->j and j->i if you want to restore the values to 1 or 0, the binarize function will restore the matrix to 1s and 0s.

#### Sparse Networks

Most networks are sparse, meaning they have far more non-edges than edges. There are 100 million twitter accounts and it would be intractable to have a 100mil x 100mil adjacency matrix. 

A sparse matrix is a way to get around the problem when working with sparse networks. This saves memory and can be found in `scipy.sparse` which has several different data structures you can use. Assumes every element in this matrix is zero and just stores information for the non-zero elements. You only need to keep track of which positions are filled and non-zero.

We generally use CSR matrices which are easy to add or multiply, however, adding a new element to the sparse matrix is more difficult. The LIL matrix is slower than the CSR for addition and multiplication, however is better for adding elements to. COO might be n-dimensional?

Sparse matrices are really useful for a lot of different applications

#### NetworkX Graphs

NetworkX is the default way to represent a network in python. 

```python
import networkx as nx
g_undirected = nx.Graph()

g.add_edge(0,1)
g.add_edge(1,2)
g.add_edge(1,4)
g.add_edge(2,1)
g.add_edge(2,3)

[0 1 0 0 0]
[1 0 1 0 1]
[0 1 0 1 0]
[0 1 0 0 0]
```

NetworkX assumes the graph is unweighted and undirected. To create a directed graph, we need to use a different graph called a Di-graph found within `nx.DiGraph()`

In general NetworkX makes a lot of assumptions so you need to be careful and read the documentation to make sure you're doing what you think you are.

```python
nx.to_numpy_array(g, nodelist=[0,1,2,3,4])
```

the `nodelist` lets us assign arbitrary labels for each node. By adding numerical labels, we can dictate the order the nodes get stored rather than the order that the nodes get added. NetworkX does not conserve the ordering that would make sense if you convert it to a numpy array.

For an adjacency matrix, we can change the order of any row or column and the information is the same. 

NetworkX is slow because it is written entirely in python. The main disadvantage is that 

#### Plotting Networks

We can start by plotting a simple network.

```python
import networkx as nx

g = nk.karate_club_graph() #toy network in networkX
```

We can extract the adjacency matrix representation

```python
nodelist = list(g.nodes())

A = nx.to_numpy_array(g, nodelist=nodelist)
A
```

We can then plot the adjacency matrix using a heatmap with seaborn.

```python
import seaborn as sb
sb.heatmap(A)

#Or use graspologic
import graspologic.plot import heatmap
heatmap(A, cbar=False)
```

Recall than any permutation or shuffling of the nodes represents the same data. We can shuffle the data and view the adjacency matrix which is done in the notes. 

If we permute the rows, we also have to permute the columns. The initial ordering of the data is arbitrary. We can 'sort' the adjacency matrix a bit more intelligently using the following code block:

```python
from graspologic.partition import leiden

partition_map = leiden(g, trials=100)
labels = np.vectorize(partition_map.get)(nodelist)
labels
```

When there are too many nodes, you won't have enough pixels to represent each edge as a pixel, the function `adjplot` helps with this. `draw_networkx` is a way to draw the network with ball and stick model. `networkplot` from graspologic helps by coloring each node by its label. Network embeddings can be used to position each node into groups (probably based on PCA).

Edge weights tend to be very large or near zero. It may be interesting to plot the distribution of edge weights. It is common to renormalize the scale of the edge weights. 

#### Centrality Measures

Tell us how important a node is within a network. 

##### Degree

```python
import networkx as nx
import numpy as np
from graspologic.datasets import load_drosophilia_left
from graspologic.utils import binarize

A = load_drosophilia_left()[:28, :28]
A = binarize(A).astype(int)
g = nx.from_numpy_array(A, create_using=nx.DiGraph)
```

Degree is also sometimes called the degree centrality. The number of other nodes to which it is connected. `g.degree()`

```python
degrees = dict(g.degree())
```

Computing degree is also easy with the adjacency matrix where you just sum up the rows and columns of an unweighted graph.

For a directed graph to get the in degree you can sum up the rows and to get the out degree you can sum up the columns. 

```python
A.sum(axis=1) #calculate outdegree of numpy mtx
```

Weighted degree (node strength) would be the num of the edge weights. Usually degree just refers to the number of edges.

##### Eigenvector Centrality

Nodes will be important if they themselves are connected to important nodes. This is a bit circular, but it works. We want a metric for relative importance. For this metric, the score is a vector which is of length n and the scale doesn't really matter since the numbers are only important relative to eachother. The ith element of the vector is the eigenvector centrality of node i. 
$$
x_i = c \sum _j A_{ij} x_j
$$
this is a linear function where c is a constant greater than zero. If we choose c to be $\lambda$ where $\lambda$ is the largest eigenvalue of A.

We can rewrite the sum as the matrix multiplication of A with the column vector x
$$
x_i = \frac{1}{\lambda} A \bar{x}
$$
which if we rewrite using $\lambda x = Ax$ 
$$
x_i = x
$$
For a positive matrix, you have a principle eigenvector which is defined for the largest eigenvalue. 

```python
g = nx.karate_club_graph()
nodelist = list(g.nodes)
A = nx.to_numpy_array(g, nodelist=nodelist)

evalues, evectors = np.linalg.eig(A)
first_evec = np.abs(evectors[:,0]) 
```

So essentially you're describing the importance of the nodes by the span of the vector which best describes the data.

##### PageRank

One of the algorithms used to take a web-network where nodes are websites and links are websites which link to one-another. PageRank is an algorithm which does this. 

Random Walks can improve this algorithm (same as MCMC sampling).

At time t you randomly select a node. Then chose one adjacent node and let x be an n-length vector with all 0s except for a 1 at the position of our random walker at time t+1. Then you calculate the probability of being at node j at time t+1 as P[x = 1] A/d. The probability is therefore 1/d if i is connected to j and 0 otherwise. 

Rather than considering a single random walker at once, we can consider a probability distribution of a random walker where we consider all start positions simultaneously. If D is a nxn matrix where the diagonal is the out degree of each node, we can create a matrix P which represents the transition probabilities where $P = D^{-1}A$ which multiples each row of A by its out degree. 

Then we can just update the probability at time t+1 by that at time t. 
$$
x^{(t+1)} = A^T D x^{(t)} = P^T x^{(t)}
$$
You can still land on a website with no links which would not be able to escape that dead end since it has no out degrees. At each time step with a probability $\alpha$ the random walk proceeds as described, however, with probability $1-\alpha$ the random walker teleports to a completely random node. 
$$
x^{(t+1)} = \alpha A^T D^{-1} x^{(t)} + \frac{(1-\alpha)}{n}
$$
Define the matrix E as the matrix of all ones. $Ex^{(t)}$ where the probability vector is multiplied by E and gives a vector of all ones. 

we can rearrange this as:
$$
x^{(t+1)} = (\alpha P^{T} + \frac{(1-\alpha)}{n} E)x^{(t)} \\
x^{(t+1)} = \hat{P}x^{(t)}
$$
we just leave $\alpha = 0.85$ by convention. 

```python
n = A.shape[0]
alpha = 0.85
n_iters = 100
out_degrees = A.sum(axis = 1)
D_inv = np.diag(1/out_degrees)
rng = np.random.default_rng()
x = rng.random(n)
x /= np.linalg.norm(x, ord=1)
P  = A.T @ D_inv
P_mod = alpha * P + (1 - alpha) / n
for i in range(n_iters):
    x = P_mod @ x
```

This has the effect of finding the prinicple eigenvector of the matrix P_mod through the process of power iteration. Which is an iterative process through which a vector converges to that eigenvector. This is a technique for very quickly calculating just the first and most important eigenvector of a matrix. 

##### Betweenness Centrality

Given the shortest path between node i and node j if you'd like to compute this from a sparse adjacency matrix, use `scipy.sparse.csgraph.shortest_path` in networkx, you can use `shortest_path`

Imagine that we have a network where every pair of nodes needs to exchange information and further assume that each node is equally efficient at transmitting information and that information will flow between pairs of nodes along the shortest path. This metric considers a node more important if more information passes through it.  

The math is on the website idc to type it rn.

##### Comparing Centrality Measures

![image-20220107140144330](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20220107140144330.png)

We can see that degree recapitulates a lot of the information in the more complicated methods. 

Seaborn pairplot will compare each metric to one-another.

#### Random Graph Models

We want ways to create a statistical network model to which we can compare our data sets. These models are a concise mathematical way of formalizing a way that a network is generated (to describe the process that creates it). These allow us to capture a basic structure of the network. Statistical models allow you to prove how well certain algorithms will perform on the data. Allows the comparison of networks. 

```python
import numpy as np
from graspologic.datasets import load_drosophilia_right
from grasologic.plot import heatmap
from graspologic.utils import binarize

adj, labels = load_drosophilia_right(return_labels=True)
adj = binarize(adj)

degrees = adj.sum(axis=0) + adj.sum(axis=1)
sort_inds = np.argsort(-degrees)
adj = adj[sort_inds][:, sort_inds]
labels = labels[sort_inds]

_ = heatmap(
    adj,
    inner_hier_labels=labels,
    title="Drosophila right MB",
    font_scale=1.5,
    sort_nodes=False,
    cbar=False,
)
```

Independent Edge Models

Sometimes called the inhomogeneous erdos renyi model. Under this model, the elements of the network's adjacency matrix A are sampled independently from a Bernoulli distribution.  Every possible edge is just an independent coin flip. 

We don't allow self-loops.

* ER

  * The simplest random graph model has a probability p for the entire network of whether all pairs of nodes have the same prob. of connecting
  * The parameter p is also known as the network density which is related to sparse vs dense networks. 

  ![image-20220110132408115](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20220110132408115.png)

  Every position away from the diagonal has the same P and the edges appear randomly distributed.

* DCER

  * Degree Correlated Erdos Renyi - We add a promiscuity parameter $\theta_i$ for each node i which specifies its expected degree relative to other nodes. $\theta_j$ is the promiscuity parameter for node j. Where $\theta$ is a vector
    * $P_{ij} = \theta_i\theta_j p$
  * If theta is bigger, p can be smaller meaning this model is nonidentifiable and we need to pick a way to limit what p can be so we can actually solve for the parameters. We use the convention that theta must sum to 1. 

  ![image-20220110133146900](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20220110133146900.png) 

* SBM

  * Stochastic Block Model: one of the most famous and useful
  * Allows the modeling of interactions between groups. Let n be the number of nodes in the graph, the vector tau is a length n vector which indicates the block membership of each node in the graph. Let K be the number of blocks then B is a KxK matrix of block connection probabilities. 
  * Needs pre-labelled groups to work properly.

  ![image-20220110133430483](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20220110133430483.png)

  Each block gets its own probability of connection. 

* DCSBM

  * Combines the degree corrected ER and the SBM. You have a matrix of probabilities for labelled edges and degree-correction factors $\theta$

  * $P_{ij} = \theta_i\theta_jB_{ij}$

    ![image-20220110133947326](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20220110133947326.png)

* RDPG

  * Each node has an associated hidden vector referred to as the latent position of that node. for the directed network, each one has a latent position vector for the in and out directions. If xi is the latent position for node i and yj is the latent position for node j then the probability of an edge between i and j is a function of these vectors.

  * $P[A_{ij} = 1] = P_{ij} = f(x_i, y_j)$

    * We restrict the latent positions such that x_i and y_j are between 0 and 1 so P the matrix of all connection probabilities can be written as $XY^{T}$ where $X \in \mathbb{R}^{n \times d}$ 

  * Adjacency spectral embedding allows estimation of the latent vectors similar to hidden markov models.

     ![image-20220110135304132](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20220110135304132.png)

![image-20220110135914697](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20220110135914697.png)

* The BA model is "rich get richer" and uses a time-based evolving process to build a network. Nodes that have more connections are more likely to form new connections. 
* $p_i = \frac{k_i}{\sum_j k_j}$

#### Community Detection

We want to identify groups of nodes that connect more within communities than they do to other residues. 

Networks are the backbones of machine learning. This allows us to form networks from nearest neighbors in high-dimensional data. 

**Modularity** is the degree to which a system's components may be separated and recombined. For our purposes it is the strength of division of a network into modules (groups), clusters, or communities. Networks with high modularity have dense connections to nodes within the modules, but sparse connections between nodes in different modules.

Mathematically, think about undirected unweighted networks with no loops as an $n \times n$ adjacency mtx A. Let k be an n-length vector with the degree of each node. m is the total number of edges.

Let $\delta (\tau_i, \tau_j)$ be an indicator which is 1 if i and j are in the same group and 0 otherwise. The total number of within-community edges is:
$$
\frac{1}{2}\sum_{i,j} A_{i,j} \delta(\tau_i, \tau_j)
$$
we add 1/2 because we don't want to count edges twice. We want to optimize some function of this expression and assume there are groups in our data.

How many edges would we expect to be within sets of nodes under a random model. 

Consider just node i, compute the probability of a particular edge (i,j). Select one edge attached to i (there are 2m-1 remaining edge "stubs" in this network). If the wiring is random, then the probability of connecting to any other edge stub is the same. We want the probability of connecting to node j. The probability of $k_i$ connecting to $k_j$ which is $P_{ij} = \frac {k_ik_j}{2m-1}$, but since m is large, we can usually just use 2m as the denominator.
$$
\frac{1}{2}\sum_{i,j} \frac {k_ik_j}{2m-1} \delta(\tau_i, \tau_j)
$$
sums over the expected probability of the matrix. We can compare by subtraction to the raw matrix by taking:
$$
Q(A,\tau) = \frac{1}{2m}\sum_{i,j}(A_{i,j} - \frac{k_ik_j}{2m})\delta(\tau_i,\tau_j)
$$
which is how we define modularity by edge rather than overall. This is defined over the partition $\tau$, not over the whole network. 

**Naïve Optimization** 

How can we infer $\tau$ from the data. There are $2^n$ possible subsets of the network into 2 groups. Even for a network of only 60 nodes, there are near $10^{18}$ possible subsets.

Given a partition tau, the most naive way to improve the modularity is to randomly pick a node, flip its group and check whether the modularity increases. 

The example in class showed that 1000 iterations of this can improve the modularity.

We can define the matrix B thish we call the **modularity matrix** as:
$$
B_{ij} = A_{ij} - \frac{k_ik_j}{2m}
$$
where our indicator function has a neater expression:
$$
\delta(\tau_i\tau_j) = \frac{1}{2}(\tau_i\tau_j+1)
$$
Now $Q(A,\tau) = \frac{1}{4m}\tau^T B_\tau$

and B is still symmetric. We can do a discrete optimization with 
$$
{max}_{\tau : \tau \in \{-1, 1\}} \tau^T B_\tau
$$
We know that the Euclidean norm of $\tau$ will always be sqrt(n) so we want to maximize in the space of all tau with this norm. 

So we showed that we can compute the principal eigenvector and eigenvalue of B. Then, we can threshold the corresponding eigenvector based on its sign to get our partition. To maximize the dot product between tau and the e.vector x, we can just take 1 for tau if x is greater than 1 and -1 if x is less than or equal to 0.

There are also **Agglomerative Optimization** algorithm which is the state-of-the-art for doing this optimization of large networks. This works by starting with each node in its own group, then check a node and merge groups if this would improve modularity, repeating until you have desired number of groups. The **Leiden** algorithm is the best one for this and this is found in `graspologic.partition`. This algorithm is not deterministic, so you can get a different modularity by calling it multiple times. You can pass in a trials keyword to run the algorithm however many times you want and pick the best modularity. You can't specify the number of communities you want for Leiden.

##### What Modularity Gives You

Finds an assortative or homophilic group of nodes (like-connects-to-like). Conversely, other algorithms might be able to find disassortative groups of nodes. This would mean there is more in common outside groups than within groups. You need other algorithms to find relationships with these because leiden would give you nonsense.

###### Resolution Limit

For certain networks, you can't find small communities even if they exist.

###### Overfitting

Algorithms can find community structure even when they aren't present. 

Running Leiden on a pure ER model, leiden will still find communities.

#### Network Embeddings

Converts a network (or multiple networks) into a vector space representation. Often this is a Euclidean vector space so each vector will represent a single node in the network. 

If you have multiple networks, you might have an embedding where each network is a point in space. Or for one, you might have one where each node is a point in space. 

This embedding can be viewed as fitting the parameters of statistical models (random dot product graph) where each node was represented as a vector (which was hidden). Embeddings can be useful for creating network visualizations. This is how `draw_networkx` works, it creates an embedding though they may not be as sophisticated. 

Embeddings allow us to apply to apply more traditional machine learning techniques since we will have vector representations of each node in the network.

#### Embedding Techniques

###### Word2Vec

This is an unsupervised Natural Language Processing model developed by google. We can train this model on a fake supervised learning task. You create a huge dataset without labels and make a labeled dataset from it by moving a sliding window over each sentence and creating word groups/pairs. The task then is to predict surrounding words from the word in the center.

How does the prediction work, we use a 2-layer neural network. The input vector is a really long one-hot encoding vector (one at word, 0s elsewhere). Our output is a soft-max-ed vector which is also one-hot encoded. The input vector is multiplied by an embedding matrix which essentially just pulls one row from the embedding matrix which gets fed into the hidden layer of the neural network. Which is then multiplied by a context matrix after some non-linearity and is output with soft-max.

###### DeepWalk

How can this technique be translated from words to networks? Our sequence on the network is a ton of random walks on the network. Use n-dimensional vectors if you have n nodes and throw the sequence into Word2Vec.

###### Node2Vec

Modifies the way that random walks are generated. Rather than being a true random walk, bias the walk to travel in the neighborhood they came from based on some user provided parameters. The authors claimed that adjusting these parameters based on application let them find more useful representations for some data sets.

Takes parameters p and q which if they are set to 1, you get exactly the deep walk algorithm.

```python
import networkx as nx
g = nx.read_edgelist( ... )

from graspologic.embed import node2vec_embed
node2vec_embedding, node_labels = node2vec_embed(g, num_walks=16, walk_length=16, inout_hyperparameter=1, return_hyperparameter=1)


```

Will output a 128-dimensional vector which you can apply PCA to, alternatively UMAP is another dimensionality reduction technique you can use. Any dimensionality reduction technique is a lie for visualization purposes only, you shouldn't use it to make conclusions really.

Network embeddings can be used for Recommendation algorithms. Allows us to say what nodes are similar to other nodes simply by looking at the nearest neighbors in k-dimensional space. 

```python
from sklearn.neighbors import NearestNeigbors

nn = NearestNeighbors(n_neighbors=6, metric='euclidean')
nn.fit(node2vec_embedding) #find in 128 dimensional space
```

##### Spectral Embeddings

Similar to the random dot product graph model, we can consider a latent position matrix where P is a probability matrix which is the matrix of Bernoulli R.V.s and we can write $P = XX^T$

We never observed X, but we can estimate it. P is low-rank

For a low rank, we can approximate it with the Singular Value Decomposition. 

###### Singular Value Decomposition (SVD)

Allows us to write a matrix $M = U \Sigma V^T$  where M is an $m \times n$ real matrix with rank r. 

* $U$ is $m \times r$ with orthonormal columns ($U^TU = I, (r\times r)$)
  * Known as the **left singular vectors**
* $V$ is $n\times r$ with orthonormal columns ($V^TV=I, (r\times r)$)
  * Known as the **right singular vectors**
* $\Sigma$ is $r \times r$ and diagonal, with elements on the diagonal in **decreasing order**
  * Known as the **singular values**

If $M$ is square and symmetric, the left and the right singular vectors are the same $M = UDU^T$ which looks like the **eigendecomposition** as M is similar to the diagonal matrix $U$

Under the hood, PCA is just the SVD.

###### Eckart-Young-Mirsky Theorem

If you have a matrix $A$ which is real, square, and full-rank (as many nonzero singular values as dimensions). To approximate the matrix A with a matrix $A_d$ which has rank of at most d.
$$
e = ||A-A_d||_F
$$
The error is the Frobenius norm of the two matrices. This would be if we square every element in the matrix, added them, and took the sqrt. 

The EYM theorem says that the best solution to this problem is the $A_d = U_d\Sigma_dV_d$ where each decomposition matrix has only the first d singular vectors/eigenvalues. Says we keep only the most important parts of the matrix A which gives us the best approximation of A in rank d.

###### Adjacency Spectral Embedding

For an undirected network, just use the truncated SVD approximation of degree d
$$
A_d = U_d \Sigma_d U_d^T
$$
we can absorb the singular values into the vectors themselves
$$
X = U_d\Sigma_d^{1/2}
$$
where we take the element-wise square root of sigma to get
$$
A_d = U\Sigma U^T = U\Sigma^{1/2}\Sigma^{1/2}U^T = U\Sigma^{1/2}(U\Sigma^{1/2})^T = XX^T
$$
which for a directed network, we can do something similar which gives $A = U\Sigma V^T = XY^T$

Which is really similar to the formula for the RDPG which was $P=XY^T$. This is because this is the adjacency spectral embedding, is a consistent estimator for the parameters X and Y in the RDPG setting. If we had an infinitely large network, then our estimated X matrix would converge to the true X matrix.

```python
import numpy as np
from graspologic.datasets import load_drosophilia_right
from graspologic.utils import binarize

A, labels = load_drosophilia_right(return_labels=True)
A_bin = binarize(A)

U, S, Vt = np.linalg.svd(A_bin)
d = 3
sigma_root = np.diag(np.sqrt(S[:d]))

X = U[:, :d] @ sigma_root
Y = Vt.T[:, :d] @ sigma_root
```

reconstruct an estimate of the probability matrix if we wanted to model as an RDPG

```python
import matplotlib.pyplot as plt
from graspologic.plot import heatmap

fig, axs = plt.subplots(1, 2, figsize=(10, 5))

ax = axs[0]
heatmap(
    A_bin,
    ax=ax,
    inner_hier_labels=labels,
    title="Adjacency matrix",
    hier_label_fontsize=15,
)
fig.axes[2].remove()

ax = axs[1]
heatmap(
    X @ Y.T,
    ax=ax,
    inner_hier_labels=labels,
    title="Probability matrix estimate",
    hier_label_fontsize=15,
)

plt.tight_layout()
```

![image-20220113134250547](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20220113134250547.png)

In graspologic this functionality is implemented under the AdjacencySpectralEmbed estimator class. There is some additional math. These tools also work for weighted networks, but you lose the interpretation of the matrix as a probability since the weights change the meaning.

```python
from graspologic.embed import AdjacencySpectalEmbed
ase = AdjacencySpectralEmbed()
X,Y = ase.fit_transform(A) #Only one if not directed
```

We can create a pair plot of the dimensions, we might see that some of the nodes are longer than others. This means that there might be higher edge weights which skew the matrix. 

We can create a histogram of edge weights and see if there are groups with larger edge weights which might skew the representation. 

When doing spectral decompositions, we can do something called **pass to ranks** which transforms the weights from a scale of smallest to largest. 

```python
from graspologic import pass_to_ranks
ase = AdjacencySpectralEmbed()
A_ptr = pass_to_ranks(A)
X, Y = ase.fit_transform(A_ptr)
pairplot(X, labels=labels)
```

This gives us a lot better separation in the pair plot which is better!

###### Laplacian Spectral Embedding (spectral clustering)

There is a parallel way to arrive at the same ideas. Given an undirected network of degree k, Let D be a diagonal matrix with k on its diagonal. The Laplacian can be defined as:
$$
L = D - A
$$
where A is the adjacency matrix. Laplacians give a connection to physical interpretations. 

For a graph with multiple connected components, the eigenvectors of the Laplacian turn out to be an indicator for each of these connected components. 

If you calculate the eigenvectors of the graph, for a graph of multiple connected components, you get indicators of each component. If the network is connected, one eigenvector is all ones or a scaled version of that. 

Clusters in plots of the eigenvector values vs index indicate a connected component.

```python
from graspologic import LaplacianSpectralEmbed
lse = LaplacianSpectralEmbed(n_components=5, form="R-DAD") #R-DAD gives the regularized laplacian
X = lse.fit_transform(pass_to_ranks(A))
```

You might see lines in which the clusters get spread out. These are called eigenspokes which correlate with the degree of the node (longer is higher). 

Why ASE vs LSE? Both are equally good but capture different information. LSE tends to get a representation that is good at separating the left and right hemispheres of the brain. (good at making separations). ASE captured the gray matter vs white matter in the brain (again separations, but a different type).

#### Connected Components

A connected component of an undirected network is a set of nodes where it is possible to get from any node i in that set to any other node j by traversing the nodes of that network. A network is fully connected if there is only one connected component.

Graspologic has tools for dealing with connected components

```python
from graspologic import is_fully_connected
is_fully_connected(G) #works on array or nx graph
```

It is often better to look at each fully connected component separately. 

```python
for component in nx.connected_components(G):
    print(len(component))
```

A weakly connected component is a set of nodes such that it is possible to ge from any node i in the set to any node j in the set but ignores edge directions. A strongly connected component is a set of nodes such that it is possible to get from any node i in the set to any node j in the set. Therefore, we handle these differently for directed graphs. 

If you want to select the largest_connected_component

```python
from graspologic.utils import largest_connected_component
A = sbm([20,10], [0.5, 0], [0, 0.5])
A_lcc = largest_connected_component(A)
A_lcc.shape #-> (20,20)
```

you can also get the indices in the adjacency matrix that correspond to those particular nodes.

#### Graph Matching

Complete exit survey. Graph matching is something you can do when you have more than one network. 

See the graspologic tutorials for more information about graph matching. 

Graph matching comes up in many different contexts: Computer vision comparing objects, communication networks such as matching user contact networks where users have different usernames, neuroscience finding mirrored neurons on different sides of the brain. 

##### Permutations

A specific ordering or arrangement of a number of objects. There are n! permutations of n objects. A permutation matrix is an nxn matrix with all zeros except for n elements which are 1s. Every row will have exactly one 1 and every column will have exactly one 1. Multiplying a vector by this matrix will permute the vector. 

The row index corresponds to the original position and the column index represents the position that the vector will go to.

This also works the same way for matrix-matrix multiplication as it will permute the rows of A. A post-multiplication with $P^T$ would permute the columns in the same way.
$$
PAP^T
$$
would retain the network order since both the rows and columns are permuted. Graph matching is the problem of finding a mapping of the nodes of one graph A and the nodes of another graph B. If B is another matrix we are searching for a similar structure, then we are searching for a permutation of B such that $A = PAP^T$

The graph isomorphism problem is the problem where you have a network and an exact copy we want to verify are the same. For graph matching, we don't necessarily care if the graphs are the same. How can we measure the quality of an alignment between two networks?
$$
e(P) = ||A - PBP^T||_F
$$
we an take the Frobenius norm to quantify the difference between the two matrices. 

##### Solving the Graph Matching Problem

There are a lot of approximate solutions since the absolute correct answer would not be possible in a reasonable amount of time. We can't search over all possible permutations in a reasonable amount of time. 

The convex hull of a permutation matrix is the set of doubly stochastic matrices. A doubly stochastic matrix has all of its rows and columns sum to 1. 

The minimizer of the Frobenius norm that we calculated earlier is given by 
$$
min_P -trace(APB^TP^T)
$$
we can move the problem to continuous doubly stochastic matrices and begin using gradients:
$$
min_D -trace(ADB^TD^T)
$$
we start with a doubly stochastic matrix and compute the gradient of the above expression wrt to D, and get a new step direction. Then compute a step size and update position. Essentially gradient descent applied to matrices. 

##### Graspologic Implementation

Basic Matching

```python
import numpy as np
from graspologic.match import GraphMatch
from graspologic.simulations import er_np

n = 50
p = 0.3

np.random.seed(1)
G1 = er_np(n=n, p=p)
node_suffle_input = np.random.permutation(n)
G2 = G1[np.ix_(node_shuffle_input, node_shuffle_input)]
print("Number of edge disagreements:", np.sum(abs(G1-G2)))
```

```python
gmp = GraphMatch
gmp = gmp.fit(G1, G2)
G2 = g2[np.ix_(gmp.perm_inds_, gmp.perm_inds_)]
print("Number of edge disagreements:", np.sum(abs(G1-G2)))
```

Adding seed nodes: If we know that some of the nodes are already correctly paired, we can use these nodes as seeds. 

The match ratio is the proportion of the number of nodes that are matched correctly. Even a small number of seeds was able to match the graphs perfectly.

You can run these algorithms on graphs with different numbers of nodes too!

###### Practical Considerations

While the number of edges in the two networks matters, the most important thing for performance is the number of nodes. The doubly stochastic matrices are dense $n\times n$ matrices. Over a few thousand nodes will take a really long time. 

The current implementation works only on dense arrays. The result is also dependent on the initialization so you can use the `n_init` parameter to do multiple initializations and take the best.

