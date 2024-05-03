# Paul C++ Course Week 50

Owner: C.L. Liu
Verification: Verified
Last edited time: May 1, 2024 5:45 AM

[https://youtu.be/a0yRUng5Roc](https://youtu.be/a0yRUng5Roc)

[Phill-DS-0417.pdf](Paul%20C++%20Course%20Week%2050%208e5d14a74c074c7b9030c23a9c7a9d8e/Phill-DS-0417.pdf)

```cpp
#include <iostream>
using namespace std;

class Node{
  public:
    int key;
    Node* left;
    Node* right;
    int height;
    
    Node(int k):key(k),left(nullptr),right(nullptr),height(1){}
};

class AVLTree{
  
  public: 
    Node* root;
    AVLTree():root(nullptr){}
    
    int height(Node* n){ // 節點丟進來 算高度
      if(n==nullptr){ // 預防節點是0 的時候  
        return 0;
      }
      return n->height;
    }
    int getBalance(Node* n){ // get BF 的值
      if(n==nullptr){// 預防節點是0 的時候 
        return 0;
      }
    
     return height(n->left)-height(n->right);
    }
    
    void updateHeight(Node* n){  // 做完 Balance 之後 高度都會有變化 ,所以要重新計算高度
      if(n!=nullptr){
        n->height=max(height(n->left),height(n->right))+1; // 父節點的高度  因為父節點 又比子節點高一階 所以 +1 
      } //遞迴
    }
    
    Node* rightRotation(Node* y){
        Node* x = y->left;   // x 為 y的左邊這一點 
        Node* T2 = x->right;
    //======================================= 只是定義位置 還沒有開始旋轉 
        x->right = y;
        y->left = T2;
        updateHeight(y); // update y   因為只有 y 點 被動到
        updateHeight(x);  // update x 的高度   因為只有x 點被動到
        return x; // 現在 x 為 root ,所以現在 y 被取代 x  
    }
    
    Node* leftRotation(Node* x){
      Node* y = x->right;
      Node* T2 = y->left;
    //========================================= 承上反之    
       y->left = x;
       x->right = T2;
       updateHeight(x);
       updateHeight(y);
       return y; 
    
    }
    Node* insert(Node* node , int key ){ //內部處理的insert    
        //BST --> Step 1 符合BST的規則   
        if(node == nullptr){
          return new Node(key); // 樹為空 或在末梢  產生節點實體   
        }
        if(key < node->key){
            node->left=insert(node->left,key);  // 利用迪回邏輯 不停地去比 ,並設置終止條件            
        }else if (key > node->key){
          node->right = insert(node->right,key);
        }else {
          return node;  // 如果相同的時候 只給他 (回傳自己) 
        }
        updateHeight(node);
       ** int balance = getBalance(node); // get BF   確認是否平衡 
        if(balance >=2 && key < node->left->key) { //表示左邊大   --> LL  
          
        }
        if(balance >=2 && key > node->left->key) { // --> LR  
          
        }
        if(balance <=-2 && key > node->right->key ){ //表示右邊比較大  --> RR
          
        }
        if(balance <=-2 && key < node->right->key ){ --> RL 
          
        }**
    }
    void insert(int key){ // 對外接口  
      root=insert(root,key);
      
    }
    
};

int main() 
{
    cout << "Hello, World!";
    return 0;
}
```

    **if(balance >=2 && key < node->left->key) { //表示左邊大   --> LL  
          
        }**

Note: key 為加進去的值  

![Untitled](Paul%20C++%20Course%20Week%2050%208e5d14a74c074c7b9030c23a9c7a9d8e/Untitled.png)

![Untitled](Paul%20C++%20Course%20Week%2050%208e5d14a74c074c7b9030c23a9c7a9d8e/Untitled%201.png)

 **if(balance >=2 && key > node->left->key) { // --> LR  
        }**

![Untitled](Paul%20C++%20Course%20Week%2050%208e5d14a74c074c7b9030c23a9c7a9d8e/Untitled%202.png)

 **if(balance <=-2 && key > node->right->key ){ //表示右邊比較大  --> RR
        }**

![Untitled](Paul%20C++%20Course%20Week%2050%208e5d14a74c074c7b9030c23a9c7a9d8e/Untitled%203.png)

        **if(balance <=-2 && key < node->right->key ){ --> RL 
        }**

![Untitled](Paul%20C++%20Course%20Week%2050%208e5d14a74c074c7b9030c23a9c7a9d8e/Untitled%204.png)

 [https://www.tldraw.com/](https://www.tldraw.com/)

**//Note: 
//若有兩個insert 會依照呼叫不同的參數 去找相對應的insert 
//所有的tree 都是遞迴 因為基本上都依照一個鐵三角下去延伸到另一個鐵三角(trre的架構) 
//BinarySearchTree 中 完全都不會有重複的值
//BST : 左小右大 
//Remove:
// 左小( 在其中挑一個最大的)
// 右大( 在其中挑一個最小的)記概念 而不去去被做法被做法**

- [ ]  要記概念 而不去去被做法

![Untitled](Paul%20C++%20Course%20Week%2049%206e61d214f4ed424aae3354477ee4f836/Untitled.png)

![Untitled](Paul%20C++%20Course%20Week%2049%206e61d214f4ed424aae3354477ee4f836/Untitled%201.png)

![Untitled](Paul%20C++%20Course%20Week%2048%20612c01cc9c8f41259934114e13ec09fd/Untitled%204.png)