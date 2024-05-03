# 特例-多重繼承問題 & 鑽石繼承 (菱形繼承)  ,  ambiguous  issue  —解法 & 虛擬繼承(virtual inheritance)                            Paul C++ Course Week 21

Owner: C.L. Liu
Last edited time: August 17, 2023 3:51 AM

[Phill-CPP-0809.pdf](%E7%89%B9%E4%BE%8B-%E5%A4%9A%E9%87%8D%E7%B9%BC%E6%89%BF%E5%95%8F%E9%A1%8C%20&%20%E9%91%BD%E7%9F%B3%E7%B9%BC%E6%89%BF%20(%E8%8F%B1%E5%BD%A2%E7%B9%BC%E6%89%BF)%20,%20ambiguous%20issue%20%E2%80%94%E8%A7%A3%E6%B3%95%20&%20%E8%99%9B%E6%93%AC%205113dbd7825141a3a92d8c48a1f75a86/Phill-CPP-0809.pdf)

[https://www.youtube.com/watch?v=D6THOU4hsiA&list=PLcX_scbPX1dFaCCTDIBJM_UUEXj6vhCyU&index=35](https://www.youtube.com/watch?v=D6THOU4hsiA&list=PLcX_scbPX1dFaCCTDIBJM_UUEXj6vhCyU&index=35)

多重繼承 multiple inheritance

```cpp
Aquatic // 水生物
Ambulatory // 陸生生物

#include <iostream>
using namespace std;

class Aquatic{
  public : 
  void swim(){
    cout << " I can swim" <<endl;
  }
};
class Ambulatory {
  public:
    void walk(){
      cout << "I can work" <<endl;
    }
};

class Penguin:public Aquatic , public Ambulatory{
  
};

int main() 
{
   Penguin p;
   p.swim();
   p.walk();
    return 0;
}

Output:

I can swim
I can work
```

1, 多重繼承問題 : 同名時 我要繼承誰? ambiguous ——解法

```cpp
#include <iostream>
using namespace std;

class Base1{
  public:
    void abc(){
      cout << " I am from BASE1" <<endl;
    }
};

class Base2{
   public:
      void abc(){
      cout << " I am from BASE2" <<endl;
    }
};

class Derived:public Base1,public Base2{
    public:
      void abcFromBASE1(){
        Base1::abc();
      }
      void abcFromBASE2(){
        Base2::abc();
      }
};

int main() 
{
    Derived d;
    d.abcFromBASE1();
    return 0;
}
```

1. 鑽石繼承 (菱形繼承)  ,  `ambiguous`  issue 

class A(aaa) → class B(aaa())→class D 

class A(aaa) → class C(aaa())→class D

```cpp
#include <iostream>
using namespace std;

class A{
  public:
    void aaa(){
      cout << "I am aaa()" <<endl;
    }
};
/
class B: public A{
  
};
class C: public A {
  
};

class D: public B ,public C{
  
};

int main() 
{
    D d;
    d.aaa();
    return 0;
}
```

虛擬繼承(virtual inheritance) 

```cpp
#include <iostream>
using namespace std;

class A{
  public:
    void aaa(){
      cout << "I am aaa()" <<endl;
    }
};

class B: virtual public A{
  
};
class C: virtual public A {
  
};

class D: public B ,public C{
  
};

int main() 
{
    D d;
    d.aaa();
    return 0;
}

Output:

I am aaa()
```

練習: 

```cpp
**繼承
	Person
  private → name
	public → getName
	Person(name) 
HW:
Pitcher 投⼿
void doPitch() → I can pitch
Player 打擊
void doBat() → I can hit
Couch 教練
void doSpeak() → I can speak**

#include <iostream>
using namespace std;

class Person{
  private:
    string Pname;
  public:
   
   Person(string  name){
     Pname=name;
   }
   string getName(){
      
      return Pname;
    }
};

class Pitcher {
  public:
  void doPitch(){
  cout << "I can Pitch" <<endl;
  }
};

class Player{
  public:
  void doBat(){
    cout << "I can Hit" <<endl;
  }
};

class Couch{
  public:
  void doSpeak(){
    cout << "I can speak!!" <<endl;
  }
};

int main() 
{
    Person p("Shohei Ohtani");
    cout << p.getName() <<endl;
    Couch C ;
    C.doSpeak();
    Player pr;
    pr.doBat();
    Pitcher pt;
    pt.doPitch();
    return 0;
}
Output:
Shohei Ohtani
I can speak!!
I can Hit
I can Pitch
```

多重繼承

```cpp
//**HW : 既是投⼿⼜是打擊 → class twoway_player**
#include <iostream>
using namespace std;

class Person{
private:
    string Pname;
  public:
   
   Person(string  name){
     Pname=name;
   }
   string getName(){
      
      return Pname;
    }
 
};

class Pitcher: virtual public Person{
    public:
     void doPitch(){
      cout << "I can Pitch" <<endl;
  }
};
class Player: virtual public Person{
      public:
      void doBat(){
        cout << "I can Hit" <<endl;
      }
};

class Couch{
   public:
    void doSpeak(){
    cout << "I can speak!!" <<endl;
    }
};

class twowayplayer:public Pitcher ,public Player {
    public:
    void doTwoway(){
      cout << "I can Pitch & Hit"<<endl;
    }
};

int main() 
{   
    Person p("Shohei Ohtani");
    cout << p.getName() <<endl;
    //wowayplayer d;
    //d.doTwoway();
    
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

class Person{
private:
    string P_name;
    int P_rbi;
    int P_hitsafes;
    double P_avg;
    double P_era;
  public:
   
   Person(string  name  ,int hitsafes,int rbi, double avg , double era ){
     P_name=name;
     P_hitsafes=hitsafes;
     P_rbi=rbi;
     P_avg = avg;
     P_era = era;
   }
   
    void showinfo();
    void showera();
   Person(const Person&) = delete;
};

void Person::showinfo(){
      cout << "---------本場球員數據----------"<< endl;
      cout << "打擊者:--->" << P_name <<endl;
      cout <<"安打:-->"  <<P_hitsafes << endl;
      cout <<"打點:-->" << P_rbi << endl;
      cout <<"打擊率:--->" <<P_avg << endl;
      cout <<"防禦率:--->" <<P_era <<endl;
    }
void Person::showera(){
      
      cout <<"防禦率:--->" <<P_era <<endl;
    }

class Pitcher:virtual Person{
    public:
     void doPitch(){
      cout << "I can Pitch" <<endl;
  }
};
class Player:virtual Person{
      public:
      void doBat(){
        cout << "I can Hit" <<endl;
      }
};

class twowayplayer:public Pitcher ,public Player {
    public:
   
    void doTwoway(){
      cout << "I can Pitch & Hit"<<endl;
      }
};

int main() 
{   
    const int ARRAY_SIZE =3;
     
    Person p[ARRAY_SIZE]={{"Shohei Ohtani",663,426,0.274 ,2.90},
                         {"J.D. Martinez" , 1610 , 975,0.286 ,0},
                         {"Freddie Freeman" ,1187 , 1124,0.301,0}
};
   
      for(int i=0;i<ARRAY_SIZE;++i){
      cout <<"Information :--> " <<endl;
      p[i].showinfo();
     
      cout << "-------------" << endl;
    }
    
    // twowayplayer d;
    // d.doTwoway();
    
    return 0;
}
```