# Paul C++ Course Week 15

Owner: C.L. Liu
Last edited time: January 3, 2024 7:30 PM

[Phill-CPP-0614.pdf](Paul%20C++%20Course%20Week%2015%206d24a0b868bc42a4a9ad6e5c6f28b1b0/Phill-CPP-0614.pdf)

[https://www.youtube.com/watch?v=mc6zcaw4L7c&list=PLcX_scbPX1dFaCCTDIBJM_UUEXj6vhCyU&index=29](https://www.youtube.com/watch?v=mc6zcaw4L7c&list=PLcX_scbPX1dFaCCTDIBJM_UUEXj6vhCyU&index=29) 

```cpp
// 惡作劇 按門鈴
#include <iostream>
using namespace std;

int main() 
{
    int count[101]={0};
    int press[10][2]={0};
    
    press[0][0]=16;
    press[0][1]=18;
    
    press[1][0]=15;
    press[1][1]=20;
    
    press[2][0]=19;
    press[2][1]=21;
   //----- 投影的結構
   
   int child =3;  
   for(int i=0;i<child;i++){
     for(int j=press[i][0];j<=press[i][1];j++){  // 起始的房子 跟結束的房子 
       count[j]=1;
       
     }
   }
    int sum=0;
    for(int k=0;k<=101;k++){
      if(count[k]==1){
        sum++;
      }
    }
    cout << "total->" << sum;
    return 0;
}

Output : 
total->7
```

```cpp
#include <iostream>
using namespace std;

void print_matrix(int M[][3], int row , int col){
   int N[3][3] ={0};
   cout << "Before: " <<endl;
  for(int i=0;i<row;i++){
    for(int j=0;j<col;j++){
     cout << M[i][j] << ' ';  
    }
     cout << endl; 
  }
  cout << endl;
  cout << "After:" <<endl;
  for(int i=0;i<row;i++){
    for(int j=0;j<col;j++){
      N[i][j]=M[j][i];
      
      cout << N[i][j] << ' ';
    }
    cout <<endl;
  }
}
int main() 
{
    int M[3][3]={{1,2,3},{4,5,6},{7,8,9}};
    print_matrix(M,3,3);
    return 0;
}

Output:

Before: 
1 2 3 
4 5 6 
7 8 9 

After:
1 4 7 
2 5 8 
3 6 9

```

![Untitled](Paul%20C++%20Course%20Week%2015%206d24a0b868bc42a4a9ad6e5c6f28b1b0/Untitled.png)

```cpp
#include <iostream>
using namespace std;

void print_matrix(int M[][3], int row , int col){
   int N[3][3] ={0};
   int Mul[3][3]={0};
   cout << "Before: " <<endl;
 
  for(int i=0;i<row;i++){
    for(int j=0;j<col;j++){
     cout << M[i][j] << ' ';  
    }
     cout << endl; 
  }
     cout <<"After: " <<endl;
      
  for(int i=0;i<row;i++){
    for(int j=0;j<col;j++){
      N[i][j]=M[j][i];
      
      cout << N[i][j] << ' ';
    }
    cout <<endl;
  }
cout << endl;
///---------------------------------------///
cout << "M^2 (multiplied) : " <<endl;
  for (int i =0;i<row;i++){
     for(int j=0;j<col;j++){
        for(int k=0;k<col;k++){
            Mul[i][j]+=M[i][k]*N[k][j];
     }
     cout << Mul[i][j]<<' ';
    }
    cout << endl;
  }
}
int main() 
{
    int M[3][3]={{1,2,3},{4,5,6},{7,8,9}};
    print_matrix(M,3,3);
    return 0;
}
 

Output:

Before: 
1 2 3 
4 5 6 
7 8 9 

After:
1 4 7 
2 5 8 
3 6 9 

M^2 (multiplied) :  
14 32 50 
32 77 122 
50 122 194

Note : 如下圖  k 為 i的第k個數值 
1 2 3      1 4 7
 k k k
4 5 6   x  2 5 8
  
7 8 9      3 6 9
```

 

![Untitled](Paul%20C++%20Course%20Week%2015%206d24a0b868bc42a4a9ad6e5c6f28b1b0/Untitled%201.png)