# Paul C++ Course Week 3

Owner: C.L. Liu
Last edited time: May 25, 2023 1:57 AM

[Phill-C3.pdf](Paul%20C++%20Course%20Week%203%202a3422b0b1284268bcc43b1b67a4e374/Phill-C3.pdf)

[https://youtu.be/rmN6Ge-5nF0](https://youtu.be/rmN6Ge-5nF0)   3-1

[https://youtu.be/-SXnB-CZAXk](https://youtu.be/-SXnB-CZAXk)    3-2

[https://youtu.be/3gXSV6B4MOE](https://youtu.be/3gXSV6B4MOE)  3-3

[https://youtu.be/nXX3R_nJiYc](https://youtu.be/nXX3R_nJiYc)       3-4

```cpp

C-style 字串
#include <iostream> 
#include <cstring> 
using namespace std; 
 int main()  { 
    const char *a="abc";  
    int length =  strlen(a);
     cout << "length=" << length;  
   return 0; }
```

```cpp
拷⾙字串#include <iostream> 
#include <cstring> 
using namespace std; 
 int main()  {  
   char arr1[]= "hello world";
     char arr2[87];   
       //string copy    
     strcpy(arr2, arr1);
     cout << arr2<< endl; 
    return 0; }

限制⻑度的拷⾙#include <iostream> 
#include <cstring>
 using namespace std; 
 int main()  {    
 char arr1[]= "hhhhhhhhhhhhhhhhhhhhhhhhhh";   
  char arr2[5];

  //string copy 
   strncpy(arr2, arr1, sizeof(arr2)-1); //安全 
   arr2[sizeof(arr2)]='\0';   
   cout << arr2<< endl; 
    return 0; }
```

sizeof vs. strlen

 sizeof c++→ not function → compiling → .exe 就已經知道⼤⼩了→ compiling time → int structure, float array → 總結構的⼤⼩

strlen 

function → runtime → char array only → 不包含 \0

```cpp
字串疊加
#include <iostream>
 #include <cstring> 
using namespace std; 
 int main()  {    
  char arr1[]= "hello";   
  char arr2[]= "world";     
  char arr3[256];       
   strcpy(arr3, arr1);  
   strcat(arr3, arr2);   
  cout << arr3 <<endl;    
 return 0; }
```

```cpp
C++ 字串
string 類別

#include <iostream>
 #include <string> 
using namespace std; 
 int main()  {   
  string my_string1="hello";   
  string my_string2=" world";      
  cout << my_string1.length(); // string method   
  cout << my_string1+my_string2;    
  return 0; }

C→ C++

#include <iostream> 
#include <string> 
#include <cstring> 
using namespace std; 
 int main()  {     //Cstyle -> C++ class 
    char char_array[]="Phill is good.";  
   string str(char_array);        
  cout << str << endl;     
 return 0; 
}

c++→C

#include <iostream>
 #include <string>
 #include <cstring>
 using namespace std; 
 int main()  {    
 string str ="Phill is good.";  
   const char* char_array= str.c_str();    
   cout << char_array << endl;    
   c// error!!    
    char_array[3]='z';   
    return 0; 
}
```

作業
C-style → function :⼤寫的string

```cpp
#include <iostream>
#include <cstring> 
using namespace std;

int main() 
{
   string str="abcd";
   
    // create a new array of chars to copy to (+1 for a null terminator)
    
    char* char_array = new char[str.length() + 1];
    char_array[str.length()]= '\0';
    
    for (int i=0;i<str.length();i++){
      char_array[i] = str[i]-32;
    }
     cout << char_array;
    
 
    return 0;
}

---------------------------------------------------------------

Output:

ABCD
```

```cpp
#include <iostream>
#include <cstring> 
using namespace std;

string cover_letter(string word){
  
  int len=word.length();
   // create a new array of chars to copy to (+1 for a null terminator)
    char* char_array = new char[len + 1];
    char_array[len]= '\0';
    for (int i=0;i<len;i++){
      char_array[i]=word[i]-32;
    }

    return(char_array);
  
} 

int main() 
{
   string str="abcd";
   string final_char_array=cover_letter(str);  
   cout << final_char_array;
 
    return 0;
}

----------------------------------------------------

Output:

ABCD
```

```cpp
//小轉大 toupper()

#include <iostream>
#include <cstring> 
using namespace std;

string cover_letter(string word){
  
  int len=word.length();
   // create a new array of chars to copy to (+1 for a null terminator)
    char* char_array = new char[len + 1];
    char_array[len]= '\0';
    for (int i=0;i<len;i++){
      char_array[i]=toupper(word[i]);
 
      
    }

    return(char_array);
  
} 

int main() 
{
   string str="abcdeeeeeeeee";
   string final_char_array=cover_letter(str);  
   cout << final_char_array;
 
    return 0;
}

--------------------------------------------------------------------

Output:

ABCDEEEEEEEEE
```

```cpp
//大轉小 tolower 

#include <iostream>
#include <cstring> 
using namespace std;

string cover_letter(string word){
  
  int len=word.length();
   // create a new array of chars to copy to (+1 for a null terminator)
    char* char_array = new char[len + 1];
    char_array[len]= '\0';
    for (int i=0;i<len;i++){
      char_array[i]=tolower(word[i]);
 
      
    }

    return(char_array);
  
} 

int main() 
{
   string str="AVCXXXXX";
   string final_char_array=cover_letter(str);  
   cout << final_char_array;
 
    return 0;
}

----------------------------------------------------
Output:

avcxxxxx
```