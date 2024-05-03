# Paul C++ Course Week 5

Owner: C.L. Liu
Last edited time: May 23, 2023 10:04 AM

指標是一種變數

C++ *靠近宣告的型態(int ,string ) 

C      *靠近變數

單一字串指標要用加上& . array 指標就不能加上& 

[https://youtu.be/ZG_Jxifmih8](https://youtu.be/ZG_Jxifmih8) 

[Phill-CPP5.pdf](Paul%20C++%20Course%20Week%205%204e8da5345ed24f33aeec8f4b7562e44e/Phill-CPP5.pdf)

```jsx
#include <iostream>
using namespace std;

int main() 
{
    string phill = "advantech";
    string* ptr_phill=&phill;
    cout << &phill <<endl;   <----0x7ffc91e3b420 
    cout << ptr_phill <<endl; <-----0x7ffc91e3b420  
    
    cout << *ptr_phill <<endl; <---advantech
    return 0;

```

```jsx
#include <iostream>
using namespace std;
int main()
{
//char a[]="Phill is working for Advantech";
int a[]={10,100,1000};
//cout << a[0]<< a[4] <<endl; //陣列 index 來取值
printf("%p\n", a);//陣列的名字本⾝就是 address <----0x7ffd04cd09dc
//char *ptr_a = a;
int *ptr_a =a;
printf("%p\n", ptr_a); <--- 0x7ffc65d709cc
printf("%d\n", *ptr_a); <--10
printf("%d\n", *(ptr_a+1)); <--100
printf("%d\n", *(ptr_a+2)); <--1000

return 0;
}

```

```jsx
#include <iostream>
#include <cstring>
using namespace std;
int main()
{
char abc[]="Phill is good!"; //"xyz"
char *start=abc;
char *end=abc+strlen(abc)-1;
while(start < end){  // 雙指標 
char tmp = *start;
*start = *end;
*end = tmp;
++start;   //指標交錯
--end;     //指標交錯
}
cout<< abc <<end;
return 0;
}
```

- **%d**：顯示整數(十進位，d 是 decimal 的意思)
- **%o**：顯示整數(八進位，octal)
- **%x**：顯示整數(十六進位，heximal)
- **%c**：顯示字元
- **%f**：顯示浮點數
- **%e**：顯示浮點數(以科學記號方式表示)
- **%lld**：顯示長整數
- **%s**：顯示字串
- **%%**：顯示一個 **%** 符號

下面這個例子示範了如何顯示字元、整數、浮點數，以及一個整數的八進位和十六進位如何表示。

```
#include <stdio.h>
int main(){
	int a=23;
	float b=9.2;
	char c='A';
	printf("%d\n", a);
	printf("%o\n", a);
	printf("%x\n", a);
	printf("%f\n", b);
	printf("%c\n", c);
	return 0;
}

```

輸出結果：

```
23
27
17
9.2
C
```