# Paul C++ Course Week 13

Owner: C.L. Liu
Last edited time: January 3, 2024 7:30 PM

[Phill-CPP-0531.pdf](Paul%20C++%20Course%20Week%2013%20cb20492ee5a345cc8f7c040e9756cc19/Phill-CPP-0531.pdf)

[https://youtu.be/e4JricNGOTs](https://youtu.be/e4JricNGOTs)

```cpp
#include<iostream>
using namespace std;

int main()
{
    char input;
    int num;
    cin >>input;
    
    if(input >='A'&& input <='Z'){
      num=input -'A';
      //cout << num;
      for(int i=0;i<=num;i++){
        for(int j=0;j<i;j++){
        cout <<" ";
       
        }
         cout << char('A'+i) <<endl;
      }
    }
 
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int main() 
{
    int n;
    cin >> n;
    for(int i=0;i<n;i++ ){
      for(int j=1;j<n-i;j++){
        cout <<" ";
        //cout <<"j" <<j;
      }
      for(int k=0;k<=2*i;k++){
        cout<<"*";
 
      }
      cout <<""<<endl;
    }
    return 0;
}

Output:

      *
     ***
    *****
   *******
  *********
 ***********
*************
```

```cpp
#include<iostream>
using namespace std;

int main()
{
    int N;
    int i, j;

    cin >> N;

    for( i=1 ; i<=N ; i++ )
    {
        for( j=1 ; j<=i ; j++ )
        {
            cout << "*";
        }
        cout << endl;
    }

    return 0;
}

Output:

*
**
***
****
```