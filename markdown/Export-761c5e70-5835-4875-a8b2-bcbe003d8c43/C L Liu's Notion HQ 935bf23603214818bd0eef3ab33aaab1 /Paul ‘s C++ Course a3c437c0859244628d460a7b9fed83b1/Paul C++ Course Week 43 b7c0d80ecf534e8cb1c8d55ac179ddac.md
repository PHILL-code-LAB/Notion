# Paul C++ Course Week 43

Owner: C.L. Liu
Last edited time: April 17, 2024 8:44 AM

[https://youtu.be/6m-kmAEX410](https://youtu.be/6m-kmAEX410)

[Phill-DS-0207.pdf](Paul%20C++%20Course%20Week%2043%20b7c0d80ecf534e8cb1c8d55ac179ddac/Phill-DS-0207.pdf)

Remove : 

### **正規的刪除方式**

被刪除的目標節點可能有以下三種情況，分開討論：

- 目標節點為葉節點：直接刪除仍能維持 BST 的結構。
- 目標節點僅有左或右子樹：將僅有子樹往上補位，即可維持 BST 的結構。
- 目標節點同時有左、右子樹：將左子樹最大（或右子樹最小）節點刪除，遞補至目標節點位置。

![Untitled](Paul%20C++%20Course%20Week%2043%20b7c0d80ecf534e8cb1c8d55ac179ddac/Untitled.png)

```cpp
 
// Binary Search Tree 
#include <iostream>
using namespace std;

struct TreeNode{
  int data;
  TreeNode* left;
  TreeNode*  right;
  TreeNode (int value ):data(value),left(nullptr),right(nullptr){}
};

class BinarySearchTree{
  private: 
   TreeNode* root;
   TreeNode* insert(TreeNode* node , int val){ // 複雜版的insert ,
   // private & public 可以用同樣的名字  若傳入的值,型態,輸出不一樣  就會當作不同的method  
     if(node==nullptr){ // 檢查----樹是不是空的 
       return new TreeNode(val);
     }
     if(val < node->data){
       node->left = insert(node->left,val);  
     }else if(val>node->data){
       node->right = insert(node->right,val);
     } 
       return node; // 最後回傳自己
   }
   
   TreeNode* remove_tree(TreeNode* node,int val){
// part 3 
     if(node==nullptr){ // 如果樹是空的 ,return nullptr
        return nullptr;
     }
//part 1 
     if(val<node->data){ // 遞迴
       node->left=remove_tree(node->left,val);
     }
     else(val >node->data){
       node->right=remove_tree(node->right,val);
     }
//part2    else{ // 最後不是以上的條件 , 就只剩下自己了
       if(node->left==nullptr){ //在左子樹空的狀況下
         TreeNode* temp = node->right;
         delete node;
         return temp;
       }else if (node->right==nullptr){
         TreeNode* temp= node->left;
         delete node;
         return temp;
       }
 //part 1       
       TreeNode* temp= minValueNode(node->right); //-> 找右邊最小的,往前遞補 
       node->data = temp->data; //把找到的(minivalueNode)數值導入temp 
       node->right=remove_tree(node->right,temp->data); 
       //刪除(找右邊最小的) 原本的位置的值 -> 用遞迴的方法做 
     }

// part 3 
     return node; // 甚麼都沒找到 只好return 自己
   }
   minValueNode(){
     
   }
  public: // abstract 的精神 
    BinarySearchTree(): root(nullptr){}
   void insert(int value){ //  正式版本 要有search 的功能 不是像之前一樣
     root= insert(root,value); //把root 回傳, 如果root有更動的話 這樣設計比較洽當
   }
   void remove_tree(int value) {
     root=remove_tree(root,value);
　   }
//   ~BinarySearchTree(){
//     destroyTree(root);
//   }
};
int main() 
{
    cout << "Hello, World!";
    return 0;
}

**//Note: 
//若有兩個insert 會依照呼叫不同的參數 去找相對應的insert 
//所有的tree 都是遞迴 因為基本上都依照一個鐵三角下去延伸到另一個鐵三角(trre的架構) 
//BinarySearchTree 中 完全都不會有重複的值
//BST : 左小右大 
//Remove:
// 左小( 在其中挑一個最大的)
// 右大( 在其中挑一個最小的)**
```

![Untitled](Paul%20C++%20Course%20Week%2043%20b7c0d80ecf534e8cb1c8d55ac179ddac/Untitled%201.png)

Note ( TreeNode* remove_tree 的大意) 

以下根據「欲刪除之節點」的child pointer 個數分成三類：

- **Case1.** 沒有child pointer
- **Case2.** 只有一個child pointer
- **Case3.** 有兩個child pointer

### **Case1：沒有child pointer**

只需要考慮原本指向此節點的父點parent，將其 left child/right child 指向NULL即可。

### **Case2：只有一個child pointer**

假如「欲刪除之節點」有一個left child，則需要將其父點 parent 的 left child/right child 重新指向「欲刪除之節點」的 left child。

### **Case3：有兩個child pointer**

須先從「欲刪除之節點」的左子樹中尋找最大值或是右子樹中尋找最小值作為取代點(假設此節點為X)，來取代「欲刪除之節點」的data，再來對於X進行刪除的動作。

- 左子樹(最小值)尋找最大值的方法：不斷地向左移動，直到碰到NULL為止。
- or
- 右子樹(最大值)尋找最小值的方法：不斷地向右移動，直到碰到NULL為止。 ←-minValueNode