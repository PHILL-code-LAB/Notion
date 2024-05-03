# Paul C++ Course Week 34

Owner: C.L. Liu
Last edited time: January 16, 2024 8:09 PM

[https://youtu.be/7BdBooTrPkk](https://youtu.be/7BdBooTrPkk)

[Phill-DS-1108.pdf](Paul%20C++%20Course%20Week%2034%20a9dcbaa90577483eb26633d58f866a35/Phill-DS-1108.pdf)

```cpp
#include <iostream>
using namespace std;

struct Node{
  int data; 
  Node* next;
};
class QueueList{
   private:
    Node* front;
    Node* rear;
   public: 
    QueueList(): front(nullptr),rear(nullptr){}
  
   void enqueue(int data){
     Node* newNode = new Node; //產生實體
     newNode->data = data; //存值
     newNode->next = nullptr; //因為不知道要指向誰 所以為nullptr = 接地
     if(rear==nullptr){ //設定好 重置,初始的狀態 
        front = rear = newNode; //queue 裡面只有我一個
        return;
     }
     rear->next = newNode;
     rear=newNode;
   }
   int dequeue(){
    Node* temp = front;
    front=front->next;
    int result= temp->data;
    if(front==nullptr){
      rear = nullptr;
    }
    delete temp;
    return result;
    
   }
   bool isEmpty(){
     return front == nullptr; //真的空了
   }
   
   ~QueueList(){
     while(!isEmpty()) dequeue();
   }
   
  
};  
 
   

int main() 
{
    
  QueueList qu;
  qu.enqueue(94);
  cout << qu.dequeue() <<endl;
  
  qu.enqueue(94);
  qu.enqueue(87);
  cout << qu.dequeue() <<endl;
  cout << qu.dequeue() <<endl;
  
  qu.enqueue(87);
  cout << qu.dequeue() <<endl;
  cout << qu.dequeue() <<endl;
    
    
    
    
    return 0;
}

STDIN
Input for the program ( Optional )

Output:

94
94
87
87
```

```cpp
練習: 
 課服服務 
	一通一通電話進來 -> 一通一通Serve
 addServiceTask()
 pickupSeviceTask()

```

```cpp
繼承
#include <iostream>
using namespace std;

struct Node{
  int data; 
  Node* next;
};
class QueueList{
   private:
    Node* front;
    Node* rear;
   public: 
    QueueList(): front(nullptr),rear(nullptr){}
  
   void enqueue(int data){
     Node* newNode = new Node; //產生實體
     newNode->data = data; //存值
     newNode->next = nullptr; //因為不知道要指向誰 所以為nullptr = 接地
     if(rear==nullptr){ //設定好 重置,初始的狀態 
        front = rear = newNode; //queue 裡面只有我一個
        return;
     }
     rear->next = newNode;
     rear=newNode;
   }
   int dequeue(){
    Node* temp = front;
    front=front->next;
    int result= temp->data;
    if(front==nullptr){
      rear = nullptr;
    }
    delete temp;
    return result;
    
   }
   bool isEmpty(){
     return front == nullptr; //真的空了
   }
   
   ~QueueList(){
     while(!isEmpty()) dequeue();
   }
   
  
};  
 class Customer_Service : public QueueList{
     
     public: 
     void AddServiceTask(int ticket){
       enqueue(ticket);
       cout << "Customer" << ticket << "<--added to service queue" <<endl;
     }
     void pickupServiceTask(){
       if(isEmpty()){
         cout << "No customer!!" <<endl;
       }
   
     int TaskID = abc.dequeue();
        cout << "Customer" << TaskID << "<--is being servered !!" <<endl;
     }  
   };
   

int main() 
{
    
    Customer_Service dell;
    dell.AddServiceTask(101);
    dell.AddServiceTask(102);
    dell.pickupServiceTask();
    dell.pickupServiceTask();
    dell.pickupServiceTask();
    
    
    
    
    
    return 0;
}

Output:

Customer101<--added to service queue
Customer102<--added to service queue
Customer101<--is being servered !!
Customer102<--is being servered !!
No customer!!
```

- 重要
    
    <aside>
    💡 **兩個Class**
    
    兩個Class 的用法 跟先前不同 在private中 加入  QueueList abc;
    
    </aside>
    

```cpp
老師寫法: 

#include <iostream>
using namespace std;

struct Node{
  int data; 
  Node* next;
};
class QueueList{
   private:
    Node* front;
    Node* rear;
   public: 
    QueueList(): front(nullptr),rear(nullptr){}
  
   void enqueue(int data){
     Node* newNode = new Node; //產生實體
     newNode->data = data; //存值
     newNode->next = nullptr; //因為不知道要指向誰 所以為nullptr = 接地
     if(rear==nullptr){ //設定好 重置,初始的狀態 
        front = rear = newNode; //queue 裡面只有我一個
        return;
     }
     rear->next = newNode;
     rear=newNode;
   }
   int dequeue(){
    Node* temp = front;
    front=front->next;
    int result= temp->data;
    if(front==nullptr){
      rear = nullptr;
    }
    delete temp;
    return result;
    
   }
   bool isEmpty(){
     return front == nullptr; //真的空了
   }
   
   ~QueueList(){
     while(!isEmpty()) dequeue();
   }
   
  
};  
 class Customer_Service{
     
     private: 
      QueueList abc;
     public: 
     void  AddServiceTask(int ticket){
       abc.enqueue(ticket);
       cout << "Customer" << ticket << "<--added to service queue" <<endl;
     }
     void pickupServiceTask(){
       if(abc.isEmpty()){
         cout << "No customer!!" <<endl;
       }
   
     int TaskID = abc.dequeue();
        cout << "Customer" << TaskID << "<--is being servered !!" <<endl;
     }  
   };
   

int main() 
{
    
    Customer_Service dell;
    dell.AddServiceTask(101);
    dell.AddServiceTask(102);
    dell.pickupServiceTask();
    dell.pickupServiceTask();
    dell.pickupServiceTask();
    
    
    
    
    
    return 0;
}

Output:

Customer101<--added to service queue
Customer102<--added to service queue
Customer101<--is being servered !!
Customer102<--is being servered !!
No customer!!
```