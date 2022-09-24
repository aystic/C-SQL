# C++ Standard Template Library

## `<string>`

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
