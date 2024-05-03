# Paul C++ Course Week 40

Owner: C.L. Liu
Last edited time: February 28, 2024 2:11 AM

[https://youtu.be/246C6oji5FE](https://youtu.be/246C6oji5FE)

[Phill-DS-0117.pdf](Paul%20C++%20Course%20Week%2040%207a6890c682d94b31a9a46ac3f4cbf9e1/Phill-DS-0117.pdf)

Leetcode 104

計算⼀棵⼆元樹的最深深度

- Linked list
- 以下⾯的程式為基礎

```cpp
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
        int leftNum= 1+countNodes(node->llink);
        int rightNum= 1+countNodes(node->rlink);
        int treeNum= max(leftNum,rightNum);
        return treeNum;
          
        }
      }
    public: 
      int MaxDepth(TreeNode *node){
       
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
      
    cout << "max depth:" << tree.MaxDepth(tree.getRoot())<<endl;
    return 0;
}

Output:

max depth:3
```

練習: 

DFS → search based on Depth-First traverse

- 印出 DFS traverse 結果
- DFS_inorder(), DFS_preorder(), DFS_postorder()

```cpp
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
  
    public: 
    
      int  traversal_inorder(TreeNode *node){
        if(node !=NULL){
          
        traversal_inorder(node->llink);
        cout << node->data;
        traversal_inorder(node->rlink);
        
        }
      }
       int  traversal_preorder(TreeNode *node){
        if(node !=NULL){
        cout << node->data;  
        traversal_inorder(node->llink);
        traversal_inorder(node->rlink);
        
        }
      }
      
      int  traversal_postorder(TreeNode *node){
        if(node !=NULL){
         
        traversal_inorder(node->llink);
        traversal_inorder(node->rlink);
        cout << node->data; 
        }
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
    cout << "\n Inorder traversal of binary tree is \n"; 
    tree.traversal_inorder(tree.getRoot());
    cout << "\n preorder traversal of binary tree is \n"; 
    tree.traversal_preorder(tree.getRoot());
    cout << "\n postorder traversal of binary tree is \n"; 
    tree.traversal_postorder(tree.getRoot());
    return 0;
}

Output:

Inorder traversal of binary tree is 
2345678
preorder traversal of binary tree is 
5234678
postorder traversal of binary tree is 
2346785
```