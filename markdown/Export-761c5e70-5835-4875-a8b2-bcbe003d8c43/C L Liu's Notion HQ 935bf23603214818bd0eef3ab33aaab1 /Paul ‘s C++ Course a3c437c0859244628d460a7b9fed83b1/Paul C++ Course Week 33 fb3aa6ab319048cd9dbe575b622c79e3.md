# Paul C++ Course Week 33

Owner: C.L. Liu
Last edited time: January 3, 2024 7:32 PM

[https://youtu.be/JqZWsiTBZdw](https://youtu.be/JqZWsiTBZdw)

[Phill-DS-1108.pdf](Paul%20C++%20Course%20Week%2033%20fb3aa6ab319048cd9dbe575b622c79e3/Phill-DS-1108.pdf)

![Untitled](Paul%20C++%20Course%20Week%2033%20fb3aa6ab319048cd9dbe575b622c79e3/Untitled.png)

![Untitled](Paul%20C++%20Course%20Week%2033%20fb3aa6ab319048cd9dbe575b622c79e3/Untitled%201.png)

```cpp
Queue 排隊
先進先出 FIFO (First in First out) 
enqueue , deeueue , front , rear (由左到右) 
注意array size 
-1 代表重置 初始化狀態 -> 避免搬動
```

```cpp

#include <iostream>
using namespace std;
#define MAX_SIZE 10

class QueueArray{
  private: 
    int front,rear; // index  
    int arr[MAX_SIZE];
  public:
    QueueArray():front(-1),rear(-1){}
    
    void enqueue(int data){
      if(rear>=MAX_SIZE-1){
     
       
            cout << "已經滿了" <<endl;
            return;
    }
     arr[++rear]=data; // 有 element 的時候
     if(front==-1) front=0; // if front =-1 為新的 element -> for front 連動更新
    }
    int dequeue(){
      if(front ==-1) { //初始或重置後的狀況 -> 空的queue  
         cout << "已經空了喔" <<endl;
         return -9999;
      }
      
      int value = arr[front];
      if(front==rear) { // 為了 maintain front rear  
        front=-1;  //取到最後一個元素 重置 Queue  
                  /// 這種做法的好處是不用搬動 array 
        rear=-1;
      }else{
        front++; //取過值後(變垃圾) front 向後指
      }
      return value;
    }
    
    bool ioempty(){
      (front==-1)?true:false; //利用重置機制 判斷是否為空的 
    }
};

int main() 
{
     
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;
#define MAX_SIZE 10

class QueueArray{
  private: 
    int front,rear; // index  
    int arr[MAX_SIZE];
  public:
    QueueArray():front(-1),rear(-1){}
    
    void enqueue(int data){
      if(rear>=MAX_SIZE-1){
     
       
            cout << "已經滿了" <<endl;
            return;
    }
     arr[++rear]=data; // 有 element 的時候
     if(front==-1) front=0; // if front =-1 為新的 element -> for front 連動更新
    }
    int dequeue(){
      if(front ==-1) { //初始或重置後的狀況 -> 空的queue  
         cout << "已經空了喔" <<endl;
         return -9999;
      }
      
      int value = arr[front];
      if(front==rear) { // 為了 maintain front rear  
        front=-1;  //取到最後一個元素 重置 Queue  
                  /// 這種做法的好處是不用搬動 array 
        rear=-1;
      }else{
        front++; //取過值後(變垃圾) front 向後指
      }
      return value;
    }
    
    bool isempty(){
      (front==-1)?true:false; //利用重置機制 判斷是否為空的 
    }
};

int main() 
{
    QueueArray qu;
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

Output:

94
94
87
87
已經空了喔
-9999
```

Link List 版本 

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
   
};  

int main() 
{
    cout << "Hello, World!";
    return 0;
}

```