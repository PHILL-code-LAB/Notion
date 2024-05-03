# Paul C++ Course Week 16

Owner: C.L. Liu
Last edited time: January 3, 2024 7:30 PM

[Phill-CPP-0621.pdf](Paul%20C++%20Course%20Week%2016%206d373c4882cc4beea562f1d5effb9fb9/Phill-CPP-0621.pdf)

 [https://youtu.be/evnRHV-Zwkg](https://youtu.be/evnRHV-Zwkg)

C++ —→ OOP 物件導向

**Struct** 

```cpp
Sample 1:

#include <iostream>
using namespace std;

struct Address{
  const char *name;
  int  number;
  const  char *street;
  const char *city;
  const char *zip;
};

int main() 
{
    Address a ={ //初始化
      "Phill Liu",
      1,
      "chung hsiao",
      "Taipei",
      "123"
    };
    
    cout << a.name  <<endl;
    cout << a.number <<endl;
    return 0;
}

Output:

Phill Liu
1
```

```cpp
Sample 2 

#include <iostream>
using namespace std;

struct Address{
  const char *name;
  int  number;
  const  char *street;
  const char *city;
  const char *zip;
};

int main() 
{
    Address a ={ //初始化
      "Phill Liu",
      1,
      "chung hsiao",
      "Taipei",
      "123"
    };
    Address* p= &a;   // struct與指標 結合
    
    
    cout << a.name  <<endl;
    cout << a.number <<endl;
    cout << p->name  <<endl;  // struct 與指標 結合
    cout << p->number <<endl; // struct 與指標 結合
    return 0;
}

Output:

Phill Liu
1
Phill Liu
1

```

```cpp
Sample 3 
#include <iostream>
using namespace std;

struct SportsCar {
  const char *brand;
  const char *model;
  int  topSpeed;
};

int main() 
{
    // 結構 跟 陣列
    const int ARRAY_SIZE =3;
    SportsCar sportCars[ARRAY_SIZE]={
      {"Ferrari" , "F8 Tributo " , 340 },
      {"Lamborghini", "Huracan EVO" , 325},
      {"Proche" , "911 GT3" , 310}
    };
    
    for(int i=0;i<ARRAY_SIZE;++i){
      cout <<"Brand :" << sportCars[i].brand <<endl;
      cout << "Model :" <<sportCars[i].model <<endl;
      cout << "TopSpeed :" << sportCars[i].topSpeed <<endl;
      cout << "-------------" << endl;
    }
    
    return 0;
}

Output:

Brand :Ferrari
Model :F8 Tributo 
TopSpeed :340
-------------
Brand :Lamborghini
Model :Huracan EVO
TopSpeed :325
-------------
Brand :Proche
Model :911 GT3
TopSpeed :310
-------------
```

```cpp
#include <iostream>
using namespace std;

struct SportsCar {
  const char *brand;
  const char *model;
  int  topSpeed;
};

int main() 
{
    // 結構 跟 陣列 -- > // 改成指標版本
    const int ARRAY_SIZE =3;
    SportsCar sportCars[ARRAY_SIZE]={
      {"Ferrari" , "F8 Tributo " , 340 },
      {"Lamborghini", "Huracan EVO" , 325},
      {"Proche" , "911 GT3" , 310}
    };
    
    
      SportsCar* ptr = sportCars; //陣列的名字就是他的地址 所以不用加  & 
      
    
    for(int i=0;i<ARRAY_SIZE;++i){
   
      cout << ptr->brand  <<endl;
      cout << ptr->model <<endl;
      cout << ptr->topSpeed  <<endl; 
      cout << "-------------" << endl;
      ++ptr; //指到下一個 struct的 address
    }
    
    return 0;
}

Output:

Ferrari
F8 Tributo 
340
-------------
Lamborghini
Huracan EVO
325
-------------
Proche
911 GT3
310
-------------
```