# Paul C++ Course Week 36

Owner: C.L. Liu
Last edited time: January 3, 2024 7:32 PM

[https://youtu.be/_mKvwX49hUM](https://youtu.be/_mKvwX49hUM) 

[Phill-DS-1213.pdf](Paul%20C++%20Course%20Week%2036%201da8e278460f4ccc94eb9761bcb249aa/Phill-DS-1213.pdf)

**Tree 的名詞與概念**

Node 節點 → data field, 資料欄位
Link, **edge**, branch 分支 → 連接兩個節點的線
degree 分支度
某一個node : 多少個 subtrees → 跟多少個 nodes 相連 → $T_1,T_2,.....T_N=N$ 
一棵樹 degree → all nodes 最大 degree
leaf node → degree =0
non-leaf node → degree  $\ne  0$

**hierarchical (等級制度) relationship**

 

- child (children) → children of a node → roots of subtrees → X’s children
- parent → children’s parent → owns your subtree
- sibling (兄弟) → sibling nodes → parent node 相同
- ancestors(列祖列宗(亞當)  → from root ~ X → path 包含的所有的 nodes → ancestors
- level : root level =1, children of root level=2, X level =N → X’s children level =N+1
- level of tree → height, depth → all nodes , maximum leve

![Untitled](Paul%20C++%20Course%20Week%2036%201da8e278460f4ccc94eb9761bcb249aa/Untitled.png)

x = y+z;
Nodes and edges 的計算
每一個 node 都一定有一個 edge → root 例外
任何一棵樹 → Node # Ｎ 跟 edge # Ｂ 有何關係 → N = B + 1

![Untitled](Paul%20C++%20Course%20Week%2036%201da8e278460f4ccc94eb9761bcb249aa/Untitled%201.png)

**二元樹 binary tree**

- level-L 節點個數最多是多少? $2^{L-1}$

![Untitled](Paul%20C++%20Course%20Week%2036%201da8e278460f4ccc94eb9761bcb249aa/Untitled%202.png)

 

- depth K binary tree , nodes # =$2^k-1$ , K≥ 1