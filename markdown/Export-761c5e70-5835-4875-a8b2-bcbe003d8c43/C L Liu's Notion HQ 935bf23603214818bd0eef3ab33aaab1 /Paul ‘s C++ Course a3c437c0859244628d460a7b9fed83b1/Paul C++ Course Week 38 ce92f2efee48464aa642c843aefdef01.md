# Paul C++ Course Week 38

Owner: C.L. Liu
Last edited time: January 10, 2024 7:37 AM

[https://youtu.be/F8J7N_NYmI0](https://youtu.be/F8J7N_NYmI0)

[Phill-DS-1213, 1220, 0103 .pdf](Paul%20C++%20Course%20Week%2038%20ce92f2efee48464aa642c843aefdef01/Phill-DS-1213_1220_0103_.pdf)

## Binary Tree Traverse

### Inorder traverse 中序 → 原則: 先找左子樹 →自己 → 再找右子樹

### preorder traverse 前序 → 原則: 先找自己 → 再找左子樹 → 再找右子樹

### postorder traverse 後序 → 原則: 先找左子樹→ 再找右子樹 → 再找自己

### Note:

### complete binary tree → efficient
skewed binary tree → 浪費空間

```cpp
#include <iostream>
using namespace std;

struct TreeNode{  //TreeNode的array 
  int value;
  int leftChildIndex;
  int rightChildIndex;
};

class BinaryTree{
  private:
    TreeNode* nodes; /// root -> index  //是一個point 
    int capacity;// 因為是一棵樹 ,所以我們要制定Array 的大小,
    int nextIndex; //即將要插入的index 
  public:
    BinaryTree(int capacity):capacity(capacity) /*初始化capacity(具體化)*/ ,nextIndex(1){
      // capacity =10 
      nodes = new TreeNode[capacity+1];  // capacity +1 = 11  要Array 要預先規畫空間
      // +1是因為沒有 index 0  // 是一個point 指向了一個array 
      // 把nodes 具象化<-- TreeNode* nodes; /// root -> index 
    }
   void insert(int value){ //新增節點
     nodes[nextIndex].value =value ; //下一個index的值 = value;
     nodes[nextIndex].leftChildIndex = -1; //初始值
     nodes[nextIndex].rightChildIndex = -1;
     
     if(nextIndex >1 ){ // 判斷是不是root ? 非root 就要處理向上的問題
      int parentIndex = nextIndex /2 ; // 取商數 ,商數即 parent  
      
      if(nextIndex%2==0){
        nodes[parentIndex].leftChildIndex=nextIndex;
      }else {
        nodes[parentIndex].rightChildIndex=nextIndex;
      }
     }
     nextIndex++;  //隱藏性的遞迴 
   }   
};
int main() 
{
    BinaryTree tree(10); //給10個節點
    tree.insert();
    return 0;
}
```

![Untitled](Paul%20C++%20Course%20Week%2038%20ce92f2efee48464aa642c843aefdef01/Untitled.png)

8/2 = 4  , 4/2 =2  2/2 =1 

所以你的parent 就是你除2的商數 (不管餘數)

   int parentIndex = nextIndex /2 ; // 取商數 ,商數即 parent  

---

 //Binary Tree中,單數在右邊,雙數在左邊

      if(nextIndex%2==0){
        nodes[parentIndex].leftChildIndex=nextIndex;
      }else {
        nodes[parentIndex].rightChildIndex=nextIndex;
      }

```cpp
#include <iostream>
using namespace std;

struct TreeNode{  //TreeNode的array 
  int value;
  int leftChildIndex;
  int rightChildIndex;
};

class BinaryTree{
  private:
    TreeNode* nodes; /// root -> index  //是一個point 
    int capacity;// 因為是一棵樹 ,所以我們要制定Array 的大小,
    int nextIndex; //即將要插入的index(現在要插入的點) 
  public:
    BinaryTree(int capacity):capacity(capacity) /*初始化capacity(具體化)*/ ,nextIndex(1){
              // capacity =10 
      nodes = new TreeNode[capacity+1];  // capacity +1 = 11  要Array 要預先規畫空間
      // +1是因為沒有 index 0  // 是一個point 指向了一個array 
      // 把nodes 具象化<-- TreeNode* nodes; /// root -> index 
    }
  // insert 其實已經把順序排好了 
   void insert(int value){ //新增節點
     nodes[nextIndex].value =value ; //下一個index的值 = value;
     nodes[nextIndex].leftChildIndex = -1; //初始值
     nodes[nextIndex].rightChildIndex = -1;
     
     if(nextIndex >1 ){ // 判斷是不是root ? 非root 就要處理向上的問題
      int parentIndex = nextIndex /2 ; // 取商數 ,商數即 parent  
      
      if(nextIndex%2==0){ //Binary Tree中,單數在右邊,雙數在左邊
				// 需要填入parent 的左樹和右樹index 
        nodes[parentIndex].leftChildIndex=nextIndex;  
      }else {   
        nodes[parentIndex].rightChildIndex=nextIndex;
      }
     }
     nextIndex++;  //隱藏性的遞迴 
   }  
 
   void preorderPrint(int index ){ //輸入點為 某一個index 
     if(index >0 && index < nextIndex){ //確定值不會錯 -> core dump 
	    //Note : index < nextIndex 的意思是 輸入點不能大於即將要輸入的點(未知的數),
      //如果大於會死機,等於(=) 無意義 因為不可能等於自己
      cout << nodes[index].value << " ";
      preorderPrint(nodes[index].leftChildIndex);
      preorderPrint(nodes[index].rightChildIndex);
       
     }
   }
};
int main() 
{
    BinaryTree tree(10); //給10個節點 ,給的capacity 
    tree.insert(1);
    tree.insert(2);
    tree.insert(3);
    tree.insert(4);
    tree.insert(5);
    tree.insert(6);
    tree.insert(7);
    tree.insert(8);
    tree.insert(9);
    tree.insert(10 );
    cout << "traverse:" << endl;
    tree.preorderPrint(1); //從 root開始做Traverse
    cout << "end" << endl;
    return 0;
}

Output:

traverse:
1 2 4 8 9 5 10 3 6 7 end
```

![Untitled](Paul%20C++%20Course%20Week%2038%20ce92f2efee48464aa642c843aefdef01/Untitled%201.png)