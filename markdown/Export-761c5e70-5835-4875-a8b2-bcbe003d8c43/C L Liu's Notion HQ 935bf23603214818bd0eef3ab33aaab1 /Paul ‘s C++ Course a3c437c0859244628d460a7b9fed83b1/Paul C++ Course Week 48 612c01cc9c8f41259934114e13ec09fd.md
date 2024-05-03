# Paul C++ Course Week 48

Owner: C.L. Liu
Last edited time: April 23, 2024 3:30 AM

[https://youtu.be/SSAzq2r8MIA](https://youtu.be/SSAzq2r8MIA)

[Phill-DS-0327.pdf](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Phill-DS-0327.pdf)

BST :  Binary Search Tree的三個重點：有根、兩個children node、左小右大。

AVL Tree  - A V L 

*AVL*樹 是一種Binary search *tree*的實做方式
高度平衡的**二元搜尋樹** → efficiency (不能有空隙,計算量會增加)

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled.png)

child tree 要很 balance

AVL Tree的條件:  

T $\in AVL$

$T_L , T_R$  $\in AVL$

| $h_L - h_R$ |  ≤ 1 —→ balanced 

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled%201.png)

左指數 跟 右指數 相差一個 還可以接受

Blalance factor 平衡因子 BF —> 針對某一個節點的高度計算結果→ BF(n) , n—> node 

|BF(n)| ≤ 1 → -1 , 0 , 1  

練習: 判斷是否Balance 

這個樹 不是 AVL Tree   因為 有 -2  不滿足  -1 , 0 , 1  

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled%202.png)

BF(F) 因為 左右兩邊沒有子樹所以為 0  

BF(D) 左 - 右 =  1 

BF(B) 左 - 右 = -2 

BF(B) 左邊為0  , 右邊的高度是 2 ,所以 左減右 = -2 

## AVL Tree 加入 Node

**LL Type** 

因為是Binary search tree  所以 30 要往左邊加 (符合 binary search tree 的定義 左邊小 右邊大) 

加入 30之後  ,50 為不符合balance 的點  (key point) 

圖1 : LL 型 把 40 往上拉(抓 key point 的左邊)   , 50 (key point)  往下降 (旋轉後) — > **1. 是AVL Tree , 2 . 是 Binary Search Tree** 

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled%203.png)

圖2 :

要加入 35  因為  binary search tree 的定義 左邊小 右邊大 , 所以 35 要往右加

  LL 型 把 (第一個L) 40 往上拉(抓 key point 的左邊 , 50 (key point)  往下降 (旋轉後) , 因為50 成為 40 的右子樹, 

所以原本的 45 要跑到 50 下面, 因為50 的右子樹已經有 60 了,所以 只能成為50 的左子樹. 

     — > **1. 是AVL Tree , 2 . 是 Binary Search Tree** 

Note  50 左邊的深度 是  3  -  右子樹  1  ⇒   BF(50 = 2 

40  左邊深度是 2  -  右子樹 是 1  = BF(40 ) = 1 

---

**RR Type** 

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled%204.png)

- RR Type = Left rotation

LR Type  - 口訣: LR  先找R 點 做L旋轉 再做右旋轉

LR Type → (右邊45 先做 left rotation) → 再整個 right rotation 

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled%205.png)

RL Type  口訣: RL 先找L點 做R右旋轉, 再做 L 左旋轉

RL Type → (左邊 55 先做 right rotation ) ,再整個 left rotation 

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled%206.png)

例子

字串 AVL → BST 原則大小 alphabetical order 大小

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled%207.png)

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled%208.png)