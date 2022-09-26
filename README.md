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

---

## &lt;list&gt;

```C++
/* Initialization */
list<int> l1;//empty
list<int> l2{1, 2, 3, 4, 5};//1,2,3,4,5
list<int> l3(l2);//copy
list<int>l4(5, 0);//0,0,0,0,0 ; fill
list<int>l5;
l5 = l4;
l5 = {1, 2, 3, 4, 5};
list<int>::iterator itr = l2.begin();
list<int>l6(l2.begin(), (advance(itr, 3), itr));//1,2,3


/* Looping */
for (int i : l2)cout << i << " ";//"int &i" to modify
//OR
for (list<int>::iterator itr = l2.begin(); itr != l2.end(); ++itr)cout << *itr << " ";

/* Iterators
- begin, end, rbegin, rend, cbegin, cend, crbegin, crend
*/

/* Methods */
l2.empty();//true|false
l2.size();//number of elements

l2.front();//1
l2.back();//5

l2.push_front(99);//99,1,2,3,4,5
l2.pop_front();//1,2,3,4,5
l2.push_back(99);//1,2,3,4,5,99
l2.pop_back();//1,2,3,4,5

l2.assign(3,0);//0,0,0
l2.assign(l4.begin(),l4.end());//0,0,0,0,0
l2.assign({1,2,3,4,5});//1,2,3,4,5

l2.insert( (itr = l2.end(), advance(itr, -2), itr), 99); //1,2,3,99,4,5
l2.insert(++l2.begin(), 3, 0); //1,0,0,0,2,3,99,4,5
l2.insert(++l2.begin(), l4.begin(), l4.end());//1,0,0,0,0,0,0,0,0,2,3,99,4,5
l2.insert(++l2.begin(), {9, 8, 7});//1,9,8,7,0,0,0,0,0,0,0,0,2,3,99,4,5

l2.erase(l2.begin());//9,8,7,0,0,0,0,0,0,0,0,2,3,99,4,5
l2.erase(l2.begin(), (advance(itr, -1), itr));//99,4,5

l2.resize(5);//99,4,5,0,0
l2.resize(8, 99);//99,4,5,0,0,99,99,99
l2.resize(5);//99,4,5,0,0

l2.clear();//size=0

l2.splice(++l2.begin(), l5);//99,1,2,3,4,5,4,5,0,0 ; l5->empty
l2.splice(++l2.begin(), l5, l5.begin(), --l5.end());//99,1,2,3,4,4,5,0,0 ; l5->5
l2.splice(++l2.begin(), l5, ++l5.begin());//99,2,4,5,0,0 ; l5->1,3,4,5

l2.remove(0);//99,2,4,5


/* Accepts predicate */
bool is_even(const int& val) {
	return (val & 1) == 0 ? true : false;
}

class is_odd {
public:
	bool operator()(const int& val) {
		return (val & 1 ) ==  1 ? true : false;
	}
};
l2.remove_if(is_even);//99,5
l2.remove_if(is_odd());//empty

l2 = {1, 2, 2, 3, 3, 4, 5, 6, 7, 7, 8, 8, 9};
l2.unique();//removes all the duplicates
/* Accepts binary predicate : removes the first element on returning true*/
bool is_even(const int& val1, const int& val2) {
	return ((val1 == val2) && (!(val1 & 1) && !(val2 & 1))) ? true : false;
}

class is_odd {
public:
	bool operator()(const int& val1, const int&val2) {
		return ((val1 == val2) && ((val1 & 1) && (val2 & 1))) ? true : false;
	}
};
l2.unique(is_even);//removes all even duplicate pairs
l2.unique(is_odd());//removes all odd duplicate pairs

l1 = {1, 3, 5, 7};
l2 = {2, 4, 5, 6, 8, 9};
//l1 and l2 should be sorted
l2.merge(l1);//l2->1,2,3,4,5,5,6,7,8,9 ; l1->empty
//if Binary Predicate returns true then the first element (in the argument of the predicate) goes first
l2.merge(l1, binaryPredicate);

l2.reverse();

l2.sort();
l2.sort(binaryPredicate);

/* Relational operators
==, !=, > , < ,>=, <= -> lexicographical
*/
```

---

## &lt;stack&gt;

- It is a container adaptor
- By default the underlying container is `deque` but `vector` and `list` can also be used

```C++
/* Initialization */
vector<int> v{1, 2, 3, 4, 5};
list<int> l{1, 2, 3, 4, 5};
deque<int>d{1, 2, 3, 4, 5};

stack<int> st1;
stack<int, vector<int>> st2(v);
stack<int, list<int>> st3(l);
stack<int, deque<int>> st4(d);//equivalent to st1

st1.size();
st.empty();//true|false

st1.top();
st1.push(99);
st1.pop();

/* Relational operators
==, !=, >, <, >=, <= -> lexicographical
*/
```

---

## &lt;queue&gt;

- It is a container adaptor
- By default the underlying container is `deque` but `list` can also be used

```C++
/* Initialization */
list<int> l{1, 2, 3, 4, 5};
deque<int>d{1, 2, 3, 4, 5};

queue<int> q1;
queue<int, list<int>> q2(l);
queue<int, deque<int>> q3(d);//equivalent to q1

q1.size();
q1.empty();

q1.push(99);
q1.pop();
q1.front();
q1.back();

/* Relational operators
==, !=, >, <, >=, <= -> lexicographical
*/
```

---

## &lt;queue&gt;->priority_queue

- It is a container adaptor
- By default the underlying container is `vector` but `dequeue` can also be used

```C++
/* Initialization */
vector<int> v{1, 2, 3, 4, 5};
deque<int>d{1, 2, 3, 4, 5};

priority_queue<int>pq1;//max heap; empty
priority_queue<int, vector<int>, greater<int>>pq2(v.begin(), v.end()); //min heap
priority_queue<int, deque<int>>pq3(d.begin(), d.end()); //max heap
priority_queue<int, deque<int>, greater<int>>pq4(d.begin(), d.end()); //min heap
priority_queue<int, vector<int>>pq5; //equivalent to pq1

class comparator {
	bool reverse;
public:
	comparator(const bool & reverse = false) {
		this->reverse = reverse;
	}
	bool operator()(const int&val1, const int& val2) {
		return reverse ? (val1 > val2) : (val1 < val2);
	}
};
priority_queue<int, vector<int>, comparator>pq7; //max heap
priority_queue<int, vector<int>, comparator>pq8(comparator(true));//min heap

pq1.empty();
pq1.size();

pq1.top();
pq1.push(99);
pq1.pop();
```

---
