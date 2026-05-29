### EX7 Implementation of Link Analysis using HITS Algorithm
### DATE: 26-05-26
### AIM: To implement Link Analysis using HITS Algorithm in Python.
### Description:
<div align = "justify">
The HITS (Hyperlink-Induced Topic Search) algorithm is a link analysis algorithm used to rank web pages. It identifies authority and hub pages 
in a network of web pages based on the structure of the links between them.

### Procedure:
1. ***Initialization:***
    <p>    a) Start with an initial set of authority and hub scores for each page.
    <p>    b) Typically, initial scores are set to 1 or some random values.
  
2. ***Construction of the Adjacency Matrix:***
    <p>    a) The web graph is represented as an adjacency matrix where each row and column correspond to a web page, and the matrix elements denote the presence or absence of links between pages.
    <p>    b) If page A has a link to page B, the corresponding element in the adjacency matrix is set to 1; otherwise, it's set to 0.

3. ***Iterative Updates:***
    <p>    a) Update the authority scores based on the hub scores of pages pointing to them and update the hub scores based on the authority scores of pages they point to.
    <p>    b) Calculate authority scores as the sum of hub scores of pages pointing to the given page.
    <p>    c) Calculate hub scores as the sum of authority scores of pages that the given page points to.

4. ***Normalization:***
    <p>    a) Normalize authority and hub scores to prevent them from becoming too large or small.
    <p>    b) Normalize by dividing by their Euclidean norms (L2-norm).

5. ***Convergence Check:***
    <p>    a) Check for convergence by measuring the change in authority and hub scores between iterations.
    <p>    b) If the change falls below a predefined threshold or the maximum number of iterations is reached, the algorithm stops.

6. ***Visualization:***
    <p>    Visualize using bar chart to represent authority and hub scores.

### Program:

```python

import numpy as np

def hits(adj_matrix,iter=100,tol=1.0e-6):
    num=len(adj_matrix)
    ascore=np.ones(num)
    hscore=np.ones(num)
    
    for i in range(iter):
    
        new_ascore=np.dot(adj_matrix.T,hscore)
        new_ascore/=np.sum(new_ascore)

        new_hscore=np.dot(adj_matrix,ascore)
        new_hscore/=np.sum(new_hscore)

        adiff=np.sum(np.abs(new_ascore-ascore))
        hdiff=np.sum(np.abs(new_hscore-hscore))

        if adiff<tol and hdiff<tol:
            print("Iterations stopped at ",i)
            break
            
        ascore=new_ascore
        hscore=new_hscore
        
    return ascore,hscore
    
    
    
    
    
adj_matrix=np.array([[0,1,1,1],[1,0,1,1],[0,0,0,0],[0,0,1,0]])

a,h=hits(adj_matrix)

for i in range(len(a)):
    print("Node",i+1,"Authority Score:",a[i],"Hub Score:",h[i])

```

### Output:

<img width="725" height="118" alt="image" src="https://github.com/user-attachments/assets/534bd6a7-7194-4975-beb2-3318917637e6" />


### Result:

Thus the Implementation of Link Analysis using HITS Algorithm in python was executed successfully.
