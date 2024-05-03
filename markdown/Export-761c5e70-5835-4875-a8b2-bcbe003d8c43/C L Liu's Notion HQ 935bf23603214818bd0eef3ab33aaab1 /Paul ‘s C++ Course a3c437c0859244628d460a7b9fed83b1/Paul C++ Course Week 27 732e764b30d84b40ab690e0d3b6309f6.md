# Paul C++ Course Week 27

Owner: C.L. Liu
Last edited time: January 3, 2024 7:31 PM

[https://youtu.be/ho_rVS0frGQ](https://youtu.be/ho_rVS0frGQ)

[Phill-DS-0920.pdf](Paul%20C++%20Course%20Week%2027%20732e764b30d84b40ab690e0d3b6309f6/Phill-DS-0920.pdf)

單向鏈結 Singly Linked List 

```cpp
#include <iostream>
using namespace std;

struct Node{
  int data;
  Node* next;   
};
class LinkedList{
   private:
      Node* head;
      //Node* tail;  
   public:
     LinkedList(){  
       head = nullptr;   
        
     } 
     
   void add(int data ){ 
     Node* newNode = new Node{data, nullptr};  //動態 ,動態規劃記憶體
                            //date ->int data  // nullptr -> Next* next
       //  {data, nullptr} 會映射到 struct Node 內的結構
     if(head==nullptr){  
       head =newNode;   
     }else{  // 有  node inside
       Node* current = head;  
       while(current->next!=nullptr){  
         current = current->next;  
       }
       current-> next =newNode;  
     }
  }
  
  void print(){
    Node* current=head;
    while (current !=nullptr){ //先檢查自己 是不是 nullptr
      cout << current-> data << "->"; //先印 
      current = current -> next; // 再接
    }
    cout << "->nullptr" << endl;
  }
  
  
  //search 
  //-------------------------------------------------------------------------
  Node* search(int data) {
    Node* current = head;
    while(current !=nullptr){
      if(current -> data == data){ // hit data 
        return current; //把節點傳回去
      }
      current = current -> next; 
      
    }
    return nullptr; //甚麼都沒找到  回傳 null 
  }
  
  //-----------------------------------------------------------------------
  //update   --找到old data  改成 new data 
  void update(int oldData , int newData){
     Node* node =search(oldData); // 接住找到的節點 
     if(node !=nullptr){ //檢查清楚 防止沒找到的情況 !!! 
         node -> data =  newData;  // in lvaule  --> 賦值     
     }  //return bool  --> HW  
  }
  
  
  //--------------------------------------------------------------------------
   //Remove
   void remove (int data ) {           // Step1 
     Node* current =head;              //Step2 
     Node* previous = nullptr; //不知道previous 是多少 先填 nullptr   //Step3   
     while(current!=nullptr){  //不停地往下追 追到nullptr             //Step4
       if(current->data ==data){ ///找到了值 (我)                    //Step5 
        if(previous==nullptr){ //代表現在還沒 bookkeeping 過 , 是頭(head)節點   // Step 9 
          head = current->next ; // 直接把頭(head) 指到我的下一個 因為我(head)要被刪掉了  //Step 10 
          
        }else { //不是頭節點的狀況 做連接的手術    //Step 11
         previous -> next = current->next; // (跳過(我)--->刪除) 接續 把上一個直接 接到我的下一個節點    //Step 8       
        }
        delete current; //處理自己空間的釋放   //Step12 
                           
       }
       previous = current ; //把自己記錄下來 因為我是下一個人的上一個位置 (previous , bookkeeping )   //Step6
       current =current->next; // 放心繼續找下一去  // Step 7 
     }
   } //bool version -> 作業
  
  
  //-------------------------------------------------------------------------
  ~LinkedList() { // 當物件結束要去執行的部分  //// 釋放記憶體(動態規劃部分記憶體) -deconstructor
    Node* current =head;
    while(current!=nullptr){ //動態記憶體 要一個一個回收回來
      Node* temp = current;  //記下要release  點的位置 
      current =current->next; //先把魁儡變數移到下⼀個⼈ 避免我被release 掉消失
      delete temp;  //最後再一次 del temp   --//釋放自己
    }
    
  }
  
};

int main() 
{
    
    LinkedList list;
    list.add(10);
    list.add(20);
    list.add(30);
     
    list.print(); //加成功了
    
    list.update(20,25);
    list.print();
    
    list.remove(10); //測試 特殊情況 當如果是頭 (head)的話 
    list.print();
    
    return 0;
}

Output:

10->20->30->->nullptr
10->25->30->->nullptr
25->30->->nullptr
```

雙向鏈結  Doubly Linked List 

![Untitled](Paul%20C++%20Course%20Week%2027%20732e764b30d84b40ab690e0d3b6309f6/Untitled.png)

![Untitled](Paul%20C++%20Course%20Week%2027%20732e764b30d84b40ab690e0d3b6309f6/Untitled%201.png)

```cpp
#include <iostream>
using namespace std;

struct Node{
  int data;
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
    
  void add(int data ){
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
  Node* search(int data){
    Node* current =head;
    while(current !=nullptr){
      if(current->data==data){  //當找到值了
        return current;
      }
      current =current->next;      
    }
    return nullptr; //找不到值時.
  } 
  
  void update(int oldData,int newData){
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
  
  void remove(int data){
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
    DoublyLinkedList list ;
    list.add(9487);
    list.add(9488);
    list.add(9489);
    list.print();
    
    list.remove(9488);
    list.print();
    return 0;
}

Output:

9487<->9488<->9489<->nullptr
9487<->9489<->nullptr
```