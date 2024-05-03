# MaxHeap

Owner: C.L. Liu
Last edited time: March 27, 2024 4:44 AM

[https://youtu.be/8lSxGfdn2tE](https://youtu.be/8lSxGfdn2tE)

[Phill-DS-Heap.pdf](MaxHeap%205e8af1e9054b4e52ae0db7752422cbe3/Phill-DS-Heap.pdf)

更新 week 46 : 

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

Note:

int parentIndex = (index -1)/ 2 ;  

 

![Untitled](MaxHeap%205e8af1e9054b4e52ae0db7752422cbe3/Untitled.png)

因為 如果是 int parentIndex = index/ 2 ;

1/2 = 0  , 2/2 =1  所以是錯的

若改成 int parentIndex = (index -1)/ 2 ;  

(1-1)/2 = 0 ,  (2-1)/2 = 0      

(3-1)/2=1  , (4-1)/2 = 1 

所以這樣才是正確的

//上上下下 比較表示深度   , 複雜度為 log (n) 

Note: remove 功能最快速的偷吃步 

(黑色箭頭)  heapArray[0]= heapArray[currentSize-1]; // 把最下面的提上來到root

(紅色箭頭)  然後再往下做調整 

![Untitled](../Paul%20C++%20Course%20Week%2045%204c7e6093dc57444abfc6fffcfd4bd0ce/Untitled%201.png)

```cpp
//調整過後的 code 
#include <iostream>
using namespace std;

class MaxHeap{
  private:
    int* heapArray;
    int capacity;
    int currentSize;
    
    void shiftUp(int index){
      int temp =heapArray[index];
      while(index >0){
        int parentIndex = (index-1)/2; //** --- 父節點的正確索引 
        if(heapArray[parentIndex]<temp){
          heapArray[index]=heapArray[parentIndex];
          index = parentIndex;
        }else{
          break;
        }
      }
      heapArray[index] = temp;
    }
    void shiftDown(int index){// root 節點 
      int temp =heapArray[index];
      while(index<currentSize){
        int leftChildIndex= 2* index+1;   // 在while 迴圈裏面還要再比 所以也要算好 ChildIndex
        int rightChildIndex= 2* index+2;
        int largest = index;
        if(leftChildIndex <currentSize && heapArray[leftChildIndex]> heapArray[largest]){
          largest = leftChildIndex;  //要換
        }
        if(rightChildIndex< currentSize && heapArray[rightChildIndex] > heapArray[largest]){
          largest = rightChildIndex;  //要換
      }
      if(largest!=index){
        swap(heapArray[index],heapArray[largest]); ///*** == 使用swap 進行元素交換
        index = largest;
      }
      else{
        break;
      }
    }
    }
    public:
      MaxHeap(int cap):capacity(cap),currentSize(0){
        heapArray=new int[capacity];
      }
      ~MaxHeap(){
        delete[]heapArray;// [] : 連續空間
      }
      void insert(int val){//插入底部 
        if(currentSize==capacity){
          cout << "Heap is Full" << endl; // ** --- heap 已滿的提示訊息 
          return;
        }
        heapArray[currentSize]=val;
        shiftUp(currentSize);//目前的位置向上調整
        currentSize++; //因為insert 多了一筆 
        
      }
      int removeMax(){
        if(isEmpty()){ //*** -- 檢查是否為空, 以避免在空堆上進行操作
          return -1; // error code 
        }
         // 作用是拿掉最大值 (take away)->不能有預設值所以 remooveMax(不能帶值)
        int maxItem = heapArray[0];//拿走最上面的
        heapArray[0]=heapArray[currentSize-1];  // 把最下面的提上來到root
        currentSize--;
        shiftDown(0); ///  因為把最小的往前提到最全面,所以天下大亂了, 
        //倒頭來還是要從root(由 index 0 )開始調整起 
        return maxItem;
      }
      bool isEmpty(){
        return currentSize==0;
      }
};
      class PriorityQueue{
        private:
          MaxHeap maxHeap;
        public: 
          PriorityQueue(int capacity):maxHeap(capacity){}
          void enqueue(int value){
            //*** -- 刪除了不必要的空條件判斷 ,因為MaxHeap 已經有滿的檢查 
            maxHeap.insert(value);
            cout<< "Priority " << value << " has been enqueue" << endl;
          }
          int dequeue(){
            int value = maxHeap.removeMax();
            if(value == -1){
              cout << "Queue is empty " << endl;
            }
            return value;
          }
          bool isEmpty(){
            return maxHeap.isEmpty();
          }
      };

int main() 
{
    PriorityQueue q(10);
    q.enqueue(20);
    q.enqueue(5);
    q.enqueue(15);
    q.enqueue(40);
    q.enqueue(10);
    while (!q.isEmpty()){
      int dequeuedValue = q.dequeue();
      if(dequeuedValue!=-1){ // *** ---檢查dequeue 返回值 , 避免錯誤輸出 
        cout << "Dequeued: " << dequeuedValue << endl;
      }
    }
    return 0;
}

Output:

Priority 20 has been enqueue
Priority 5  has been enqueue
Priority 15 has been enqueue
Priority 40 has been enqueue
Priority 10 has been enqueue
Dequeued: 40
Dequeued: 20
Dequeued: 15
Dequeued: 10
Dequeued: 5*/ 
```