# Paul C++ Course Week 51

Owner: C.L. Liu
Verification: Verified
Last edited time: May 1, 2024 5:45 AM

[https://youtu.be/zb_p4bLvbrg](https://youtu.be/zb_p4bLvbrg)

[Phill-DS-0424.pdf](Paul%20C++%20Course%20Week%2051%203ad05e383e9140e5904eec5b4fd422ee/Phill-DS-0424.pdf)

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
      }
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
        int balance = getBalance(node); // get BF   確認是否平衡 
        if(balance >=2 && key < node->left->key) { //表示左邊大   --> LL  
             return rightRotation(node);
        }
        if(balance >=2 && key > node->left->key) { // --> LR  
            node->left = leftRotation(node->left);
            return rightRotation(node);
        }
        if(balance <=-2 && key > node->right->key ){ //表示右邊比較大  --> RR
            return leftRotation(node);
        }
        if(balance <=-2 && key < node->right->key ){ //--> RL 
             node->right =rightRotation(node->right);
             return leftRotation(node);
        }
        return node;
    }
    void insert(int key){ // 對外接口  
      root=insert(root,key);
      
    }
    
};

int main() 
{
    AVLTree tree;
    tree.insert(94);
    tree.insert(87);
    tree.insert(945);
    return 0;
}
```

AVL 刪除: 

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
      }
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
        int balance = getBalance(node); // get BF   確認是否平衡 
        if(balance >=2 && key < node->left->key) { //表示左邊大   --> LL  
             
            return rightRotation(node);
        }
        if(balance >=2 && key > node->left->key) { // --> LR  
            node->left = leftRotation(node->left);
            return rightRotation(node);
        }
        if(balance <=-2 && key > node->right->key ){ //表示右邊比較大  --> RR
            return leftRotation(node);
        }
        if(balance <=-2 && key < node->right->key ){ //--> RL 
             node->right =rightRotation(node->right);
             return leftRotation(node);
        }
        return node;
    }
    void insert(int key){ // 對外接口  
      root=insert(root,key);
      
    }
    Node* remove (Node* node,int key){  
  
       //刪除 -> BST 
       if(node==nullptr){
         return node;
       }
       if(key< node -> key){
         node->left = remove(node->left);
       }
       else if(key > node->key){
         node->right = remove(node->right)
       }
       else {
         //(終止條件) -->
         if(node->left== nullptr || node->right ==nullptr){  /// 單子節點 或 無子節點 
          Node* temp = node->left ? node->left: node->right; 
          // temp 會是要保留的節點 或是 空子節點  : 只有三狀況,左邊空 ,全部空 ,右邊空. 
          // 1、是搜尋到要刪除的節點 (遞迴) 
===================================================================
//2、是實際找到、做要刪除的動作 
          if(temp == nullptr){
            tmep = node;
            node =nullptr;//刪除後沒東西了,要塞一個空值
            delete temp;
          }else {
            *node = *temp;  // 保留子節點 ,因為call by pointer 所以要加*號
          }
          else{ //當如果有兩個子節點
            Node* temp = minNode(node->right);  
            **//BST : 左小右大  //如圖
            //Remove: // 左小( 在其中挑一個最大的) || // 右大( 在其中挑一個最小的)**
            node->key = temp->key;  // 把最小值抽上來填入,
            node->right= remove(node->right, tmep->key); 
            //所以 把最小值抽上來填入 等於 右邊那棵樹的最小元素的節點被delete掉了
            // ==> 所以 node->right = xxx 是把delete 掉剩下的子樹接上
          }
       }
    }
    
    void remove (int key ){
      
    }
};

int main() 
{
    AVLTree tree;
    tree.insert(94);
    tree.insert(87);
    tree.insert(945);
    
    
    
    return 0;
}
```

  Ex1.

![Untitled](Paul%20C++%20Course%20Week%2051%203ad05e383e9140e5904eec5b4fd422ee/Untitled.png)

               目前是左子樹 不 balance  (左子樹 BF 通常是大於 0) 所以一直往左邊走 為 LL 型  

![Untitled](Paul%20C++%20Course%20Week%2051%203ad05e383e9140e5904eec5b4fd422ee/Untitled%201.png)

Ex2. 

![Untitled](Paul%20C++%20Course%20Week%2051%203ad05e383e9140e5904eec5b4fd422ee/Untitled%202.png)

![Untitled](Paul%20C++%20Course%20Week%2051%203ad05e383e9140e5904eec5b4fd422ee/Untitled%203.png)

![Untitled](Paul%20C++%20Course%20Week%2051%203ad05e383e9140e5904eec5b4fd422ee/Untitled%204.png)

刪除動作
root → 找 pivot → |BF| >1
Phill-DS-0320 11
pivot BF>0 + pivot →llink BF≥0 → LL
pivot BF>0 + pivot →rlink BF<0 → LR
pivot BF<0 + pivot →rlink BF≥0 → RL
pivot BF<0 + pivot →rlink BF<0 → RR
根據類型再做對應的 rotation

======================================================

  **//BST : 左小右大 
   //Remove:
  // 左小( 在其中挑一個最大的)
      // 右大( 在其中挑一個最小的)**

![Untitled](Paul%20C++%20Course%20Week%2043%20b7c0d80ecf534e8cb1c8d55ac179ddac/Untitled.png)

### **正規的刪除方式**

被刪除的目標節點可能有以下三種情況，分開討論：

- 目標節點為葉節點：直接刪除仍能維持 BST 的結構。
- 目標節點僅有左或右子樹：將僅有子樹往上補位，即可維持 BST 的結構。
- 目標節點同時有左、右子樹：將左子樹最大（或右子樹最小）節點刪除，遞補至目標節點位置。