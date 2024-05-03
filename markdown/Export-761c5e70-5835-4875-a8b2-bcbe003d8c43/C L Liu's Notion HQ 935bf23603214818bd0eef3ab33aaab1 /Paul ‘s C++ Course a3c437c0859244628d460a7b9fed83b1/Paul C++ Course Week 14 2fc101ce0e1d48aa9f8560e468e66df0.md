# Paul C++ Course Week 14

Owner: C.L. Liu
Last edited time: January 3, 2024 7:30 PM

[https://youtu.be/3I--Hc4RMA8](https://youtu.be/3I--Hc4RMA8) 

[Phill-CPP-0607.pdf](Paul%20C++%20Course%20Week%2014%202fc101ce0e1d48aa9f8560e468e66df0/Phill-CPP-0607.pdf)

```cpp
檢查三⾓形 → a,b,c
不成三⾓形 a+b ≤ c → 0
鈍⾓三⾓形 → 1
直⾓三⾓形 → 2
銳⾓三⾓形 → 3
→ isTriangle(a,b,c)
提示：若a、b、c為三個線段的邊長，且c為最大值，則

　　若 a+b ≦ c　　　　　，三線段無法構成三角形

　　若 a×a+b×b ＜ c×c　　，三線段構成鈍角三角形(Obtuse triangle)

　　若 a×a+b×b ＝ c×c　　，,三線段構成直角三角形(Right triangle)

　　若 a×a+b×b ＞ c×c　　，三線段構成銳角三角形(Acute triangle)

#include <iostream>
using namespace std;

int isTriangle(int a,int b,int c){
  
 
  if(a+b<=c){
    cout << "No"; 
  }else if(a*a +b*b < c*c){
      cout << "Obtuse triangle";
    }else if(a*a+b*b==c*c){
      cout << "Right triangle";
    }else if (a*a +b*b > c*c){
      cout << "Acute triangle";
    }
  
  
} 

int main() 
{
  int x,y,z;
  cin >> x >> y >> z;
  isTriangle(x,y,z);
    
    return 0;
}
```

```cpp
請做⼀個 produceTriangle() 印出 邊⻑⼩於⼀百,
的所有直⾓三⾓形
ex: 3,4,5
8,15,17
….
→ 邊⻑⼩於 100
→ 3,4,5 x 4,3,5

#include <iostream>
using namespace std;

void produceTriangle(){
  for(int a=1;a<100;a++){
    for(int b=a;b<100;b++){
      for(int c=b;c<100;c++){
        if(a*a+b*b==c*c) {
          cout << a <<","<<b <<"," <<c <<endl;
        }
      }
    }
  }
  
}

int main() 
{
   produceTriangle();  
    return 0;
}
```

```cpp
列出 1000 以內的質數

#include <iostream>
using namespace std;

int main()
{
  int i,k;
    for(i=2;i<=1000;i++){
      int p=1;
      for (k=2;k<i;k++){
        if(i%k==0){
              p=0;
        }
      }
        if(p==1){
          cout <<" "<<i;
      }
  }
    return 0;
}
Output:
 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97 101 103 107 109 113 127 131 137 139 149 151 157 163 167 173 179 181 191 193 197 199 211 223 227 229 233 239 241 251 257 263 269 271 277 281 283 293 307 311 313 317 331 337 347 349 353 359 367 373 379 383 389 397 401 409 419 421 431 433 439 443 449 457 461 463 467 479 487 491 499 503 509 521 523 541 547 557 563 569 571 577 587 593 599 601 607 613 617 619 631 641 643 647 653 659 661 673 677 683 691 701 709 719 727 733 739 743 751 757 761 769 773 787 797 809 811 821 823 827 829 839 853 857 859 863 877 881 883 887 907 911 919 929 937 941 947 953 967 971 977 983 991 997
```

```cpp
輸⼊⼀個正整數, 印出他有幾位數
9487
輸出 4

#include <iostream>
using namespace std;

int main() 
{
    int a =9487;
    int cnt=0;
    while(a>0){
      a=a/10;
      cnt++;
      
    }
    cout << cnt;
    return 0;
}
```