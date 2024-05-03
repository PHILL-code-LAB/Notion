# Paul C++ Course Week 39

Owner: C.L. Liu
Last edited time: February 23, 2024 9:02 AM

[https://youtu.be/3NPmpUVd9KA](https://youtu.be/3NPmpUVd9KA)

[Phill-DS-1213, 1220, 0103, 0110.pdf](Paul%20C++%20Course%20Week%2039%200f713cb146954c9e8ee6c78be64e7d9f/Phill-DS-1213_1220_0103_0110.pdf)

```cpp
//Note : 建構Linklisted Binary Tree 第一階段  
#include <iostream>
using namespace std;

struct TreeNode{
  int data;
  TreeNode* llink;
  TreeNode* rlink;
  TreeNode(int value):data(value), llink(NULL),rlink(NULL){}
};

class  BinaryTree{
  private: 
    TreeNode* root;
  public:
    BinaryTree(): root(NULL){}
    void insert (int data){
      if(root==NULL){
        root=new TreeNode(data)
        return;
      }
    }
};

int main() 
{
    cout << "Hello, World!";
    return 0;
}
```

Note: 

![Untitled](Paul%20C++%20Course%20Week%2039%200f713cb146954c9e8ee6c78be64e7d9f/Untitled.png)

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
     ~BinarySearchTreee(){
       destoryTree(root);
     }
      void destoryTree(TreeNode *node){
        if(node != NULL){ // 不要free掉空tree <--需要檢查是不是空的樹) 
          destoryTree(node->left); //先free 左
          destoryTree(node->right); //再free 右
          delete node;      //再 free 自己 
        }
      }
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
```

練習 

用上面的class 

計算binary Tree 有多少個nodes? →

 method : 

private → countNodes() 

public → totalNodes()

return 一個值 給我們

```cpp
//自己版本
#include <iostream>
using namespace std;

struct TreeNode{
  int data;
  TreeNode* llink; //左指數 link list 
  TreeNode* rlink; //右指數 link list 
  
  TreeNode(int value): data(value), llink(NULL) , rlink(NULL){}
};

class BinaryTree{
  private: 
    TreeNode* root;
    
  public:
    BinaryTree():root(NULL){}
    
    void insert(int data){
      if(root ==NULL){ // 樹 是空的
        root = new TreeNode(data);
        return;
      } 
      TreeNode* temp = root;    // Travse 的魁儡變數
      while (true){
        if(data < temp->data ){ //插入的值 比魁儡變數值小 -> 則向左走  
          if(temp->llink == NULL){ //如果左邊是空的
            temp->llink = new TreeNode(data); // 直接assign 成左 node  
            return;
          }
          temp = temp-> llink; //推移左魁儡變數到下一層 
        }else {
          if(temp->rlink == NULL){ //如果右邊是空的  
            temp->rlink=new TreeNode(data);
            return;
          }
          temp=temp->rlink; //推移右魁儡變數到下一層  
        }
      }
    }
    TreeNode *getRoot(){ //get 到root 的實體  -> getter 
      return root;
    }
    ~BinaryTree(){
      destoryTree(root);
    }
    private:  // 用travse 的方式(delete) 結束掉  
      void destoryTree(TreeNode *node){
        if(node != NULL){ // 不要 free 掉 空 tree 
          destoryTree(node->llink);
          destoryTree(node->rlink);
          delete node;      
        }
      }
  
    private: 
      int  countNodes(TreeNode *node){
        if(node !=NULL){
        int leftNum=countNodes(node->llink);
        int rightNum=countNodes(node->rlink);
        int treeNum= leftNum+rightNum+1;
        return treeNum;
          
        }
      }
    public: 
      int totalNode(TreeNode *node){
        return countNodes(node);
        }
};

int main() 
{
    BinaryTree tree;
    tree.insert(5);
    tree.insert(3);
    tree.insert(7);
    tree.insert(2);
    tree.insert(4);
    tree.insert(6);
    tree.insert(8);
    return 0;
}
```