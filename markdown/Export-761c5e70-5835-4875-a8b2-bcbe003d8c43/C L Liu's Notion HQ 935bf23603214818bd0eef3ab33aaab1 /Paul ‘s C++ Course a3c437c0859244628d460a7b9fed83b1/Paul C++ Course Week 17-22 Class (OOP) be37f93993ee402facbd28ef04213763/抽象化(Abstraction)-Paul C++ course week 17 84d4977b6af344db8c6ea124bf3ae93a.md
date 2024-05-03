# 抽象化(Abstraction)-Paul C++ course week 17

Owner: C.L. Liu
Last edited time: January 9, 2024 7:55 PM

[Phill-CPP-0628.pdf](%E6%8A%BD%E8%B1%A1%E5%8C%96(Abstraction)-Paul%20C++%20course%20week%2017%2084d4977b6af344db8c6ea124bf3ae93a/Phill-CPP-0628.pdf)

[https://youtu.be/MOHKwR5GR74](https://youtu.be/MOHKwR5GR74) 

## **class**

在程式中，物件可能屬於同一種類（擁有相同的特徵、模式），因此常常會先做出一個藍圖，再根據藍圖製造出擁有相同屬性的不同物件，這個藍圖便是 class。class 可以看成是由程式設計者定義的 datatype，由設計者自己去定義特徵，定義完成了之後，便可以像系統預設資料模式一般，自由新增相關物件。

```
class object_name {
  //特徵描述
};
```

class 中靜態的特徵稱為 data member，動態的行為稱為 member function。member function 即是由 function 轉化而來，但僅在該 class 中有意義。

class 定義完成之後，就可以開始生成物件：

```
class_name object_name;
```

其實就跟宣告變數的做法一樣，當

然也可以指定 reference、pointer 種類的變數。

## **process specification**

C++ 中有三種 process specifier：private、public 以及 protect：

```
public：公開函式，可以與外界互動，通常放 member function
private：不可從外界直接拿到相關資訊，通常用來儲存 data member
```

OO 的寫法 →C++ 

```cpp
#include <iostream>
using namespace std;

class person{ //data member
public:
  int id;
  string name;
  
  void showName(){ //method
    cout << "my name is " <<name <<endl;
  }
  
  
};

int main() 
{
    person phill;
    
    phill.name="Phill";
    phill.showName();
    
    
    return 0;
}

Output:

my name is Phill
```

```cpp

```

public

對所有⼈開放 存取權 使⽤權

跨class使⽤

```cpp
#include <iostream>
using namespace std;
class Circle{
   public:
     double radius=3; 
         double compute_region(){ 
      return radius*radius*3.14;    
 }
 }; 
 int main()  {  
   Circle o;   
       o.radius= 10;     
     cout << "radius = " << o.radius <<endl; 
    cout << "region =" << o.compute_region() << endl;  
   return 0; 
}
```

 private

```cpp
#include <iostream> 
using namespace std; 
 class Circle{   
private: 
    double radius=3;  
  public:      
  double compute_region(){
       return radius*radius*3.14;     
} 
};
  int main()  { 
    Circle o;      
    //o.radius= 10;
		return 0;
	}

```

Setter 

```cpp
#include <iostream> 
using namespace std; 
 class Circle{   
private:     
double radius=3;   
 public:   
     double compute_region(){
       return radius*radius*3.14;     
}   
  //setter 
  void setRadius(double setting){  
   radius = setting;   // 間接
}
}; 
 int main()  {
     Circle o;    
      o.setRadius(10); 
         //cout << "radius = " << o.radius <<endl;   
		  cout << "region =" << o.compute_region() << endl; 
    return 0; 
}
```

```cpp
//練習建⽴⼀個 class 
//銀⾏帳戶存錢 deposit()
//提錢 withdraw()
//查詢餘額 queryBalance()

#include <iostream>
using namespace std;

class Bank{
  
public:
  string person_name;
  int blance; // 餘額
  //存款方式
  void deposit(double amount){
    blance +=amount;
  }
  //提款方式 
  void withdraw(double amount){
    if(blance <amount){
      cout << "over blance value" <<endl;
      return;
    }
    blance-=amount;
    cout<< "withdraw successfully , Blance value is  " << blance << endl;
    
  }
// 查詢帳戶資訊方法
  void queryBlance(){
    cout << "account name " << person_name <<endl;
    cout <<"Blance is " << blance << endl;
  }
};

int main() 
{
    Bank owner;
    owner.person_name="Phill";
    owner.blance=10000;
    owner.queryBlance();
    owner.deposit(100);
    owner.withdraw(1000);
    owner.queryBlance();
    
    
    return 0;
}

Output:

account name Phill
Blance is 10000
withdraw successfully , Blance value is  9100
account name Phill
Blance is 9100
```

```cpp
HW  羽球場 book 系統

#include <iostream>
using namespace std;

class Badminton {
  
  public: 
    string person_name; 
    int venue_amount=3;
    
  void booked_venue_amount(int venue_num ){
     
    if(venue_amount <venue_num){
      cout << "venue_num is not enough" <<endl;
    } 
    venue_amount-=venue_num;
     cout<< "預約成功 " <<endl;
     cout <<"預約場地數量 :"<< venue_num << endl;
     
  }
 
  void book_info(){
    cout << "預約者姓名 : " << person_name <<endl;
   
  }
  void available_venue_amount(){

  cout << "剩餘場地數量 : " << venue_amount <<endl;
  
    if(venue_amount<0){
    cout <<"場地已滿" <<endl;
  }
  }  
 
}; 

int main() 
{
    Badminton Venue;
    Venue.person_name="Phill";
    Venue.booked_venue_amount(1);
    Venue.book_info();
    Venue.available_venue_amount();
    
    cout <<endl;
    cout <<endl;
    
    Venue.person_name="Jack";
    Venue.booked_venue_amount(2);
    Venue.book_info();
    Venue.available_venue_amount();
    return 0;
}

Output:

預約成功 
預約場地數量 :1
預約者姓名 : Phill
剩餘場地數量 : 2

預約成功 
預約場地數量 :2
預約者姓名 : Jack
剩餘場地數量 : 0
```