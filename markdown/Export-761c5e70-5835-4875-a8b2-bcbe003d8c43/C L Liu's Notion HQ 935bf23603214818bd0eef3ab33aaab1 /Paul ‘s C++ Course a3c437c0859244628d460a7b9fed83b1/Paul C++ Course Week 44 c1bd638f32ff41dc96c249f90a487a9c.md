# Paul C++ Course Week 44

Owner: C.L. Liu
Last edited time: February 28, 2024 7:35 AM

[https://youtu.be/gEfD08o-wnM](https://youtu.be/gEfD08o-wnM)

[Phill-DS-0220.pdf](Paul%20C++%20Course%20Week%2044%20c1bd638f32ff41dc96c249f90a487a9c/Phill-DS-0220.pdf)

```cpp
#include <iostream>
using namespace std;
struct TreeNode{
  int data;
  TreeNode* left;
  TreeNode* right;
  TreeNode(int value):data(value),left(nullptr),right(nullptr){}
};

class BinarySearchTreee{
  private: 
    TreeNode* root;
    TreeNode* insert(TreeNode* node,int val){
      if(node==nullptr){
        return new TreeNode(val);
      }
      if(val < node->data){
        node->left=insert(node->left,val);
      }else if(val > node->data){
        node->right=insert(node->right,val);
      }
    }
    TreeNode* remove_tree(TreeNode* node,int val){
      
      
      if(val<node->data){
        node->left=remove_tree(node->left,val);
      }else { 
        if(val > node->data){
        node->right = remove_tree(node->right,val);
        }else {
          if(node->left==nullptr){
            TreeNode* temp = node->right;
            delete node;
            return temp;
          }else if(node->right==nullptr){
            TreeNode* temp=node->left;
            delete node;
            return temp;
          }
           TreeNode* temp = miniValueNode(node->right);
           node->data = temp->data;
           delete node;
           return temp;
        }

      }
        return node;
    }
    
    TreeNode* miniValueNode(TreeNode* node){
    TreeNode* current = node;
    while(current!=nullptr&& current->left!=nullptr){
      current = current->left;
      return current;
    }
  }
  public:
    BinarySearchTreee():root(nullptr){}
    void insert(int value){
      root=insert(root,value);
    }
    void remove_tree(int value){
      root=remove_tree(root, value);
    }
    // ~BinarySearchTreee(){
    //   destoryTree(root);
    // }
};
int main() 
{
    
    BinarySearchTreee bst ; 
    bst.insert(50);
    bst.insert(30);
    bst.insert(20);
    bst.insert(10);
    bst.insert(40);
    bst.insert(80);
    return 0;
}   

//HW 完成 destory 
//	 完成 treavals 
```

Note : miniValueNode 

current → left 

![Untitled](Paul%20C++%20Course%20Week%2044%20c1bd638f32ff41dc96c249f90a487a9c/Untitled.png)

return curent  (當左邊找到底 為nullptr ) ,最後救回傳自己本身

![Untitled](Paul%20C++%20Course%20Week%2044%20c1bd638f32ff41dc96c249f90a487a9c/Untitled%201.png)

Heap 堆 

其實是一顆Tree ,  而且是binary tree , 但不是Binary search tree → 上下有大小的限制, 左右不分大小 

有四種 heap 

Max heap , Mini heap , min-max heap , deap.

應用

heap sort  → efficient  ( nlogn 的複雜度) 

priorty queue 的陽春版

Max Heap 

![Untitled](Paul%20C++%20Course%20Week%2044%20c1bd638f32ff41dc96c249f90a487a9c/Untitled%202.png)

大小

排列方式 保證 最大值永遠在根節點 

Priority Queue

O(nlogn)

Sorting

建立Heap 

    1. 由上到下(調整)

   鐵三角比較 上下比兩次or (左右比) 再往上比

   逐層比較由上往下

   可能會造成層與層之間大小不對的狀況 , 所以 比完之後 還要再向上比才行

![Untitled](Paul%20C++%20Course%20Week%2044%20c1bd638f32ff41dc96c249f90a487a9c/Untitled%203.png)

1. 由下往上

   先把有的值(節點)做編號(array index) ,以號碼大的先開始處理

   鐵三角同層比較,由下往上進行

   比完以後,還要向下再比一次

![Untitled](Paul%20C++%20Course%20Week%2044%20c1bd638f32ff41dc96c249f90a487a9c/Untitled%204.png)

加入元素

要加入的元素 要加在最下方

藉由調整的機制,還原成heap 的原則

Note: 實作上按照編號, 元素先加左腳,再加右腳

![Untitled](Paul%20C++%20Course%20Week%2044%20c1bd638f32ff41dc96c249f90a487a9c/Untitled%205.png)

 刪除元素

刪除節點

要刪除某一個節點 ,先把左邊往上提, 再把右邊往左腳補 (因為要維持先左後右的原則) 

![Untitled](Paul%20C++%20Course%20Week%2044%20c1bd638f32ff41dc96c249f90a487a9c/Untitled%206.png)

[test](Paul%20C++%20Course%20Week%2044%20c1bd638f32ff41dc96c249f90a487a9c/test%20e0257406a72b4b90990c4d9c0329ed9c.md)