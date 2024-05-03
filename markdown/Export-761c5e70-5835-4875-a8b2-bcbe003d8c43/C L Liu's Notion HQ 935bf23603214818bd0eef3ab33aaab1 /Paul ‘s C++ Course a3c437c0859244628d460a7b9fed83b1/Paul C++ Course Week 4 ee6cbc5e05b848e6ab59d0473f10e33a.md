# Paul C++ Course Week 4

Owner: C.L. Liu
Last edited time: May 23, 2023 10:03 AM

[Phill-CPP_0322.pdf](Paul%20C++%20Course%20Week%204%20ee6cbc5e05b848e6ab59d0473f10e33a/Phill-CPP_0322.pdf)

[https://youtu.be/aCxs4UYcaR4](https://youtu.be/aCxs4UYcaR4)

練習“C++ is fun to learn!” → “C++-is-fun-to-learn!”

```cpp
1#include <iostream>
using namespace std;

//練習“C++ is fun to learn!” → “C++-is-fun-to-learn!” 
int main() 
{
    string str1="C++ is fun to learn!!";
    string str2="";
    int len =str1.size();
    
    for(size_t i=0;i<len;i++){
      if(str1[i]==' '){
        str2.append("-");
      }else{
        str2.append(1,str1[i]);
      }
    }
    cout << str2; 
    return 0;
}

---------------------------------
Output:

C++-is-fun-to-learn!!
```

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() 
{
    string str1="C++ is fun to learn!";
    int len =str1.size();
    char* array=new char[len];
    
    for (size_t i=0;i<len;i++){
      array[i]=str1[i];
      if(str1[i]==' '){
        array[i]='-';
      }
      cout <<array[i];
    }
    
    return 0;
}

---------------------------------
Output:
C++-is-fun-to-learn!
 
```

```cpp
#include <iostream>
using namespace std;

string Addsymbol(string word){
  int len = word.size();
  string str2="";
  
  for(size_t i=0;i<len;i++){
    if(word[i]==' '){
      str2.append("-");
    }else{
      str2.append(1,word[i]);
    }
  }
  return(str2);
  
}

int main() 
{
    string str1 ="C++ is fun to learn!";
    string res=Addsymbol(str1);
    cout << res;
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

string Addsymbol(string word){
  int len = word.size();
     char* array=new char[len];
    
    for (size_t i=0;i<len;i++){
      array[i]=word[i];
      if(word[i]==' '){
        array[i]='-';
      }
       
    }
    return(array);
}

int main() 
{
    string str1 ="C++ is fun to learn!";
    string res=Addsymbol(str1);
    cout << res;
    return 0;
}
```

## Note :

### **size_t 和 int 比較**

- size_t在32位架構中定義為：typedef unsigned int size_t；
- size_t在64位架構中被定義為：typedef unsigned long size_t；
- size_t是無符號的，並且是平臺無關的，表示0-MAXINT的範圍；int為是有符號的；
- int在不同架構上都是4位元組，size_t在32位和64位架構上分別是4位元組和8位元組，在不同架構上進行編譯時需要注意這個問題。
- **ssize_t**是**有符號**整型，在32位機器上等同與int，在64位機器上等同與 long int.

計算長度用 : src.size(); 

## **Append()**

**C++ string append()新增文字**

使用append()新增文字常用方法:

**直接新增另一個完整的字串:**

如str1.append(str2);

**新增另一個字串的某一段子串:**

如str1.append(str2, 11, 7);

**新增幾個相同的字元:**

如str1.append(5, '.');

注意,個數在前字元在後.上面的程式碼意思為在str1後面新增5個".".

`//========================================
 
#include<iostream>
 
using namespace std;
 
//========================================
 
int main()
 
{
 
 string str1="I like C++";
 
 string str2=",I like the world.";
 
 string str3="Hello";
 
 string str4("Hi");
 
 //====================================
 
 str1.append(str2);
 
 str3.append(str2, 11, 7);
 
 str4.append(5, '.');
 
 //====================================
 
 cout<<str1<<endl;
 
 cout<<str3<<endl;
 
 cout<<str4<<endl;
 
 system("pause");
 
 return 0; 
 
}
 
//========================================`

**執行結果為**

`I like C++,I like the world.
Hello World.
Hi.....`