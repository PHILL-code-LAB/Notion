# Paul C++ Course Week 12

Owner: C.L. Liu
Last edited time: January 3, 2024 7:30 PM

[Phill-CPP-0524.pdf](Paul%20C++%20Course%20Week%2012%209f3e5c5d96104dacbcf60b44a469cdd6/Phill-CPP-0524.pdf)

[https://youtu.be/B8C5TVVcl4o](https://youtu.be/B8C5TVVcl4o)

Sample 1: 

```cpp
## Sample 1 
#include <iostream>
#include <cctype> 
using namespace std;

int main()  {
int a=0 , b=0,c=0,d=0;
string input={"aAbBc12345@#$%"};

for(int i=0;i<input.length();i++){
    
    if(isupper(input[i])){
      a++;
    }else if(islower(input[i])){
      b++;
    }else if(isdigit(input[i])){
      c++;
    }else{
      d++;
    }
}
cout <<"upper numbers is -->" <<a <<endl;
cout <<"lower numbers is -->" << b <<endl;
cout << "digit numbers is --> " << c <<endl;
cout << "others numbers is -->" << d <<endl;
return 0;

}

Output:

upper numbers is -->2
lower numbers is -->3
digit numbers is --> 5
others numbers is -->4
```

Sample 2 : 

```cpp
請挑出字元請使⽤ c-style 字串陣列
#include <iostream>
#include <cstring>
#include <cctype> 
using namespace std;

int main() 
{
    char arr1[]="aAbBc12345@#$%";
    int len = strlen(arr1);
    char upper[101]="";
    char lower[101]="";
    char digit[101]="";
    char others[101]="";  //需要初始化 不然會跑出奇怪的符號
    
    int upper_cnt=0 , lower_cnt=0,digit_cnt=0,others_cnt=0;
    for(int i=0;i<len;i++){
      char str=arr1[i];
      
      if(isupper(str)){
      upper[upper_cnt++]=str;
      }else if(islower(str)){
        lower[lower_cnt++]=str;
      }else if(isdigit(str)){
        digit[digit_cnt++]=str;
      }else {
        others[others_cnt++]=str; 
      }
      
    }
    cout << "upper_word-->" << upper<<endl;
    cout << "lower_word-->" << lower<<endl;
    cout << "digit_word-->" << digit<<endl;
    cout << "others_word-->"<< others<<endl;
    return 0;
}

Output:

upper_word-->AB
lower_word-->abc
digit_word-->12345
others_word-->@#$%
```

```cpp
Sample 3 

“Hello Advantek!” → 不管⼤⼩寫, 忽略digits others
→
 H or h = ? 個
Ｅ or e = ? 個
……

#include <iostream>
#include <cstring>
#include <cctype> 
using namespace std;

int main() 
{
    string str="Hello Advantech!";
    int len = str.size();
    int c[26]={0};
    for(int i=0;i<len;i++){
        str[i] =tolower(str[i]);
        cout << str[i];
        if(str[i]>='a' && str[i]<='z'){
          c[str[i]-'a']++;
          
        }
    }

  cout <<endl;
  for(int i=0;i<26;i++){
    cout << char(i+65)<< "發生-->" <<c[i] <<endl; //(大寫)
    //cout << char(i+97)<< "發生-->" <<c[i] <<endl; (小寫)
  }
  	
    return 0;
}

Output:

hello advantech!
A發生-->2
B發生-->0
C發生-->1
D發生-->1
E發生-->2
F發生-->0
G發生-->0
H發生-->2
I發生-->0
J發生-->0
K發生-->0
L發生-->2
M發生-->0
N發生-->1
O發生-->1
P發生-->0
Q發生-->0
R發生-->0
S發生-->0
T發生-->1
U發生-->0
V發生-->1
W發生-->0
X發生-->0
Y發生-->0
Z發生-->0
```

```cpp
#include<iostream>
#include<string>
//#include<cstring>
using namespace std;
int main()
{
	string str="hello advantech!";
 
	int cnt[256]={};
	for(int i=0;i<str.size();i++)
	//for(int i=0;i<strlen(str);i++)
		cnt[(int)str[i]]++;
	for(int i=0;i<256;i++)//输出字符出现次数
	{
		if(cnt[i]!=0)
			cout<<(char)i<<':'<<cnt[i]<<endl;
	}
}

Output:

 :1
!:1
a:2
c:1
d:1
e:2
h:2
l:2
n:1
o:1
t:1
v:1
```

```cpp
#include <iostream>
#include <cstring>
#include <cctype> 
using namespace std;

int main() 
{
    string letter="abcdefghijklmnopqrstuvwxyz";
    string str="Hello Advantech!";
    int len = str.size();
    int cnt[26]={0};
    for(int i=0;i<len;i++){
      for(int j=0;j<26;j++){
        str[i] =tolower(str[i]);
        if(str[i]==letter[j]){
          cnt[j]++;
        }
      }
    }

  cout <<endl;
  for(int i=0;i<26;i++){
    cout << char(i+65)<< "發生-->" <<cnt[i] <<endl; //(大寫)
  }
  	
    return 0;
}

Output:

A發生-->2
B發生-->0
C發生-->1
D發生-->1
E發生-->2
F發生-->0
G發生-->0
H發生-->2
I發生-->0
J發生-->0
K發生-->0
L發生-->2
M發生-->0
N發生-->1
O發生-->1
P發生-->0
Q發生-->0
R發生-->0
S發生-->0
T發生-->1
U發生-->0
V發生-->1
W發生-->0
X發生-->0
Y發生-->0
Z發生-->0
```

```cpp

Sample 4
兩個字串之間的關係
ABCDABBADCAB 
AB 
1 5 11  <<-- 會在這些位置出現 AB 

#include <iostream>
#include <string>
using namespace std;

int main() 
{
   string str1, str2;
   cin >> str1 >> str2;
   
   size_t str1_len=str1.length(); // 12 
   size_t str2_len=str2.length(); // 2  
   int diff = str1_len-str2_len;  /// 當不同長度比字串時   
   cout << diff <<endl;
   for(size_t i=0;i<=str1_len-str2_len;i++){
     if(str1.substr(i,str2_len)==str2){
       cout  << i+1 << " ";
     }
   }
   return 0;
}

STDIN
ABCDABBADCAB  
AB

Output:

10
1 5 11
```