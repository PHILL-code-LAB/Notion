# Paul C++ Course Week 10

Owner: C.L. Liu
Last edited time: January 3, 2024 7:30 PM

[Phill-CPP-0503.pdf](Paul%20C++%20Course%20Week%2010%20f33bdadaf0c743438a8a8654fcb19f17/Phill-CPP-0503.pdf)

[https://youtu.be/MzACJFZO-Rg](https://youtu.be/MzACJFZO-Rg) 

```cpp
** for 的無窮迴圈

#include <iostream>
using namespace std;

int main() 
{
    int i=0;
    do{
      cout << "please input a number (>=100" <<endl;
      cin >> i;
    }while(i<100);
    cout << "done";
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int main() 
{
    int i=0;
    while(true){
      cout << "i="<<i<<endl;
      i+=2;
    }
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;
int main()
{
int i=1; 
while(i<=10){
  
    if(i%2==0){ 
        cout<<i<<"是偶數"<<endl;
    }
i=i+1;
}
return 0;
}

Output:

2是偶數
4是偶數
6是偶數
8是偶數
10是偶數

```

```cpp
#include <iostream>
using namespace std;

int main() 
{
    int A[12]={2,2,3,4,5,5,5,6,7,7,8,9};
    int B[12]={0};
    int i, j, k=0;
    for(i=0;i<12;i++){
      for(j=0; j<k; j++){
        if(A[i]==B[j]){ //重複了
          break;
          
      }
      cout << "j:" <<j << endl;
    }
        if(j==k){ //沒找到
        B[k]=A[i];
       cout <<"\t"<< "k:" <<k << endl;
       
      k++; //累加
  }
}
 cout << "result->"; 
  for(int z=0; z<k;z++){ 
      cout << B[z] << " "; 
  }
  cout << "end"<<endl;
  return 0;
}
```

```cpp
/*作業
do while…
確定您要結束嗎? → ‘y’ */

#include <iostream>
using namespace std;

int main()
{
    char choice;
    do
    {
        cout<<"Would you want to leave ? (Y/N)"<<endl;
        cout<< "You must type a 'Y' or an 'N'.\n";
        cin >> choice;

    }while((choice !='Y')&&(choice !='N')&&(choice !='y')&&(choice !='n'));
      if(choice=='Y' || choice=='y'){
        cout << "bye"<<endl;
      }
return 0;
}
```

```cpp
/*作業
string → “hello world!” → “!lo le”
for i—
if, continue
倒反來印(跳⼀個) */

#include <iostream>
using namespace std;

int main() 
{
   char array[]={"Hello World!"};
   int length = sizeof(array) / sizeof(array[0]);
   for(int i=length;i>=0;i--){
      if(i%2==0){
        
        continue;
      }
        cout << array[i];
     }
      
    
   
     
    return 0;
}

/* Output:

!lo le */
```