# Paul C++ Course Week 45

Owner: C.L. Liu
Last edited time: March 27, 2024 4:43 AM

[https://youtu.be/U2WlvrXRfro](https://youtu.be/U2WlvrXRfro) 

ref: [https://alrightchiu.github.io/SecondRound/comparison-sort-heap-sortdui-ji-pai-xu-fa.html](https://alrightchiu.github.io/SecondRound/comparison-sort-heap-sortdui-ji-pai-xu-fa.html) 

[Phill-DS-0228.pdf](Paul%20C++%20Course%20Week%2045%204c7e6093dc57444abfc6fffcfd4bd0ce/Phill-DS-0228.pdf)

![Untitled](Paul%20C++%20Course%20Week%2045%204c7e6093dc57444abfc6fffcfd4bd0ce/Untitled.png)

Heap 大魔王

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
        int parentIndex = (index-1) / 2 ; 
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
     shiftDown(0); ///  因為把最小的往前提到最全面,所以天下大亂了, 倒頭來還是要從root(由 index 0 )開始調整起  
     return maxItem;
   }
};

int main() 
{
    cout << "Hello, World!";
    return 0;
}
```

Note: remove 功能最快速的偷吃步 

(黑色箭頭)  heapArray[0]= heapArray[currentSize-1]; // 把最下面的提上來到root

(紅色箭頭)  然後再往下做調整 

![Untitled](Paul%20C++%20Course%20Week%2045%204c7e6093dc57444abfc6fffcfd4bd0ce/Untitled%201.png)