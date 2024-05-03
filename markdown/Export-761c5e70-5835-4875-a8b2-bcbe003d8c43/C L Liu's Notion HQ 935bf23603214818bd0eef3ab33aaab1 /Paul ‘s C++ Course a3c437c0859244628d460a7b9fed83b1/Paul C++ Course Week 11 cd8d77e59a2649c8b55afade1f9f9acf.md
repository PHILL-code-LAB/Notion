# Paul C++ Course Week 11

Owner: C.L. Liu
Last edited time: January 3, 2024 7:30 PM

[Phill-CPP-0517.pdf](Paul%20C++%20Course%20Week%2011%20cd8d77e59a2649c8b55afade1f9f9acf/Phill-CPP-0517.pdf)

[https://youtu.be/6aagl9aqgEk](https://youtu.be/6aagl9aqgEk)

![Untitled](Paul%20C++%20Course%20Week%2011%20cd8d77e59a2649c8b55afade1f9f9acf/Untitled.png)

```cpp
#include <iostream> 
#include <string>
#include <map>
#include <cmath>
using namespace std; 

int trans_rome_to_int(string s ){
  
  int sum =0;
  map<char ,int > rome_map={{'I',1},{'V',5},{'X',10},{'L',50},{'C',100},{'D',500},{'M',1000}};
  
  for(int i=0;i<s.size();i++){
   if( i<s.size()-1 && rome_map[s[i]] < rome_map[s[i+1]]){
   sum=sum-rome_map[s[i]];  
   }else{
     sum=sum+rome_map[s[i]];
   }
   //cout <<sum<<endl;
  }
  return sum;
}

string trans_int_to_rome(int num){
  string rome=" ";
  string symbol[]={"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
  int  values[]={1000,900,500,400,100,90,50,40,10,9,5,4,1}; //代幣法
  for(int i=0;num>0;i++){
    while(num>=values[i]){
    num=num-values[i];
    rome=rome+symbol[i];
    }
  }  
  return rome;
}

int main() 
{
  
    string rome_int1,rome_int2;
    while(cin >> rome_int1 >>rome_int2){
      int int_num1= trans_rome_to_int(rome_int1);
      int int_num2= trans_rome_to_int(rome_int2);
      
      cout << int_num1 <<endl;
      cout << int_num2 <<endl;
      int diff=abs(int_num1-int_num2);
      cout << diff <<endl;
      if(diff==0 ){
        cout << "Zero" <<endl;
       }
      else{
        string rome_diff= trans_int_to_rome(diff);
        cout << rome_diff;
      }
    }
    return 0;
}
```