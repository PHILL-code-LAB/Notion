# Paul C++ Course Week 6

Owner: C.L. Liu
Last edited time: May 23, 2023 10:04 AM

[Phill-CPP-0405.pdf](Paul%20C++%20Course%20Week%206%20d1de413b2ddc42219d651ae84525ae89/Phill-CPP-0405.pdf)

[https://youtu.be/y9jabJ2Taxc](https://youtu.be/y9jabJ2Taxc)

[https://youtu.be/hnS7heBFCik](https://youtu.be/hnS7heBFCik)

練習1:

```cpp
#include <iostream>
using namespace std;

//找最大 & 找最小
int main() 
{
    int arr[]={3,5,2,7,1,8};
    int size = sizeof(arr)/sizeof(arr[0]);
    int max , min; 
    int *p_max=&max, *p_min=&min; 
    
    *p_max=arr[0];
    *p_min=arr[0];
    
    for(int i=1;i<size;i++){
      if(arr[i]<*p_min){
          *p_min=arr[i];        
      }
      if(arr[i]>*p_max){
        *p_max=arr[i];
      }
    }
    
    cout << max << endl;
    cout << min << endl;
    
    return 0;
}
```

練習2:

```cpp
#include <iostream>
using namespace std;

void sum(int a ,int  b , int *c ){
  *c=a+b;
  cout << "in function ->" << *c << endl;
}

int main() 
{
    int total;
    int *p_total=&total;
   
    sum(1,2,p_total);
    cout << "in main:" << total <<endl;
     cout <<"*p_total>>>>" <<*p_total <<endl;
    return 0;
}

---------------------------
Output:

in function ->3
in main:3
*p_total>>>>3
```

練習3 

```cpp
#include <iostream>
using namespace std;

void funMaxMin(int *arr,int *fun_Max,int *fun_Min, int size ){
  
  *fun_Min=arr[0];
  *fun_Max=arr[0];
  for(int i=1;i<size;i++){
    if(arr[i]<*fun_Min){
      *fun_Min=arr[i];
    }
    if (arr[i]>*fun_Max){
      *fun_Max=arr[i];
    }
  }

  
}

int main() 
{
    int arr[]={3,5,2,7,1,8};
    int Max,Min;
 
    
    int size = sizeof(arr)/sizeof(arr[0]);
    funMaxMin(arr,&Max,&Min,size);
    cout << "Max value:" << Max << endl;
    cout << "Min value:" << Min << endl;
    return 0;
}

----------------------
Output:

Max value:8
Min value:1
```