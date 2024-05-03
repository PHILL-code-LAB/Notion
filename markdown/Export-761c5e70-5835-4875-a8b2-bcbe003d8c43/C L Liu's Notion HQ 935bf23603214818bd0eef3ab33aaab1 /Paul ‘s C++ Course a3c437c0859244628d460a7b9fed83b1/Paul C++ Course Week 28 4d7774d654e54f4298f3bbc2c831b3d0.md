# Paul C++ Course Week 28

Owner: C.L. Liu
Last edited time: January 3, 2024 7:31 PM

[https://youtu.be/CW5Asaj2Q_g](https://youtu.be/CW5Asaj2Q_g)

[Phill DS-0927.pdf](Paul%20C++%20Course%20Week%2028%204d7774d654e54f4298f3bbc2c831b3d0/Phill_DS-0927.pdf)

Double Link List 應用 -PlayList 

```cpp
#include <iostream>
using namespace std;

struct Node{
  string data;
  Node* next;
  Node* prev; 
//雙向鏈結,可向上連
};

class DoublyLinkedList{
  private:
    Node* head;
    Node* tail;  //因為可以向前, 加入tail 可以從末端開始更快. 反而中間變成最慢
  public:
    DoublyLinkedList(){
      head = nullptr;
      tail = nullptr;
    }
    
  void add(string data ){
    Node* newNode= new Node{data, nullptr,nullptr};
    if(head == nullptr){
    //當沒有node 存在於 head 與 tail 之間
    head = newNode;
    tail = newNode;
    }else{
		//有 node 存在
    tail->next = newNode; // newNode加到尾巴
    newNode->prev =tail; // newNode 本身元素, 也要把tail加入雙向鏈結
    tail =newNode; //把尾巴指向新的tail
  }
  }  
  Node* search(string data){
    Node* current =head;
    while(current !=nullptr){
      if(current->data==data){  //當找到值了
        return current;
      }
      current =current->next;      
    }
    return nullptr; //找不到值時.
  } 
  
  void update(string oldData,string newData){
    Node* node =search(oldData);
    if(node!=nullptr){ //要檢查-> 找不到的case 
      node->data =newData; //更新新值
    }
  }
  
  void print(){
    Node* current=head;
    while(current != nullptr){
      cout << current->data <<"<->";
      current=current->next;
    }
    cout << "nullptr" <<endl;
  }
  
  void remove(string data){
    Node* current = search(data); //找到要刪除的資料
    if(current !=nullptr){ //避免是找不到的情況
      if(current ->next !=nullptr ){ //後面有連到結點
        current->next->prev = current->prev; //把下一個的prev 串到前面一個  (圖的下面那條線)
      }
      if(current->prev!= nullptr){ //前面真的有東西
        current->prev->next = current->next; //把上一個的next 串到下一個 (圖的上面那條線)
      }
      if(current==head){
        head = current ->next; // 直接把 head 指向我後面 ,我就不在鏈結上了. 
      }
      if(current == tail){ // 直接把 tail 指向我前面 ,我就不在鏈結上了
        tail = current->prev;
      }
      delete current;
      return;
    }
  }
  
};

int main() 
{
    DoublyLinkedList Playlist ;
    
    Playlist.add("不為誰而做的歌");
    Playlist.add("修煉愛情");
    Playlist.add("江南");
    Playlist.print();
    
    
    Playlist.update("修煉愛情","小酒窩");
    Playlist.print();
    
    Playlist.remove("江南");
    Playlist.print();
    
    
    return 0;
}
```

Double Link List 應用 -瀏覽器 back , forward

練習 瀏覽器

class 做修改

URL → 輸入網址

URL*3 

back 上一頁 

forward 下一頁

輸入 URL 

print URL

輸入 back, 呼叫 back() 

跳到 上一頁 印出上一頁的 URL

輸入 forward , forward()

跳到 下一頁 印出下一頁的 URL

```cpp

```

環狀LinkList 

![Untitled](Paul%20C++%20Course%20Week%2028%204d7774d654e54f4298f3bbc2c831b3d0/Untitled.png)

![Untitled](Paul%20C++%20Course%20Week%2028%204d7774d654e54f4298f3bbc2c831b3d0/Untitled%201.png)

```cpp
#include <iostream>
using namespace std;

struct Node{
  int data; 
  Node* next;
};
class CircularLinkedList{
  private:
   Node* head;
  public: 
    CircularLinkedList(){
      head=nullptr;
    }
    
  void add(int data){
    Node* newNode =new Node{data,nullptr};
    if(head==nullptr){ //鍊表為空
      head = newNode; //把自己加入head
      newNode->next=head;//因為元素只有一個 把自己指回自己 (環狀)
    }else{ //已經有node 在裡面了, 加尾巴
      Node* current =head; //設定魁儡變數在開頭
      while(current->next!=head){ //環狀特徵 還沒到底
        current=current->next; //指向下一個
      }
      //以指向最後一個
      current->next = newNode; //把自己加在尾巴
      newNode->next = head; //環狀指回 head 
    }    
  }
  
  void  print(void){
    Node* current=head;
    do{
      cout << current->data << "->";
      current=current->next;
    }while(current!=head); // 已繞回頭
    cout << "Stop" <<endl; //作結束記號.
    
  }
};

int main() 
{
    CircularLinkedList list;
    list.add(123);
    list.add(456);
    list.add(789);
    list.print();
    return 0;
}

Output: 
123->456->789->Stop
```

```cpp
#include <iostream>
using namespace std;

struct Node{
  int data; 
  Node* next;
};
class CircularLinkedList{
  private:
   Node* head;
  public: 
    CircularLinkedList(){
      head=nullptr;
    }
    
  void add(int data){
    Node* newNode =new Node{data,nullptr};
    if(head==nullptr){ //鍊表為空
      head = newNode; //把自己加入head
      newNode->next=head;//因為元素只有一個 把自己指回自己 (環狀)
    }else{ //已經有node 在裡面了, 加尾巴
      Node* current =head; //設定魁儡變數在開頭
      while(current->next!=head){ //環狀特徵 還沒到底
        current=current->next; //指向下一個
      }
      //以指向最後一個
      current->next = newNode; //把自己加在尾巴
      newNode->next = head; //環狀指回 head 
    }    
  }
  
  Node* search(int data){
    Node* current = head;
      do{
         //每次先判斷內容 不對在往下走 
         if(current->data == data){
           return current; //找到
         }
        current = current->next; //繼續往下走 
        
      }while(current!=head); //找到繞回來 
        return nullptr;  /// 繞回來 還沒找到 
      
  }
  
  
  void  print(void){
    Node* current=head;
    do{
      cout << current->data << "->";
      current=current->next;
    }while(current!=head);
    cout << "Stop" <<endl;
    
  }
};

int main() 
{
    CircularLinkedList list;
    list.add(123);
    list.add(456);
    list.add(789);
    list.print();
    
    Node* foundNode = list.search(456);
    if(foundNode==nullptr) {
      cout << "Not Found" << endl;
      
    }else {
      cout << "found: " << foundNode->data <<endl;
    } 
    
    
    
    return 0;
}

Output: 
123->456->789->Stop
found: 456
```

```cpp
#include <iostream>
using namespace std;

struct Node{
  int data; 
  Node* next;
  
};
class CircularLinkedList{
  private:
   Node* head;
  public: 
    CircularLinkedList(){
      head=nullptr;
    }
    
  void add(int data){
    Node* newNode =new Node{data,nullptr};
    if(head==nullptr){ //鍊表為空
      head = newNode; //把自己加入head
      newNode->next=head;//因為元素只有一個 把自己指回自己 (環狀)
    }else{ //已經有node 在裡面了, 加尾巴
      Node* current =head; //設定魁儡變數在開頭
      while(current->next!=head){ //環狀特徵 還沒到底
        current=current->next; //指向下一個
      }
      //以指向最後一個
      current->next = newNode; //把自己加在尾巴
      newNode->next = head; //環狀指回 head 
    }    
  }
  
  Node* search(int data){
    Node* current = head;
      do{
         //每次先判斷內容 不對在往下走 
         if(current->data == data){
           return current; //找到
         }
        current = current->next; //繼續往下走 
        
      }while(current!=head); //找到繞回來 
        return nullptr;  /// 繞回來 還沒找到 
      
  }
  
    void update ( int oldData , int newData){
    Node* node = search(oldData);
    if(node != nullptr) { // 如果有找到 
       node->data = newData;
    }
  }
  
  void remove(int data) {
    Node* current=head;
    Node* prev = nullptr;  // 因為是單向連結 必須保留上一個 以便移除
    do {
      if(current->data ==data) { //找到 
        if(prev != nullptr){
          prev->next =current->next ; //我被刪掉  因為我要消失了, 上一個人的下一個人 = 我的下一個人
        }
        if(current == head){ // 我是頭 要被刪除 
          
          head =head-> next; // 必須指向下一個  也等於 = current-> next 
        }
         delete current;
         return;
        
      }  
      prev=current; // 我就是下一個人的前一個人 
      current=current->next;  //保留了 prev 再向下走
    }while(current!=head); // 找到繞回頭 
  }
  
  void  print(void){
    Node* current=head;
    do{
      cout << current->data << "->";
      current=current->next;
    }while(current!=head);
    cout << "Stop" <<endl;
    
  }

  
  
};

int main() 
{
    CircularLinkedList list;
    list.add(123);
    list.add(456);
    list.add(789);
    list.print();
    
    Node* foundNode = list.search(456);
    if(foundNode==nullptr) {
      cout << "Not Found" << endl;
      
    }else {
      cout << "found: " << foundNode->data <<endl;
       
    } 
    //update & remove 
    
    list.update(123,999); // update 123 -> 999 
    list.print();
    list.remove(456);
    //list.remove(999);
    list.print(); 
    
    
    return 0;
}

Output:

123->456->789->Stop
found: 456
999->456->789->Stop
999->789->Stop
```

```cpp
#include <iostream>
using namespace std;

struct Node{
  int data; 
  Node* next;
  
};
class CircularLinkedList{
  private:
   Node* head;
  public: 
    CircularLinkedList(){
      head=nullptr;
    }
    
  void add(int data){
    Node* newNode =new Node{data,nullptr};
    if(head==nullptr){ //鍊表為空
      head = newNode; //把自己加入head
      newNode->next=head;//因為元素只有一個 把自己指回自己 (環狀)
    }else{ //已經有node 在裡面了, 加尾巴
      Node* current =head; //設定魁儡變數在開頭
      while(current->next!=head){ //環狀特徵 還沒到底
        current=current->next; //指向下一個
      }
      //以指向最後一個
      current->next = newNode; //把自己加在尾巴
      newNode->next = head; //環狀指回 head 
    }    
  }
  
  Node* search(int data){
    Node* current = head;
      do{
         //每次先判斷內容 不對在往下走 
         if(current->data == data){
           return current; //找到
         }
        current = current->next; //繼續往下走 
        
      }while(current!=head); //找到繞回來 
        return nullptr;  /// 繞回來 還沒找到 
      
  }
  
    void update ( int oldData , int newData){
    Node* node = search(oldData);
    if(node != nullptr) { // 如果有找到 
       node->data = newData;
    }
  }
  
  void remove(int data) {
    Node* current=head;
    Node* prev = nullptr;  // 因為是單向連結 必須保留上一個 以便移除
    do {
      if(current->data ==data) { //找到 
        if(prev != nullptr){
          prev->next =current->next ; //我被刪掉  因為我要消失了, 上一個人的下一個人 = 我的下一個人
        }
        if(prev == head){ // 我是頭 要被刪除 
          
          head =head-> next; // 必須指向下一個  也等於 = current-> next 
        } 
        
         delete current;
         return;
        
      }  
      prev=current; // 我就是下一個人的前一個人 
      current=current->next;  //保留了 prev 再向下走
    }while(current!=head); // 找到繞回頭 
  }
  
  void  print(void){
    Node* current=head;
    do{
      cout << current->data << "->";
      current=current->next;
    }while(current!=head);
    cout << "Stop" <<endl;
    
  }

  
  
};

int main() 
{
    CircularLinkedList list;
    list.add(123);
    list.add(456);
    list.add(789);
    list.print();
    
    Node* foundNode = list.search(456);
    if(foundNode==nullptr) {
      cout << "Not Found" << endl;
      
    }else {
      cout << "found: " << foundNode->data <<endl;
       
    } 
    //update & remove 
    
    list.update(123,999); // update 123 -> 999 
    list.print();
    list.remove(456);
    list.remove(999);
    list.print(); 
    
    
    
    return 0;
}

Output:

123->456->789->Stop
found: 456
999->456->789->Stop
789->Stop
```