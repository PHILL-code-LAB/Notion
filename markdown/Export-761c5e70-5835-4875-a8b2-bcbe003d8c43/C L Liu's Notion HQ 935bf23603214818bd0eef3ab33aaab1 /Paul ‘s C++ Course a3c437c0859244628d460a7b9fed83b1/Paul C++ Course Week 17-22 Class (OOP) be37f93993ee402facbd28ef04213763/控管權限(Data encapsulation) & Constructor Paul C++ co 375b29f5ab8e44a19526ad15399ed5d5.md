# 控管權限(Data encapsulation) & Constructor                                                  Paul C++ course week 19

Owner: C.L. Liu
Last edited time: September 12, 2023 3:23 AM

[Phill-CPP-0712.pdf](%E6%8E%A7%E7%AE%A1%E6%AC%8A%E9%99%90(Data%20encapsulation)%20&%20Constructor%20Paul%20C++%20co%20375b29f5ab8e44a19526ad15399ed5d5/Phill-CPP-0712.pdf)

[https://youtu.be/Ez6vr90iHvQ](https://youtu.be/Ez6vr90iHvQ)

```cpp
#include <iostream>
using namespace std;

class Cirle{
  private : 
    double radius=0;
    friend void read_radious(Cirle& c);
  public: 
    double compute_area(double r){
      if(r>=0){
        radius=r;
      }
      cout << "Inside class->" << radius <<endl;
      return 3.14159*radius*radius;
    }
};

void read_radious(Cirle& c){
  cout << "I am friend access private member->" << c.radius<<endl;
}

int main() 
{
    Cirle obj;
    cout << obj.compute_area(100) <<endl;
    read_radious(obj);
    return 0;
}

Output:

Inside class->100
31415.9
I am friend access private member->100
```

```cpp
Data encapsulation
控管權限
實作 member functions

#include <iostream>
using namespace std;

class Person{
  public:
    int id;
    string name;
    void showName(){
      cout << "my name is " << name <<endl;
    }
    void printName();
};

//implement
void Person::printName(){
  cout << "my name printName--> " << name <<endl;
}

int main() 
{
    Person p1;
    p1.name ="phill";
    p1.showName();
    p1.printName();
    return 0;
}

Output:

my name is phill
my name printName--> phill
```

```cpp
#include <iostream>
using namespace std;

class Person{
  public: 
    int id;
    string name;
    void showName(){
      cout << "my name is " << name << endl;
    }
    
    void printName(); //不要做在這裡
    void changeName(string newName);
};

//implement 
void Person::printName(){
  cout << "my name printName ->" << name <<endl;
}
void Person::changeName(string newName){
  name = newName;
}

int main() 
{
    Person p1;
    p1.name ="Phill";
    p1.changeName("Phill Liu");
    p1.printName();
    return 0;
}

Output:

my name printName ->Phill Liu
```

## **Constructor**

1. 加一個 與 Class 同名的 person  (constructor )  , Constructor 沒有return 值
2. 在Constructor 中做Initlization 
3. 並在 main 中直接給值 , 可產生很多instance , 

```cpp
#include <iostream>
using namespace std;

class Person{
  public: 
    int id;
    string name;
    void showName(){
      cout << "my name is " << name << endl;
    }
    
    Person(string initName , int initID){
      //constructor , Initlization
      name = initName;
      id = initID;
    }
    
    
    void printName(); //不要做在這裡
    void changeName(string newName);
};

//implement 
void Person::printName(){
  cout << "my name printName ->" << name <<endl;
}
void Person::changeName(string newName){
  name = newName;
}

int main() 
{
    Person p1("Phill1234",1);
    Person p2("Phill",2);
    Person p3("Phill Liu",3);
    p2.printName();
    p2.printName();
    return 0;
}

Output:

my name printName ->Phill
my name printName ->Phill
```

```cpp
練習
Car 類別
brand, model, year
constructor
(Tesla model-S 2022), (BMW, X5, 1999)

#include <iostream>
using namespace std;
class Car {
	public:
		string brand;
		string model;
		int year;
		void showInfo(){
				cout << "Car Infomation -->" << brand <<" " << model <<" " << year <<endl;
}
	Car(string initbrand , string initmodel, int inityear){
		brand=initbrand;
		model=initmodel;
		year=inityear;
	}
};
int main()
{
	Car p1("xxxx","xxxx",123);
	Car p2("Tesla","model-S",2022);
	Car p3("BMW","X5",1999);
  p2.showInfo();
  p3.showInfo();
	return 0;
}

Output:

Car Infomation -->Tesla model-S 2022
Car Infomation -->BMW X5 1999
```

Assignment
電影院座位系統
OO ⾓度去設計
class → Seat → member (data, functions)
思考⼀下跟 原先的設計有何不同 優缺點

→ **Person  可再增加 某個人 去預定位置 , 刪除位置. 等功能 === HW**

![Untitled](%E6%8E%A7%E7%AE%A1%E6%AC%8A%E9%99%90(Data%20encapsulation)%20&%20Constructor%20Paul%20C++%20co%20375b29f5ab8e44a19526ad15399ed5d5/Untitled.png)

```cpp
Sampel 1 : 一維 電影座位預約

#include <iostream>
using namespace std;

class Seat {
  private:
    int row;
    int column;
    bool isReserved;
    
  public:
    Seat(int r,int c ){
      row=r;
      column =c;
      isReserved=false;
    }
  void reserve(){
    isReserved=true;
  }
  void cancel(){
    isReserved=false;
  }
  bool isReservedxxx(){
    return isReserved;
  }
  int getRow(){
    return row;
  }
  int getColumn(){
    return column;
  }
};

// Seat::Seat(int r,int c){
//   row=r;
//   column=c;
//   isReserved=false;
// }

int main() 
{
   Seat s(1,1);
    
    cout << "Row :" << s.getRow()<<", Column:" <<s.getColumn() <<endl;
    cout << "reserved:" << s.isReservedxxx() <<endl;
    s.reserve();
     cout << "reserved:" << s.isReservedxxx() <<endl;
    s.cancel();
     cout << "reserved:" << s.isReservedxxx() <<endl;
     
    return 0;
}

Output:

Row :1, Column:1
reserved:0
reserved:1
reserved:0

```

```cpp
Sample 2 : 3 維 電影座位預約

#include <iostream>
using namespace std;

class Seat {
  private:
    int row;
    int column;
    bool isReserved;
    
  public:
    Seat(int r,int c ){
      row=r;
      column =c;
      isReserved=false;
    }
  void reserve(){
    isReserved=true;
  }
  void cancel(){
    isReserved=false;
  }
  bool isReservedxxx(){
    return isReserved;
  }
  int getRow(){
    return row;
  }
  int getColumn(){
    return column;
  }
};

// Seat::Seat(int r, int c){   // 也可以放到外面來
//   row=r;
//   column= c;
//   isReserved=false;
// } 

int main() 
{
  
   //靜態
   Seat s[3]={
     Seat(1,1),
     Seat(2,2),
     Seat(3,3)
   };
   //動態
   Seat* s[9][9]; 
   for(int i=1; i<10; i++){
    for(int j=1; j<10; j++){
       s[i][j]=new Seat(i,j);
    }
   }

    cout << "Row :" << s[0][8]->getRow()<<", Column:" <<s[0][8]->getColumn() <<endl;
   // cout << "reserved:" << s[0].isReservedxxx() <<endl;
   // s[0].reserve();
   //  cout << "reserved:" << s[0].isReservedxxx() <<endl;
    // s.cancel();
    // cout << "reserved:" << s[0].isReservedxxx() <<endl;
     
    return 0;
}

→ **Person  可再增加 某個人 去預定位置 , 刪除位置. 等功能 === HW**
```

Setter → reserve(), cancel() → public function → control private data
Getter → isReserved(), getRow() → public function → retrieve(取回) private data

Inheritance 繼承
abstraction 階層化 → inheritance → efficient → 軟體⼯程
Window → Warning Window
→ Yes, no window
→ Fatal window
⽗類別 → base class
⼦類別 → derived class
primitive object → 空