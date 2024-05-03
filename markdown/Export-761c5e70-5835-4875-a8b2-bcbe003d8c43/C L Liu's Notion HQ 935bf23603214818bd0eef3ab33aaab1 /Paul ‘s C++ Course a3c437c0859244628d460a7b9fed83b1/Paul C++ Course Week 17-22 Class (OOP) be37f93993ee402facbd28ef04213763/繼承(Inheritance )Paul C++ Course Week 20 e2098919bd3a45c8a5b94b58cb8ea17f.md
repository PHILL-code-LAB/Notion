# 繼承(Inheritance )Paul C++ Course Week 20

Owner: C.L. Liu
Last edited time: August 17, 2023 3:43 AM

[Phill-CPP-0802.pdf](%E7%B9%BC%E6%89%BF(Inheritance%20)Paul%20C++%20Course%20Week%2020%20e2098919bd3a45c8a5b94b58cb8ea17f/Phill-CPP-0802.pdf)

 [https://youtu.be/gmPaF7QCdvs](https://youtu.be/gmPaF7QCdvs)

```cpp
#include <iostream>
using namespace std;

class Vehicle{
  public:
    string name="vehicle"; 
    void launch(){
      cout << "start your enginel"<<endl;
    }
};

class Car : public Vehicle{
  public:
    string brand ="Tesla";
    string model ="Model-S";
};

int main() 
{
    
    Car myCar;
    myCar.launch();
    cout << "my car is " << myCar.brand <<" , " << myCar.model <<endl;
    
    return 0;
}
```

```cpp

#include <iostream>
using namespace std;

class Vehicle{
  public:
    string name="vehicle"; 
    void launch(){
      cout << "start your enginel"<<endl;
    }
};

class Car : public Vehicle{
  public:
    string brand ="Tesla";
    string model ="Model-S";
};

class Rocket :public Vehicle{
  public:
    string brand ="xSpace";
    string model = "Falcon-9";
  
};

class e_motorcycle :public Vehicle{
  public: 
    string brand ="Gogoro";
    string model ="Viva Mix";
};

int main() 
{
    
    Car myCar;
    e_motorcycle myemoto;
    myCar.launch();
    myemoto.launch();
    cout << "my car is " << myCar.brand <<" , " << myCar.model <<endl;
    cout << "my myemoto is "<< myemoto.brand<< " ,  " << myemoto.model <<endl; 
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

class Person{
  public:
  int bouns =100;
  protected:
    int salary=100;
  private:
    int deposit=100;
};

class Programer: public Person{
  public:
    void setSalary(int s){
      salary =s;
      
    }
    int getSalary(){
      return salary;
    }
};

int main() 
{
  
    Programer p;
    p.bouns=1000;
    cout << "bouns is " << p.bouns<<endl;
    p.setSalary(1000);
    cout << "salary is " << p.getSalary()<<endl;
  
    return 0;
}
```

Private 在父子之前不能share的.

Protected  在父子之前是可以share的