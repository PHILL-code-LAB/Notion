# Paul C++ Course Week 41

Owner: C.L. Liu
Last edited time: January 26, 2024 3:44 AM

[https://youtu.be/cEd8h8M6hQs](https://youtu.be/cEd8h8M6hQs) 

[Phill-DS-0124.pdf](Paul%20C++%20Course%20Week%2041%2061ed924cba96491aaf8a1e78e077b350/Phill-DS-0124.pdf)

# BFS (Breath-First Search)

BFS:空間換取時間 

DFS:時間換取空間

traverse 方式

本質上是Queue的問題

TreeNode → Node

QueueNode →根據綠線來連結 

Queue 的框架 

![Untitled](Paul%20C++%20Course%20Week%2041%2061ed924cba96491aaf8a1e78e077b350/Untitled.png)

Queue: 

![Untitled](Paul%20C++%20Course%20Week%2041%2061ed924cba96491aaf8a1e78e077b350/Untitled%201.png)

Note: 把Tree 放在一個Queue 的結構裡

```cpp
#include <iostream>
using namespace std;

struct TreeNode{
  int data;
  TreeNode *llink;
  TreeNode *rlink;
  TreeNode(int value):data(value),llink(nullptr),rlink(nullptr){}
  
};

struct QueueNode{ //只指向資料不自帶資料  不會寫 int data , 因為redundant(多餘的) 重複帶資料
   TreeNode* treeNode;
   QueueNode* next; //recursive的方式 指向下一個
   QueueNode(TreeNode* node): treeNode(node),next(nullptr){}  //初始化 
  
};

class Queue{
  private: 
    QueueNode* front;
    QueueNode* rear;
  public:
    Queue(): front(nullptr) , rear(nullptr){}  // 初始化 
    
    ~Queue(){//distruct
      while(front!=nullptr){  
      QueueNode* temp = front; // 魁儡變數  -?準備被release  
      front =  front->next;  //指向下一個
      delete temp;
      }
    }  
   void enqueue(TreeNode* node){
     QueueNode* newNode = new QueueNode(node);
     if(rear==nullptr ){
       front=rear=newNode;
        return;
     }
     rear->next = newNode;
     rear=newNode;
   }
   TreeNode* dequeue(){
      if(front==nullptr){
      return nullptr;
    }
    QueueNode* temp = front;
    front= front->next;
    if(front==nullptr){ //當被拿光的時候 ,需要回復原狀
     rear = nullptr;
    }
    TreeNode* result =  temp->treeNode; ///拆包裝紙 把牛肉拿出來
    delete  temp; 
    return result;
    
    }
};

int main() 
{
    cout << "Hello, World!";
    return 0;
}
```