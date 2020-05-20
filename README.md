## DECISION TREE

A decision tree is a non parametric supervised Machine learning algorithm that is used for both classification and regression problems. It is mostly used for classification tasks. The goal is to build a model to predict the value of the target label  by using simple decision rules inferred from data.

<img src="https://imgur.com/IccCCME.png" title="source: decision tree"/>

## IMPORTANT TERMINOLOGIES :

**ROOT NODE :** Root node is where the population data is present before any split. It represents the entire population or sample which further gets divided into sub-nodes.The orange color node at the top of the tree represents the root node.

**Decision Nodes :** When a sub-node gets divided further into different sub-nodes it is known as decision node. The nodes in red color represent the decision nodes as they are further getting divided into different sub-nodes.

**Leaf / Terminal Node :** The node which does not get divided further is known as leaf / terminal node. The nodes in green color represents the terminal nodes.

**Depth :** The depth of the tree is the longest path from the root node to the leaf of the tree. The depth of the tree is 3 here as we have to take 3 steps to reach from the root node to the last terminal / leaf node.

**Splitting :** The process of dividing a node further into sub-nodes is known as splitting.

**Pruning :** It is the opposite of splitting. When a decision tree is fully grown we remove the sub-nodes from the decision node and this process is known as pruning.

---



## ADVANTAGES OF DECISION TREE :
* Decision trees are simple to interpret and visualize.
* Requires less effort for data preparation compared to other algorithms.
* Useful in data exploration. Decision trees are one of the fastest ways to identify the most significant variables.
* A decision tree can handle both categorical and numerical variables.
* A decision tree can handle missing values. 

## DISADVANTAGES OF DECISION TREE :
* Decision trees are very prone to overfitting.
* A small change in data can cause a large change in the structure of the decision tree.
* Decision trees are relatively expensive as complexity and time taken is more.

## DECIDING BEST SPLIT :

A decision tree uses multiple algorithms to decide to split a node into different sub-nodes. The sub-nodes are more homogeneous than the previous nodes with respect to the target variable. As we go on splitting the nodes the purity of the nodes increases.

A decision tree splits the nodes on all the available variables and selects the one which results in most homogeneous sub-nodes. The process is repeated until a full grown tree is formed.

The algorithm selection for split is dependent on the type of target variable. Here we will only look into the categorical target variables and different algorithms that are there to decide the split.

---

## GINI IMPURITY

                            Gini Impurity = 1- Gini
                            Gini = p^2 + q^2

The goal of learning algorithms in decision tree is always to find the best split for each node of the tree.

Gini Impurity measures the disorder of a set of elements. To understand it better consider a example. Suppose we have data about students in a class and we want to find out who is most likely to pass or fail.

Suppose we have information about students whether they attend tution or not and they participate in co-curricular activities or not as two features and we want to predict if the students is going to fail or pass based on these 2 features. 

      | FEATURES |
      --- | 
      | ATTEND TUTION |
      | CO-CURRICULAR ACTIVITIES | 


| TOTAL STUDENTS | 20|
--- | ---|
| PASS | 12 |
| FAIL | 8 |

First we will calculate the gini impurity for both the split and select the one with less impurity.

**Let's first consider the split on tution**

<img src = 'https://imgur.com/lDkDTsu.png'>

We have total 20 students in root node. Where star represents failed students and the spehere represents passed students.

We will represent Probability of pass by p and probability of fail with q

Out of 20, 12 of them pass and 8 fail. So at root node we have  p = 20/12 which equals 0.6 and q = 8/20 which equals 0.4

If we calculate Gini at root node we will have p^2 + q^2 = 0.6^2 + 0.4^2 which equals  0.52.

*Impurity = 1 - Gini*

Impurity = 1 - 0.52 = 0.48

                      So at the root node we have impurity = 0.48. 
We have split the node based on tution, where tution = 1 represent students attend tutuions and tution = 0 represents students didn't attend tutuion.

**After the split we have 12 values in left node and 8 values in right node**

    For the left sub-node. Tution = 1, we have total 12 students. Out of those 12, 9 pass and 3 fail.
    
                    p = 9/12 which equals  0.75 
                    q = 3/12 which equals 0.25
                    p^2 + q^2 = 0.75^2 + 0.25^2 = 0.625

                    Gini Impurity = 1 - Gini
                                  = 1 - 0.625 = 0.37
          
    For the right sub-node. Tution = 0, we have total 8 students. 3 Pass and 9 Fail
    
                    p = 3/9 which equals  0.38 
                    q = 5/9 which equals 0.62
                    p^2 + q^2 = 0.38^2 + 0.62^2 = 0.53

                    Gini Impurity = 1 - Gini
                                  = 1 - 0.53 = 0.47
           
     Now we will calculate the weighted impurity for the split on tution.

    Weighted Node impurity = ( (Total number of values in left child node / Total values in parent node) *  Gini Impurity of left node) +
                            ( (Total number of values in right child node / Total values in parent node) *  Gini Impurity of right node )

                            Weighted Impurity = 12/20 (0.37) + 9/20 (0.47) = 0.41
                          

In parent node the gini impurity was 0.48 and now after the split the gini impurity is 0.41. That means we have more homogeneous group and split was significant.

**Similarly We will calculate the split on Co-curricular activities** 

We will leave the calculation part for you. calculate the weighted impurity for the split on the co-curricular activities. For simplicity round off the values.

Here's what you will get after all the calculations.

<img src = "https://imgur.com/5jk0AyN.png" height="350" width = "800" align="center">

---




    We can see that the gini impurity is less when the split is done on Tutions so we select tution as our 1st split. 
    
We will again repeat the same steps and select the feature with less impurity for further splitting.
