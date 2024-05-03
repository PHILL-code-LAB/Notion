# (Data encapsulation & Constructor) -Paul C++ course week 18

Owner: C.L. Liu
Last edited time: September 6, 2023 4:47 AM

[Phill-CPP-0705.pdf]((Data%20encapsulation%20&%20Constructor)%20-Paul%20C++%20cours%20113c96fbd2d5450d9ebe5b59567673a9/Phill-CPP-0705.pdf)

[https://youtu.be/yFs0WQZ6YpQ](https://youtu.be/yFs0WQZ6YpQ) 

**public, private**

**private → friend function**

**Friend Function** 

```cpp
//OO 設計    /// Friend Function 
#include <iostream>
using namespace std;

//布丁的包裝
class Cirle {
  private : 
    double  radius =10;
    friend void read_radius (Cirle& c); // <--- friend function 需要在class 才算數
  public :
    double compute_area(double r){
      if(r>=0){
        radius = r;
      }
      cout << "Inside class ->" << radius <<endl;
      return 3.14159* radius*radius;
    }
};
                  
void read_radius(Cirle& c ){  // <---- frined function   不能寫在class 裡面
  cout << "I am friend access private member ->" << c.radius <<endl;
}
int main() 
{
    Cirle obj;
    cout << obj.compute_area(100) <<endl;
    read_radius(obj);  //<<--friend
    return 0;
}

Output:

Inside class ->100
31415.9
I am friend access private member ->100

```

**Data encapsulation (封裝)**

```cpp
Data encapsulation 
控管權限

#include <iostream>
using namespace std;

class Person {
  
  public : 
    int id;
    string name;
    void showName(){
      cout << "my name is " << name <<endl;  << structure  
    }
    void printName();   // << 不要做在這裡,是因為Class 通常很龐大 ,
												//	通常把class 的宣告放在head file裡面 
    void changeName(string newName);  // 傳遞參數
    
};
void Person::printName(){  // << 在這裡implement
  cout << "my name printName -->" << name <<endl;
}

void Person::changeName(string newName){ // implement //傳參數
  name =newName;
  cout <<"change successfully" <<endl;
}

int main() 
{
    Person p1;
    p1.name="Phill";
    p1.changeName("Phill Liu");
    p1.printName();
    return 0;
}
Output:

change successfully
my name printName -->Phill Liu
```

## Constructor

用**Constructor 改寫 (35:00)**

<aside>
💡 Constructor
#include <iostream>
using namespace std;
class Person{
public:
int id;
string name;
void showName(){
cout << "my name is " << name <<endl;
}
Person(string initName, int initID){ **//constructor , initalization  沒有return 值**
name = initName;
id = initID;
}
void printName(); //不要做在這裡
void changeName(string newName);
};
//implement
void Person::printName(){
cout << "my name printName -> "<< name <<endl;
cout << "id=" << id <<endl;
}
void Person::changeName(string newName){
name = newName;
 
}
int main()
{
Person p1("Phill123", 1);                                                                                                                 //第一開始觸發時會填的值 , 之後如果要修改值 就如p2 , p3 的 設定
Person p2("Phill", 2);
Person p3("Phill Liu", 3);
//p1.changeName("Phill Liu");
p2.printName();
p3.printName();
return 0;
}

</aside>

```cpp
/*練習
Car 類別
brand, model, year
constructor
(Tesla model-S 2022), (BMW, X5, 1999) */

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

```cpp
#include <iostream>
using namespace std;

class Person {
  
  public : 
    int id;
    string name;
    void showName(){
      cout << "my name is " << name <<endl;
    }
    void printName();
};
void Person::printName(){
  cout << "my name printName -->" << name <<endl;
}

int main() 
{
    Person p1;
    p1.name="Phill";
    p1.showName();
    p1.printName();
    return 0;
}

Output:

my name is Phill
my name printName -->Phill
```

```cpp
#include <iostream>
using namespace std;

class Person {
  
  public : 
    int id;
    string name;
    void showName(){
      cout << "my name is " << name <<endl;
    }
    
    Person(string initName, int initID){
      name =initName;
      id = initID;
    }
    
    
    void printName();
    void changeName(string newName);
    
};
void Person::printName(){
  cout << "my name printName -->" << name <<endl;
  cout << "id=" << id <<endl;
}

void Person::changeName(string newName){
  name =newName;
  cout <<"change successfully" <<endl;
}

int main() 
{
    Person p1("Phill123",1); //initial
    Person p2("Phill",2);
    Person p3("Phill.Liu",3);
    
    p2.printName();
    p3.printName();
    return 0;
}

Output:

my name printName -->Phill
id=2
my name printName -->Phill.Liu
id=3
```