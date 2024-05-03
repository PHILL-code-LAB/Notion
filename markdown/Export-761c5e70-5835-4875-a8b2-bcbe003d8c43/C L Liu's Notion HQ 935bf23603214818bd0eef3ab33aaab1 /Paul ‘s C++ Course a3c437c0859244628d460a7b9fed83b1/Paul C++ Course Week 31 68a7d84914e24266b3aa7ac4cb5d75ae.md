# Paul C++ Course Week 31

Owner: C.L. Liu
Last edited time: January 3, 2024 7:32 PM

[https://youtu.be/7i-OCMs7AaU](https://youtu.be/7i-OCMs7AaU)

[Phill-DS-1018.pdf](Paul%20C++%20Course%20Week%2031%2068a7d84914e24266b3aa7ac4cb5d75ae/Phill-DS-1018.pdf)

```cpp
**Stack Linked List version**
	不受 maximum size 的限制 
```

![Untitled](Paul%20C++%20Course%20Week%2031%2068a7d84914e24266b3aa7ac4cb5d75ae/Untitled.png)

![Untitled](Paul%20C++%20Course%20Week%2031%2068a7d84914e24266b3aa7ac4cb5d75ae/Untitled%201.png)

  往左長  

 newNode->next =  top; //新增的節點在左邊 (往左長比較有效率) )
  top = newNode; //指向最後加入的新節點 

```cpp

#include <iostream>
using namespace std;

struct Node{
  
 int data;
 Node* next;
  
};

class StackList{
  private: 
    Node* top;
  public: 
    StackList():top(nullptr){}
    
    void push(int data){
      Node* newNode= new Node;
      newNode->data = data;
      newNode->next =  top; //新增的節點在左邊 (往左長比較有效率) )
      top = newNode; //指向最後加入的新節點 
    }
    
    int pop(){  // LIFO (Last in First out ) 後進 先出 
      if(top == nullptr){ //沒東西可以pop  // Step 6 
        cout << "stack underflow"<<endl;  //Step 7
        return -9999;   //Step 8 
      }
      Node* current = top; //暫存要刪掉的節點 // Step 1 
      top = top ->next; //把top 的位置先調到下一個  //Step 2 
      int value = current->data ; // 先存return 值  //Step 3 
      delete current;  //Step 4 
      return value;  // Step 5 
      
    }
};

int main() 
{
    cout << "Hello, World!";
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

struct Node{
  
 int data;
 Node* next;
  
};

class StackList{
  private: 
    Node* top;
  public: 
    StackList():top(nullptr){}
    
    void push(int data){
      Node* newNode= new Node;
      newNode->data = data;
      newNode->next =  top; //新增的節點在左邊 (往左長比較有效率) )
      top = newNode; //指向最後加入的新節點 
    }
    
    int pop(){
      if(top == nullptr){ //沒東西可以pop 
        cout << "stack underflow"<<endl;
        return -9999;  //cout << "UnderFlow" <<endl;
      }
      Node* current = top; //暫存要刪掉的節點
      top = top ->next; //把top 的位置先調到下一個
      int value = current->data ; // 先存return 值
      delete current;
      return value;
      
    }
    
    bool isEmpty(){
      return (top==nullptr);
    }
    
    ~StackList(){ //回收記憶體    **(前面幾個章節 都要做這個)** 
      while (!isEmpty()){
        pop(); // 會照 traverse 方式 free      
      }
    }
};

int main() 
{
    cout << "Hello, World!";
    return 0;
}
```

```cpp
練習題 
用stack 來字串反轉
	要用以上的class
	不用array 
	string abc =" hello world" 

 
 #include <iostream>
using namespace std;
#include <string>

struct Node{

  char data;
  Node* next;
};

class StackLinkedList{
  private: 
    Node* top;
  public: 
    StackLinkedList():top(nullptr){}
 
    void push(char data){
      Node* newNode =new Node;
      newNode->data=data;
      newNode->next=top;
      top =newNode;
    }
      
    int pop(){
      if(top==nullptr){
        cout << "stack underflow" <<endl;
        return -9999;
      }
      Node* current = top;
      top = top->next;
      int value = current->data;
      delete current;
      return value;
      
    } 
    bool isEmpty(){
  return(top==nullptr);
}
~StackLinkedList(){
  while(!isEmpty()){
    pop();
  }
}
    
};

int main() 
{
    string abc= "Hello, World!";
    StackLinkedList st;
    for (char c: abc){
      st.push(c);
    }
    string reverseABC="";
    while(!st.isEmpty()){
      reverseABC+=st.pop();
    }
    
    cout << reverseABC <<endl;
    return 0;
}
```