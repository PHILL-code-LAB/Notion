# Paul C++ Course Week 8

Owner: C.L. Liu
Last edited time: May 23, 2023 10:06 AM

[Phill-CPP-0419.pdf](Paul%20C++%20Course%20Week%208%202704276b929a4bccb0f5ba9b9d0ea57b/Phill-CPP-0419.pdf)

[https://youtu.be/0Y5qyB5if0g](https://youtu.be/0Y5qyB5if0g) 

```cpp

HW :  數入月份 = 季節

#include <iostream>
using namespace std;

int main() 
{
    int a;
    cin >> a;
    int m=(a%12)/3;
    //cout <<m;
    //因為 1 %12 取餘數 = 1    , 1/3 =0 2/3 =0 3/3=1 , 4/3 =1 ,5/3=1,6/
    // 12,1,2=0 ; 3 ,4 ,5 =1 ; 6,7,8 =2 , 9,10 11 =3 
    if (a<1 || a>12){
      cout << "N/A" <<endl;
    }else {
       switch (m){
         case 0:
         cout << "Winter" <<endl;
         break;
         case 1:
         cout << "Spring" <<endl;
         break;
         case 2:
         cout << "Summer" << endl;
         break;
         case 3:
         cout << "Fall" << endl;
       }
    }
}

```

2D array 算位置方法

![Untitled](Paul%20C++%20Course%20Week%208%202704276b929a4bccb0f5ba9b9d0ea57b/Untitled.png)

![Untitled](Paul%20C++%20Course%20Week%208%202704276b929a4bccb0f5ba9b9d0ea57b/Untitled%201.png)

```cpp
#include <iostream>
using namespace std;

void reserve_seats(int *arr1,int x,int y,int size){
 
  int *xx=arr1+(x*size+y);
  cout << *xx <<endl;   //<<<---- 2  取值
  cout << xx <<endl;    //<<<---- 0x7ffff3de4540 取位置
 }

int main() 
{
   int x=0;
   int y=0;
   int arr1[] = {2,0,0,0};
   int size = sizeof(arr1)/sizeof(arr1[0]);
   reserve_seats(arr1,x,y,size);
   
  return 0;
 
}
```

```cpp
#include <iostream>
using namespace std;
int reserve_seats(int *arr1,int x,int y,int size,int B_ticket_numbers);
/*
* Reserve_seats
* description:
  So far,Input Menu Item number and ticket numbers , it will show your booking seat list.  When you finished in first time , it will return to menu again until you selected the "[2] EXIT".
*Issue :it cannot be accumulated when you buy only one ticket repeatedly 
* arguments:
* @param arr1: int,1x1 matrix
*        nCommand : Menu Item number 
*        x : x axis of seat list 
*        y : y axis of seat list 
*        size: array size
*        ticket_numbers : ticket numbers 
*        reserve_arr1 : reserve array 
*        reserve_seats_position : reserve position 
*        B_reserve_seats_position: Buy again position
*        B_reserve_arr1: Buy again reserve arry 
*        B_ticket_numbers : Buy again ticket numbers
* return : *arr1 
*/

int reserve_seats(int *arr1,int x,int y,int size,int B_ticket_numbers){
   
  // cout << *reserve_seats_position <<endl;   //<<<---- 2  取值
  //cout << reserve_seats_position <<endl;    //<<<---- 0x7ffff3de4540 取位置
 
 for(int i=0;i<B_ticket_numbers;i++){
     int *reserve_seats_position=arr1+(x*size+i);
      if(*reserve_seats_position==0 && B_ticket_numbers<4){
        *reserve_seats_position=1;
      }  
    
 }
  cout <<endl;
  return *arr1;
} 

int  Buyagain(int *arr1, int x,int y,int size,int ticket_numbers,int B_ticket_numbers){
  
     int *B_reserve_arr1=arr1;
    ///bug 無法累加  
  for(int i=0;i<ticket_numbers+B_ticket_numbers;i++){
      
     int *B_reserve_seats_position=B_reserve_arr1+(x*size+i);
            if(*B_reserve_seats_position!=1 ){
             *B_reserve_seats_position=1;
            }
       
     }
 
 for(int j=0;j<4;j++){
  
     cout <<"\t"<<B_reserve_arr1[j];  
  }
   cout <<endl;
  
 } 
  
 
int  display_seating(int *arr1,int x, int y)
{
	
	int *reserve_arr1=arr1;

for(int j=0;j<4;j++){
  
     cout <<"\t"<<reserve_arr1[j];
     
  }
 
  cout <<endl;
 

}  

  
int main() 
{
Start:
  int x;
  int y;
  int nCommand;
  int arr1[] = {0,0,0,0};
  int size = sizeof(arr1)/sizeof(arr1[0]);
  int ticket_numbers;  //default  =1 
  cout << "Welcome CINEMA Reserve Seat System"<<endl;
  cout << "  [1] Buy ticket" << endl;
  cout << "  [2] EXIT" << endl;
  cout << "  [3] Buy again" << endl;
  cout << endl;
	cout << "  Enter your command: ";
  cin  >> nCommand;
  switch (nCommand){ 
      case 1:
        cout <<"Please input your ticket numbers: ";
        cin >> ticket_numbers;
        cout << ticket_numbers << endl;
        if(ticket_numbers>4){
          cout << "over range" <<endl;
        }
        if(ticket_numbers<=4){
          for(int i=0;i<ticket_numbers;i++){
            x=0;
            y=i;
          } 
        } 
        reserve_seats(arr1,x,y,size,ticket_numbers);
        display_seating(arr1,x,y);
        
        break;
      case 2 :
        exit(0);
        break; 
      case 3: 
        int B_ticket_numbers;
        cout <<"Please input your numbers: ";
        cin >> B_ticket_numbers;
        cout << B_ticket_numbers << endl;
                 
          Buyagain(arr1, x,y, size,ticket_numbers,B_ticket_numbers);
          
        
      default : 
        break;       
      }   
       goto Start;
  return 0;
  }
```

![Untitled](Paul%20C++%20Course%20Week%208%202704276b929a4bccb0f5ba9b9d0ea57b/Untitled%202.png)