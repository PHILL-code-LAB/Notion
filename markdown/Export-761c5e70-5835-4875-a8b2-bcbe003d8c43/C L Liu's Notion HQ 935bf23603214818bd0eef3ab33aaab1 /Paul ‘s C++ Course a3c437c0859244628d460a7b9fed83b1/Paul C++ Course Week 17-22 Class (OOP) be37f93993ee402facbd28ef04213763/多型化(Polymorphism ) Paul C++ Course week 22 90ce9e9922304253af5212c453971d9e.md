# 多型化(Polymorphism )                            Paul C++ Course week 22

Owner: C.L. Liu
Last edited time: August 17, 2023 3:46 AM

[https://youtu.be/Vm3JjsSieNM](https://youtu.be/Vm3JjsSieNM)

[Phill-CPP-0816.pdf](%E5%A4%9A%E5%9E%8B%E5%8C%96(Polymorphism%20)%20Paul%20C++%20Course%20week%2022%2090ce9e9922304253af5212c453971d9e/Phill-CPP-0816.pdf)

Polymorphism 多型化
   繼承: 另外⼀個類別 屬性⽅法 → 有點像
    實作: 兄弟們不同的實作, methods 名稱相同, behavior完全不同

```cpp
#include <iostream>
using namespace std;

class Person{
  public:
  void run(){
    cout << " I can run " << endl;
  }
  
};

class Salesman : public Person{
  public: 
    void run(){ //overriding 
      cout << "I can visit customer quickly" << endl;
    }
};

class Superman : public Person {
  public: 
    void run(){
      cout << " I can run to fly very FAST!!!" << endl;
    }
};

int main() 
{
    Person p1 ;
    Superman p2;
    Salesman p3;
    
    p1.run();
    p2.run();
    p3.run();
    return 0;
}

Output:

I can run 
I can run to fly very FAST!!!
I can visit customer quickly
```

充分來使⽤ virtual

宣告⼀個 method 虛擬 → 衍⽣class 可以完全覆蓋跟重新定義 → base class 在宣
告時 明明⽩⽩定義⾃⼰將來要被覆蓋掉
運⽤共同相似性, 可以定義相同的 pointer 來裝盛, 使⽤共同的 dereference 來call

```cpp
#include <iostream>
using namespace std;

class Person{
  public:
    virtual void run(){ //設成 virtual function, 實現 polymorphism 
    cout << " I can run " << endl;
  }
  
};

class Salesman : public Person{
  public: 
    void run() override { //overriding 
      cout << "I can visit customer quickly" << endl;
    }
};

class Superman : public Person {
  public: 
    void run() override{
      cout << " I can run to fly very FAST!!!" << endl;
    }
};

int main() 
{
    Person* persons[3];
    
    persons[0]=new Person();// new -> 動態產生 //address 裝進 person [0]
    persons[1]=new Salesman();
    persons[2]=new Superman();

    for (int i=0;i<3;i++){
      persons[i] -> run(); //多型化的用法
      delete persons[i];
    }
    return 0;
}

Output:

 I can run 
 I can visit customer quickly
 I can run to fly very FAST!!!
```

```cpp
//example 
// Shape 形狀 (draw(),move().... OOA ) 
-> triangle , circle , square 
 -> Shape* things[]
->for things->draw(), thing -> move() -> 一個形狀 多種不同的行為 polymorphism

```

![Untitled](../Paul%20C++%20Course%20Week%2022%20Computer%20Secience%20Computer%20ee957950d03740ddb5ad7cc277b88874/Untitled.png)

```cpp
------- 進入下一個階段 Computer Secience  離開OOP
Hw: shap 形狀 
```

Computer Secience

Computer —> Efficiency 

評估

→ 時間用了多少(~response time) 

→ 空間用了多少(~memory usage) 

→ 耗能

評估方法-

定義 :甚麼是問題 

描述一個問題 : 定義一個問題 有甚麼樣的參數 (輸入) , 輸入範圍 (參數數值) ,參數之間的關聯性

問題的解: 正確答案(輸出) , 需要滿足條件(限制時間的條件, 符合最佳化的目標 ,最佳化的限制, 花的代價最少) 

產生問題實際的例子: 給一到多組的參數→ 一到多組的正確解; →測資

→ 用演算法去解決問題 

→ 評估演算法的複雜度