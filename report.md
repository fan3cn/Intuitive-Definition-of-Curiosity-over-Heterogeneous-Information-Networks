# Intuitive Definition of Curiosity over Heterogeneous Information Networks

**Yongyong Fan**

[yfanal@ust.hk](yfanal@ust.hk)

Department of Computer Science and Engineering

Hong Kong University of Science and Technology



### ABSTRACT

Heterogeneous Information Network (HIN)[1] is a natural and general representation of data in modern large commercial recommender systems which involve heterogeneous types of data. Many researchers have done a lot of work on this area, e.g. Huan Zhao proposed a Meta-Graph Based method to make recommendations over HIN[2]. However, current recommendation methods over HIN are all similarity-based approaches which means people may get too familiar with the recommended items and thus get bored. In this article, we try to address this over-familiar problem by introducing Curiosity into HIN. We introduce two kinds of curiosity, namely, user curiosity and item curiosity. The main contribution of this paper is that we proposed a new idea of propagating curiosity throughout HIN, which has never been done by anyone before.



## 1  Introduction

We know that the traditional recommendation systems are all based on similarity, which means the recommended items are very easy to similar to the user’s interest as well as between themselves. Thus, the user will quickly find the recommended items too familiar and uninteresting for exploration. Some researchers have done a lot of work to overcome this problem. For example, Discovery-Oriented Recommendation Systems (DORSs) introduce metrics called Discovery Utilities (DUs) as additional dimensions besides relevance for ranking the candidate items[3]. Further on this, Dik Lun introduced a model called Probabilistic Curiosity Model (PCM), which is based on the curiosity arousal theory and Wundt curve in psychology research[4]. However, nobody has ever tried to introduce curiosity or novelty into recommender systems over HIN. In real world, HIN is important, it is a natural and general representation of data in modern large commercial recommender systems. We are living in an interconnected world. Most of data or informational objects, individual agents, groups, or components are interconnected or interact with each other, forming numerous, large, interconnected, and sophisticated networks. We call this network which involves heterogeneous types of data "Heterogeneous Information Network"[1]. Thus, to address the over-familiar problem existed in Recommender System over HIN becomes vital. We try to expand user's taste and discover new interesting items based on user's different degrees of curiosity.



## 2  What is Item Curiosity?

We are all familiar with the concept of curiosity of a person, but how about an item or object? Does a city have Curiosity? What is an item's curiosity? An item‘s curiosity is used to measure how curious an item is to a person, the more curious an item is, the more likely it will attract courious people's attention. Say a cat in blue will probably catch people's eyes, because it's rare to see. We believe that in real world an item has its curiosity which naturally exists just as some other common properties like Beauty, Character or Personality etc. However, item curiosity is very easy to be ignored, because people get used to accept the concept of curiosity of a person rather than an item. 



## 3  Definition of Item Curiosity over HIN?

### 3.1  What is Item Curiosity over HIN?

We first partition all entity nodes over HIN into two catagories: person-like node and item-like node. The curiosity of nodes with different types could be defined as:

- Person-like node curiosity

  It measures how curious a person is. It depends on how many unique and diverse items (s)he is interested in based on his/her access history.[5]

  ​

- Item-like node curiosity

  It measures how attractive an item is to a user with a certain degree of curiosity. We believe that item curiosity could not only be decided by users but also its connectd items, which means an item-like curiosity can now propagate through the whole network. 

### 3.2 How will Item Curiosity propagate?

Intuitively, if an item is frequently accessed by many highly curious users, then it is possibly welcomed by another new curious user.

Simliarly, if an item $A$ is connected with many other highly courious items, we have confidence to believe that there is a high possibility that the curiosity of $A$ should be large. For example, *New York City is more curious to people because it has a lot of interesting things to see compared to a small town few people know.*

After considering two types of nodes together into the computation of curiosity, the item curiosity can now propagate through the whole network. 

### 3.3  Formal Definition

Given two sets of item-like nodes $\{B_1,B_2,…,B_p\}$ and user nodes $\{U_1,U_2,…,U_q\}$ derived from a Heterogeneous Information Network $H$. 

#### 3.3.1 User Curiosity

For a node $U_i$, all its connected item nodes are denoted as: $N_{U_i}=\{B_1,…,B_m\}$. Suppose $B_i$ belongs to category $K_{B_i}$ = $\{k_1,…,k_{r_{B_i}}\}$.  Different categories of items connected to $U_i$ could be computed as:
$$
K_{U_i} = K_{B_1} \cup K_{B_2} \cup ... \cup K_{B_m}
$$
Then we compute User Curiosity with a simple counting-based method:
$$
C_{U_i} = |K_{U_i}|
$$

#### 3.3.2 Item Curiosity

Concretely, for a item-like node $B_i$, all its connected user nodes are denoted as: $U_{B_i}=\{U_1,…,U_n\}$, all its connected item nodes are denoted as:  $B_{B_i} = \{B_1,…B_m\}$. The curiosity of $B_i$ is computed by two parts:

- User contribution

  The user contribution to the curiosity of $B_i$ is decided by the top $k$ curious users connected. Say $U_{B_i}'$ is the set of top $k$ curious users  derived from $U_{B_i}$. Therefore, the curiosity of $B_i$ could be defined as:
  $$
  P_1=\sum_{U \in U_{B_i}'} C_{U}
  $$

- Item contribution

  The item contribution to the curiosity of $B_i$ is computed by the average of connected items curiosity. It is defined as:
  $$
  P_2 = \frac{1}{|B_{B_i}|} \times \sum_{B \in B_{B_i}}C_{B}
  $$
  ​

Therefore, the  curiosity of $B_i$ is defined as:
$$
C_{B_i}=\frac{1}{(T-T_0)}  ( \sum_{U \in U_{B_i}'} C_{U} + \frac{1}{|B_{B_i}|} \times \sum_{B \in B_{B_i}}C_{B} )  + b
$$
where,

 $T$ is the current time, $T_0$ is the time when $B_i$ is created.

$\frac{1}{(T-T_0)}$ is the time shift penalty which indicates the curiosity decreases as time goes by.

$b$ is the global initial value used to incorporate its own base freshness. Say if we want to promote this item on its release, we can set $b$ a relatively large value.

$C_U$ denotes the curiosity of a user $U$.

$C_B$ denotes the curiosity of an item $B$.

$U_{B_i}'$ is the set of top $k$ curious users  derived from $U_{B_i}$.



#### 3.3.3  Why do we need to incorporate item contribution?

Except the "NewYork VS Small Town" example mentioned above, we will explain with another example from the perspecitive of HIN to demonstrate that it is neccessary to consider the interaction between two connected items in terms of calculating their curiosity.

Suppose we have the following HIN instances:

![](cb_2.png)

Say $B_1$ and $B_2$ are item nodes with large value of curiosity as connected with many courious users. However, $B_3$ is an "underdog", only few people know its existance. If we only consider user contribution, $B_3$ will probably be ignored by people due to its small curiosity. However, $B_3$ is connected  by two highly curious items $B_1$ and $B2$, we have strong confidence to believe that $B_3$ is more likely to be curious and thus should not be ignored. Therefore, considering item contribution while computing curiosity makes sense in real world  scenario.



## 4  Apply curiosity

After traversing the whole HIN, we can compute the user curiosity as: 
$$
\vec{C_{U}} = [C_{U_1},…,C_{U_m}]
$$
and item curiosity as:
$$
\vec{C_{B}} = [C_{B_1},…,C_{B_n}]
$$
Based on the two curiosity vector $\vec{C_{U}}$ and $\vec{C_{B}}$ , we then calculate the **User-Item Curiosity Matrix $M_C$** as:
$$
M_C = \vec{C_{U}}^{T}  \times  \vec{C_{B}}
$$
Obviously, $M_C$ is a matrix with dimension of $m \times n$ calculated by the cross product of  vector $\vec{C_{U}}$ and $\vec{C_{B}}$ ,   the $i$th row and $j$th column of $Mc$ means **how much  $i$th user and $j$th item are relevant in terms of curiosity.** More intuitively, it can be used to explain how much $i$ th user is interested in $j$th item. 

Next, for a given similarity-based User-Item matrix $M$, we apply User-Item Curiosity Matrix $M_C$ on it by the Hadamard product(element-wise product):
$$
M' = M \odot M_C
$$
By doing so, we successfully introduce curiosity factor into a traditional similarity-based recommender system to address the over-familiar problem. Because the recommended item is now no longer only based on similarity but also curiosity, that is, for a given user, his/her most interested and revelant items will be more likely to be recommended.



## 5 Conclusion

In this paper, we proposed an novel approach to solve the over-familar problem in recommender systems over HIN. We first introduce user curiosity and item curiosity in Heterogeneous Information Networks (HIN). User curiosity is obtained based on the number of different item categories that a user has accessed,whereas item curioisty reflects the inherent attractiveness of the item to users, which is measured by the number of users accessing the item and the item curiosity of its neighbor items.Next, we construct the User-Item Curiosity Matrix based on the two vectors. Finally, we apply the curiosity matrix into any existing User-Item similarity-based matrix by Hadamard product.



## 6 Future Work

This article only presents a rough idea on how the concept of curiosity is defined intuitively over HIN by which we try to solve the over-familiar problem. However, there is still a lot of work need to be done in order to make the solution complete and convincing. Our future work mainly covers:

- Polish and improve the existing equation.
- Develop a concrete and efficient algorithm to calculate the curiosity across HIN.
- Design and conduct an experiment to verify whether the idea works.

## 7 References:

[1] Y Sun, J Han. Mining Heterogeneous Information Networks: A Structural Analysis Approach. ACM SIGKDD Explorations Newsletter, 2013.

[2] H Zhao, Q Yao, J Li, Y Song, DL Lee. Meta-Graph Based Recommendation Fusion over Heterogeneous Information Networks. KDD '17 ACM SIGKDD, 2017.

[3] S. Vargas. Novelty and diversity enhancement and evaluation in recommender systems and information retrieval. SIGIR’14.

[4] P Zhao, DL Lee. How Much Novelty is Relevant? It Depends on Your Curiosity. ACM SIGIR '16.

[5] Valentina Maccatrozzo, Eveline van Everdingen. Everybody, More or Less, likes Serendipity. UMAP '17.

[6] D Cao, L Nie, X He, X Wei, S Zhu. Embedding Factorization Models for Jointly Recommending Items and User Generated Lists. SIGIR '17.

[7] Y Sun, J Han, X Yan, PS Yu, T Wu. PathSim: Meta Path-Based Top-K Similarity Search in Heterogeneous Information Networks. VLDB 2011.
