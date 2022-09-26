# C++ Standard Template Library

## &lt;string&gt;

```C++
/* Initialization */
string s0;//empty string
string s1{"Hello"};//"Hello"
string s2(s1);//"Hello"
string s7("Hello",2);//"He"
string s3(s1, 2); //"llo"
string s4(s1, 1, 3); //"ell"
string s5(s1.begin(), s1.begin() + 3); //"Hel"
string s6(3, '*'); //"***"

/* Iterators */
//Type -> std::string::iterator
char ch=*s1.begin();//H
char ch=*(s1.end() - 1);//o
char ch=*s1.rbegin();//o
char ch=*(s1.rend() - 1) ;//H
char ch=*s1.cbegin();//H
char ch=*(s1.cend() - 1) ;//o
char ch=*s1.crbegin();//o
char ch=*(s1.crend() - 1);//H

/* Looping */
for (string::iterator itr = s1.begin(); itr != s1.end(); ++itr) {
	cout << *itr;
}
//OR
for (int i = 0; i < s1.size(); ++i) {
	cout << s1[i];
}
//OR
for (char ch : s1) {//"char &ch" to modify
	cout << ch;
}

/* Methods */
s1.length();
s1.size();
s1.resize(10,'x');//"Helloxxxxx"
s1.resize(3);//"Hel"
s1.resize(4);//"Hel\0"
s1.capacity();//>=length
s1.reserve(28);//capacity>=28
s1.clear();//""
s1.empty();//true | false
s1.front();//'H'
s1.back();//'l'
s1.push_back('x');//Hellox
s1.pop_back();
const char * str = s1.c_str();
const char* str2 = s1.data();
s1.copy(to,no_of_char,start_posn);
/*
find -> first occurence
rfind -> last occurence
*/
s1.find("*");//-1
s1.find(string,start_pos,no_of_chars_to_match);
// find_fisrt_not_of and find_last_not_of also exist
s1.find_first_of(string);//first match any char of string
s1.find_last_of(string);//last match of any char of string
string arr = s1.substr(2);//llo
string arr2 = s1.substr(2, 2);//ll
s1.compare(0, 3, "Hi Hello", 3, 3);//0; |Hel|lo == Hi |Hel|lo

// Append
s1.append(s1);//HelloHello
s1.append(s1, 2, 3);//Hellollo
s1.append("Hello", 2);//HelloHe
s1.append("world");//Helloworld
s1.append(3, '*');//Hello***

//Assign
s1.assign(s2);//Hello
s1.assign("world");//world
s1.assign("world", 4);//worl
s1.assign("world", 2, 3);//rld
s1.assign(3, '*'); //***
s1.assign(s2.begin(), s2.begin() + 2);//He

//Erase
s1.erase(2, 2); //Heo
s1.erase(2);//He
s1.erase(s1.begin() + 1); //Hllo
s1.erase(s1.begin(), s1.begin() + 2); //llo

//Insert
s1.insert(2, "***"); //He***llo
s1.insert(2, s2); //HeHellollo
s1.insert(2, "World", 4); //HeWorlllo
s1.insert(2, "World", 2, 3); //Herldllo
s1.insert(2, 3, '*'); //He***llo
s1.insert(s1.begin() + 2, s2.begin(), s2.end() ); //HeHellollo

//Replace
/* Positions can be also given as the iterators */
s1.replace(0, 2, "xyz");//xyzllo
s1.replace(0, 2, s2); //Hellollo
s1.replace(0, 2, "world", 3); //worllo
s1.replace(0, 2, "world", 2, 3); //rldllo
s1.replace(0, 2, 3, '*');//***llo

```

---

## &lt;array&gt;

```C++
/* Initialization */
array<int, 5> arr{1, 2, 3, 4, 5};

/* Looping */
for (int i : arr)cout << i << " ";//"int &i" to modify
//OR
for (int i = 0; i < arr.size(); ++i)cout << arr[i] << " ";
//OR
for (array<int, 5>::iterator itr = arr.begin(); itr != arr.end(); ++itr)cout << *itr << " ";
//OR
int* ptr = arr.data();//Pointer to first element
for (int i = 0; i < 5; ++i)cout << *(ptr + i) << " ";

/* Iterators
- begin, end, rbegin, rend, cbegin, cend, crbegin, crend
*/

/* Methods */
arr.size();//5
arr.empty();//true|false
arr.front();//1
arr.back();//5
arr.fill(0);//0 0 0 0 0
arr.swap();
arr[pos];//access elements
get<pos>(arr);//access elements
arr1==arr2;//== != > < >= <=

```

---

## &lt;vector&gt;

```C++

/* Initialization */
vector<int> arr;//empty
vector<int>arr1{1, 2, 3, 4, 5};//Initializer list
vector<int>arr2(5, 0);//fill; 0,0,0,0,0
vector<int>arr3(arr1.begin(), arr1.begin() + 3);//1,2,3
vector<int>arr4(arr1);//copy
arr4=arr2;//arr4-> 0,0,0,0,0


/* Iterators
- begin, end, rbegin, rend, cbegin, cend, crbegin, crend
*/


/* Looping */
for (int i : arr1)cout << i << " ";//use "int &i" to modify
//OR
for (vector<int>::iterator itr = arr1.begin(); itr != arr1.end(); ++itr)
	cout << *itr << " ";
//OR
for (int i = 0; i < arr1.size(); ++i)cout << arr1[i] << " ";
//OR
int *ptr = arr.data();//returns the pointer
for (int i = 0; i < arr.size(); ++i)cout << *(ptr + i) << " ";


/* Methods */
arr1.push_back(9);//1,2,3,4,5,9
arr1.pop_back();//1,2,3,4,5
arr1.size();//number of elements
arr1.capacity();//>=size
arr1.reserve(20);//20>arr1.capacity()?capacity=20:capacity=arr1.capacity();
arr1.empty();//true|false

//Resize
arr1.resize(3);//1,2,3
arr1.resize(5);//1,2,3,0,0

//Erase
arr1.erase(arr.begin()+3);//1,2,3,0
arr1.erase(arr.begin(),arr.begin()+2);//3,0

arr1.front();//1
arr1.back();//0
arr1.clear();//size=0

//Assign
arr1.assign(arr.begin(), arr.end());
arr1.assign({1, 2, 3});
int array[] {9, 8, 7, 6, 5};
arr1.assign(array, array + 3);//9,8,7

//Insert
arr.insert(arr.begin() + 2, 99);//9,8,99,7
arr.insert(arr.begin() + 2, 3, 0);//9,8,0,0,0,99,7
arr.insert(arr.begin(), arr.begin(), arr.begin() + 2);//9,8,9,8,0,0,0,99,7

/* relational operators
== != > < >= <= -> lexicographical
 */

```
