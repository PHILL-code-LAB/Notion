# Paul C++ Course Week 7

Owner: C.L. Liu
Last edited time: January 9, 2024 9:47 PM

[Phill-CPP-0412.pdf](Paul%20C++%20Course%20Week%207%200b44d4da11f04db7bb8748895f38b95c/Phill-CPP-0412.pdf)

 [https://youtu.be/8TrHyGB-k9A](https://youtu.be/8TrHyGB-k9A)

## 結構

- 陣列同質性
- 異質性資料

```cpp
#include <iostream>
using namespace std;

int main() 
{
    struct Address{
      const char *name;
      int number;
      const char *street;
      const char *city;
      const char *zip;
    }; //收尾
    Address a = { //變數的宣告,初始化 
    "Phill Liu",
    1,
    "Neihu",
    "Taipei",
    "114"
    }; 
    cout << a.name << a.number << a.zip<<endl;
    return 0;
}

Output:

Phill Liu1114
```

### struct → pointer 怎麼辦

### pointer of struct

```cpp
#include <iostream>
using namespace std;

int main() 
{
    struct Address{
      const char *name;
      int number;
      const char *street;
      const char *city;
      const char *zip;
    }; //收尾
  Address a = { //變數的宣告,初始化 
    "Phill Liu",
    1,
    "Neihu",
    "Taipei",
    "114"
    };   
  Address* ptr_a = &a;
  cout << &a <<endl;
  cout << ptr_a <<endl;
  cout << ptr_a -> name <<endl; //struct pointer dereference 
  //cout << a.name << a.number << a.zip<<endl;
    return 0;
}

Output:

0x7fff9565f420
0x7fff9565f420
Phill Liu
```

### Struct + array

```cpp
#include <iostream>
using namespace std;

int main() 
{
    struct SportCar{
      const char *brand;
      const char *model;
      int topSpeed;
    };//收尾
    const int ARRAY_SIZE=3;
    SportCar a[ARRAY_SIZE]={
      {"Ferrari", "F8 Tributo",211 },
      {"Lamborghini","Huracan EVO",202},
      {"Porche","911 GT3",197}
    };
    for(int i=0;i<ARRAY_SIZE;i++){
      cout << a[i].brand << " "<< a[i].model << " " << a[i].topSpeed <<endl;
    }
     
    return 0;
}
Output:

Ferrari F8 Tributo 211
Lamborghini Huracan EVO 202
Porche 911 GT3 197
```

### 練習算出這三台⾞的平均速度

## **static_cast 轉型寫法**

static_cast 轉型的寫法如下，

| 1 | static_cast<type-id>(expression) |
| --- | --- |

上述的例子使用 static_cast 轉型的寫法就會變成這樣，

| 1 | int num2 = static_cast<int>(num) |
| --- | --- |

```cpp
#include <iostream>
using namespace std;

int main() 
{
    struct SportCar{
      const char *brand;
      const char *model;
      int topSpeed;
    };//收尾
    const int ARRAY_SIZE=3;
    SportCar a[ARRAY_SIZE]={
      {"Ferrari", "F8 Tributo",211 },
      {"Lamborghini","Huracan EVO",202},
      {"Porche","911 GT3",197}
    };
    for(int i=0;i<ARRAY_SIZE;i++){
      cout << a[i].brand << " "<< a[i].model << " " << a[i].topSpeed <<endl;
    }
    int totalspeed =0;
    for (int i=0;i<ARRAY_SIZE;i++){
      totalspeed += a[i].topSpeed;
    }
     cout << static_cast<double>(totalspeed)/ARRAY_SIZE <<endl;
    return 0;
}

Output:

Ferrari F8 Tributo 211
Lamborghini Huracan EVO 202
Porche 911 GT3 197
203.333
```

### 改成指標版

```cpp
#include <iostream>
using namespace std;

int main() 
{
    struct SportCar{
      const char *brand;
      const char *model;
      int topSpeed;
    };//收尾
    const int ARRAY_SIZE=3;
    SportCar a[ARRAY_SIZE]={
      {"Ferrari", "F8 Tributo",211 },
      {"Lamborghini","Huracan EVO",202},
      {"Porche","911 GT3",197}
    };
    for(int i=0;i<ARRAY_SIZE;i++){
      cout << a[i].brand << " "<< a[i].model << " " << a[i].topSpeed <<endl;
    }
    int totalspeed =0;
    SportCar *ptr =a;
    for (int i=0;i<ARRAY_SIZE;i++){
      totalspeed += ptr->topSpeed;
      ptr++;
    }
     cout << static_cast<double>(totalspeed)/ARRAY_SIZE <<endl;
    return 0;
}

Output:

Ferrari F8 Tributo 211
Lamborghini Huracan EVO 202
Porche 911 GT3 197
203.333

```

### ⼩專案

華納威秀 電影院座位預定系統
seat → struct → int seatNumber, bool isReserved
初始化
印出⽬前電影座位狀況
makeReserve(Seat* array, int seatNumber)
萬⼀已預訂回結果
失敗讓重新預定