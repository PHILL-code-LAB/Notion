# Paul C++ Course Week 32

Owner: C.L. Liu
Last edited time: January 3, 2024 7:32 PM

[https://youtu.be/U9FX5dqFdjY](https://youtu.be/U9FX5dqFdjY)

[Phill-DS-1025.pdf](Paul%20C++%20Course%20Week%2032%2062e6fdbcb50846a883943efea70d4d47/Phill-DS-1025.pdf)

## **Stack 例題**

```cpp

#include <iostream>
using namespace std;
#include <string> 

 
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
    string expression = "(a+b)*(c+d))";
    StackLinkedList st;
    bool flag =true;
    for(char c : expression){
    if( c=='('){
      st.push(c);
    }else if(c==')'){
      if(st.isEmpty()){
        flag=false;
        break;
      }
      st.pop();
    }
    
    }
     if(flag==true){
      cout << "Yes!!" <<endl;
    }else {
      cout << "No!!" <<endl;
     }
    return 0;
}

Output:

No!!
```

![Untitled](Paul%20C++%20Course%20Week%2032%2062e6fdbcb50846a883943efea70d4d47/Untitled.png)

```cpp
//Postfix 
#include <iostream>
using namespace std;
#include <string> 
#include <cctype>
 

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
    string postfix_expression = "23+82-*";
    StackLinkedList st;
    int opt1=0,opt2=0;
     for(char c : postfix_expression){
      if(isdigit(c)){
          st.push(c-'0');
      }else {
        switch(c) {
          case '+':
            opt1=st.pop();
            opt2=st.pop();
            st.push(opt1+opt2);
            break;
          case '-':
            opt1=st.pop();
            opt2=st.pop();
            st.push(opt1-opt2);
            break;
          case '*':
            opt1=st.pop();
            opt2=st.pop();
            st.push(opt1*opt2);
            break;
          case '/':
            opt1=st.pop();
            opt2=st.pop();
            st.push(opt1/opt2);  
            break;
        }
         
      }
    
    } 
     cout << "final resoult : " << st.pop();
    return 0;
}

final resoult : -30
```

減去字元0，即減去0的ASCII碼值48，數位字元減去‘0’就得到了對應的整數數位。

所以 ‘2’ = 50 ,’0’ = 48  

  50 - 48 =2 

左邊是字元

右邊是他的代碼

找到`'0'`了嗎，可以看到他旁邊的代碼是48

 以此類推

`'1'`的代碼則是49

`'2'`的代碼則是50

一直到`'9'`的代碼是57

![Untitled](Paul%20C++%20Course%20Week%2032%2062e6fdbcb50846a883943efea70d4d47/Untitled%201.png)