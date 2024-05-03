# Paul C++ Course Week 46

Owner: C.L. Liu
Last edited time: March 27, 2024 1:17 AM

[https://youtu.be/9uTYkGTBY8Q](https://youtu.be/9uTYkGTBY8Q)

[Phill-DS-0220 0306.pdf](Paul%20C++%20Course%20Week%2046%20eb1c1a21f87748c3bfd6afddf2d284a4/Phill-DS-0220_0306.pdf)

```cpp
#include <iostream>
using namespace std;

class MaxHeap {
  
  private:
  
    int* heapArray;  // 指標開頭將產生實體 (動態的Array)
    int capacity; 
    int currentSize; // 目前狀態(現在的點到哪裡了)
    
    void shiftUp(int index){
      int temp = heapArray[index]; //把現在的值 ,放進魁儡變數裡面 
      while(index>0){ //因為到root 要停  , 但大於root的index 要繼續做 
        int parentIndex = (index -1)/ 2 ; 
        if(heapArray[parentIndex] < temp){ // 要換  
          heapArray[index] = heapArray[parentIndex]; //換 
          index = parentIndex;
        }
        else{
          break;
        }
      }
      heapArray[index] =temp; //我的最高點 -->//換到最後,index為最高點填入temp中  
    }
    void shiftDown(int index){ // root 節點 
      int temp = heapArray[index];
      int  ChildIndex = 2*index+1; // 由下往上 要先算
      while(ChildIndex < currentSize){
        if(temp <  heapArray[ChildIndex]){
          heapArray[index]= heapArray[ChildIndex]; //要換
          index = ChildIndex;
          ChildIndex=2*index+1; // 在while 迴圈裏面還要再比 所以也要算好 ChildIndex
        }else{
          break;
        }
      } 
      heapArray[index] = temp; //我的最低點 -->//換到最後,index為最低點填入temp中
    }
  
  public: 
   MaxHeap(int cap):capacity(cap),currentSize(0){ //初始化
     heapArray = new int [capacity]; //連續空間
   }
   
   ~MaxHeap(){
     delete[] heapArray;  // [] : 連續空間
     // C++ 11 的連續空間歸還 
   }
   
//Step1
  void insert(int val){ //插入底部 
     if(currentSize==capacity){
       cout << "滿了" << endl;
       return;
     }
     heapArray[currentSize] = val; // 插入最後一個   (先左再右的原則)  : heapArray[currentsize]-->剛好是最後一個
     shiftUp(currentSize);//目前的位置向上調整
     currentSize++; //因為insert 多了一筆 
     
   }
   //
   // Note : currentsize 從0 開始
   //currentsize-1 = 右邊的樹 8 的位置 ,所以 currentsize  等於 30的位置 
   // 那 currentsize -1 等於 30, 那currentsize = 50的位置 
   // 所以一定會 先左再右的原則
						
//Step2
   int removeMax(){ 
   // 作用是拿掉最大值 (take away)->不能有預設值所以 remooveMax(不能帶值)
     int maxItem= heapArray[0]; //拿走最上面的
     heapArray[0]= heapArray[currentSize-1]; // 把最下面的提上來到root
     currentSize--;
     shiftDown(0); ///  因為把最小的往前提到最全面,所以天下大亂了, 
     //倒頭來還是要從root(由 index 0 )開始調整起  
     return maxItem;
   }
   bool isEmpty(){
     return currentSize==0;
   }
};

int main() 
{
    
    int number[]={8,5,2,9,10,6,3};
    int length=sizeof(number) / sizeof(number[0]);
    MaxHeap heap(length);
    for (int i=0; i<length;i++){
      heap.insert(number[i]);
    }
     int j=0;
     while(!heap.isEmpty()){
       number[j++]=heap.removeMax();
     }
     for(int z=0;z<length;z++){
       cout << number[z] << " ";
     }
    return 0;
}
```

Heap 的應用:

使用上面的class 

Heap Sort 

int numbers[]={8,5,2,9,10,6,3}

———————————————————————————————————————————-

練習

Priority Queue
	item 會有一個優先值 20,5,15,40,10
	class PriorityQueue →使用class MaxHeap

             enqueue : 照順序 equeue 

             dequeue : 依照優先權高的取得

```cpp
#include <iostream>
using namespace std;
class ProiorityQueue{
  private:
    MaxHeap maxHeap;
  
  public: 
    ProiorityQueue(int capacity): maxHeap(capacity){}
    void enqueue(int val){
      
        maxHeap.insert (value);
        cout << "Proiority" << value << "has been enqueue"<<endl;
    }
    int dequeue(){
      if(maxHeap.isEmpty()){
        cout << "Queue has been empty." << endl;
        return -1; //error code 
      }
      int value = maxHeap.removeMax();
      return value;
    }
    bool isEmpty(){
      return maxHeap.isEmpty();
    }
};
int main() 
{
    ProiorityQueue q(10);
    q.enqueue(20);
    q.enqueue(5);
    q.enqueue(15);
    q.enqueue(40);
    q.enqueue(10);
    
    while(q.isEmpty()){
      q.dequeue();
    } 
    return 0;
}
```