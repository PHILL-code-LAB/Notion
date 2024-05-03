# Paul C++ Course Week 49

Owner: C.L. Liu
Last edited time: April 23, 2024 2:44 AM

[https://youtu.be/KAfZX-B1k1k](https://youtu.be/KAfZX-B1k1k)

[Phill-DS-0404.pdf](Paul%20C++%20Course%20Week%2049%206e61d214f4ed424aae3354477ee4f836/Phill-DS-0404.pdf)

[AVL_Tree_練習解析.pdf](Paul%20C++%20Course%20Week%2049%206e61d214f4ed424aae3354477ee4f836/AVL_Tree_%25E7%25B7%25B4%25E7%25BF%2592%25E8%25A7%25A3%25E6%259E%2590.pdf)

[AVL_Tree_練習解析.docx](Paul%20C++%20Course%20Week%2049%206e61d214f4ed424aae3354477ee4f836/AVL_Tree_%25E7%25B7%25B4%25E7%25BF%2592%25E8%25A7%25A3%25E6%259E%2590.docx)

```cpp
#include <iostream>
using namespace std;

class Node{
  public: 
    int  key;
    Node* left;
    Node* right;
    int height;
    
    Node(int k):key(k),left(nullptr),right(nullptr),height(1){}
  
  
};

class AVLTree{
  public: 
    Node* root;
    AVLTree():root(nullptr){}
    
    int height(Node* n){
      if(n==nullptr){
        return 0;
      } 
      return n->height;
    }
      int getBalance(Node* n){
        if(n==nullptr) {
          return 0;
        }
        return height(n->left) - height(n->right);
      }
      
      void updateHeight(Node* n){
        if(n!=nullptr){
        n->height=max(height(n->left),height(n->right))+1; // 父節點的高度  
        }
      }
      Node* rightRotation(Node* y){
        Node* x = y->left;
        Node* T2 = x->right;
        x->right = y;
        y->left = T2;
        updateHeight(y);
        updateHeight(x);
        return x; // 現在 x 為 root ,所以現在 y 被取代 x  
    }
};
int main() 
{
    cout << "Hello, World!";
    return 0;
}
```

============================================================

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
};

int main() 
{
    cout << "Hello, World!";
    return 0;
}
```

![Untitled](Paul%20C++%20Course%20Week%2049%206e61d214f4ed424aae3354477ee4f836/Untitled.png)

![Untitled](Paul%20C++%20Course%20Week%2049%206e61d214f4ed424aae3354477ee4f836/Untitled%201.png)