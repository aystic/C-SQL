# C++ Standard Template Library

## STL Components

- Containers
  - Sequence Containers
    - [Array](#array)
    - [Vector](#vector)
    - [List](#list)
    - [Deque](#deque)
    - [Forward List](#forward_list)
  - Container Adaptors
    - [Stack](#stack)
    - [Queue](#queue)
    - [Priority Queue](#queue-priority_queue)
  - Associative Containers
    - [Set](#set)
    - [Multiset](#set-multiset)
    - [Map](#map)
    - [Multimap](#map-multimap)
  - Unordered Associative Container
    - [Unordered Set](#unordered_set)
    - [Unordered Multiset](#unordered_set---unordered_multiset)
    - [Unordered Map](#unordered_map)
    - [Unordered Multimap](#unordered_map---unordered_multimap)
- [Algorithms](#algorithm)
- Others
  - [String](#string)
  - [IOManip](#iomanip)
  - [Limits](#limits)
  - [Utility](#utility)
  - [Tuple](#tuple)
  - [Bitset](#bitset)
  - [Functors](#functors)

---

## &lt;array&gt;

[View Index](#stl-components)

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

[View Index](#stl-components)

- Internally, **Dynamically allocated array** is used

```C++
/* Initialization */
vector<int> v;//empty
vector<int>v1{1, 2, 3, 4, 5};//Initializer list
vector<int>v2(5, 0);//fill; 0,0,0,0,0
vector<int>v3(v1.begin(), v1.begin() + 3);//1,2,3
vector<int>v4(v1);//copy
v4=v2;//v4-> 0,0,0,0,0


/* Iterators
- begin, end, rbegin, rend, cbegin, cend, crbegin, crend
*/


/* Looping */
for (int i : v1)cout << i << " ";//use "int &i" to modify
//OR
for (vector<int>::iterator itr = v1.begin(); itr != v1.end(); ++itr)
	cout << *itr << " ";
//OR
for (int i = 0; i < v1.size(); ++i)cout << v1[i] << " ";
//OR
int *ptr = v.data();//returns the pointer
for (int i = 0; i < v.size(); ++i)cout << *(ptr + i) << " ";


/* Methods */
v1.push_back(9);//1,2,3,4,5,9
v1.pop_back();//1,2,3,4,5

v1.size();//number of elements
v1.capacity();//>=size
v1.reserve(20);//20>v1.capacity()?capacity=20:capacity=v1.capacity();
v1.empty();//true|false

//Resize
v1.resize(3);//1,2,3
v1.resize(5);//1,2,3,0,0

//Erase
v1.erase(v.begin()+3);//1,2,3,0
v1.erase(v.begin(),v.begin()+2);//3,0

v1.front();//1
v1.back();//0
v1.clear();//size=0

//Assign
v1.assign(v.begin(), v.end());
v1.assign({1, 2, 3});
int vay[] {9, 8, 7, 6, 5};
v1.assign(vay, vay + 3);//9,8,7

//Insert
v.insert(v.begin() + 2, 99);//9,8,99,7
v.insert(v.begin() + 2, 3, 0);//9,8,0,0,0,99,7
v.insert(v.begin(), v.begin(), v.begin() + 2);//9,8,9,8,0,0,0,99,7

/* relational operators
== != > < >= <= -> lexicographical
 */
```

---

## &lt;list&gt;

[View Index](#stl-components)

- Implemented as **doubly linked lists**

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

## &lt;deque&gt;

[View Index](#stl-components)

- Generally implemented as **dynamic arrays**
- **Not guaranteed** to store all the elements in contiguous manner
- Elements are **scattered** in different chunks of storage

```C++
/* Initialization */
int arr[] {1, 2, 3};
vector<int> v{1, 2, 3, 4, 5};

deque<int> dq;//empty
deque<int> dq1(3);//0,0,0
deque<int> dq2(3, 99); //99,99,99
deque<int> dq3{1, 2, 3, 4, 5}; //1,2,3,4,5
deque<int> dq4(dq3);//1,2,3,4,5
deque<int> dq5(arr, arr + (sizeof(arr) / sizeof(int))); //1,2,3
deque<int> dq6(v.begin(), v.end() - 2); //1,2,3
dq=dq1;//0,0,0
dq={1,2,3,4,5};//1,2,3,4,5

/* Iterators
- begin, end, rbegin, rend, cbegin, cend, crbegin, crend
*/

//Looping
for (int i : dq)cout << i << " ";//use 'int &i' to modify
//OR
for (int i = 0; i < dq.size(); ++i)cout << dq[i] << " ";
//OR
for (deque<int>::iterator itr = dq.begin(); itr != dq.end(); ++itr)cout << *itr << " ";

//Capacity
dq.size();
dq.empty();//true|false
dq.resize(3);//1,2,3
dq.resize(4);//1,2,3,0
dq.resize(5,99);//1,2,3,0,99

//Element access
dq[3];//0
dq.at(3);//0
dq.front();//1
dq.back();//99

//Modifiers
dq.push_back(0);
dq.pop_back();
dq.push_front(0);
dq.pop_front();

dq.assign(dq1.begin(),dq1.end()-1);//0,0
dq.assign(arr,arr+3);//1,2,3
dq.assign(3,1);//1,1,1
dq.assign({1,2,3,0,99});//1,2,3,0,99

dq.erase(dq.begin() + 3); //1,2,3,99
dq.erase(dq.begin() + 2, dq.begin() + 4);//1,2

dq.insert(dq.begin() + 2, 99);//1,2,99
dq.insert(dq.begin() + 1, 3, 0); //1,0,0,0,2,99
dq.insert(dq.begin(), arr, arr + 2);//1,2,1,0,0,0,2,99
dq.insert(dq.end(), {2, 3, 4});//1,2,1,0,0,0,2,99,2,3,4

dq.clear();//size=0

/* Relational operators
== != > < >= <= -> lexicographical
*/
```

---

## &lt;forward_list&gt;

[View Index](#stl-components)

- Implemented as **singly linked lists**

```C++
/* Initialization */
int arr[] {1, 2, 3, 4, 5};

forward_list<int> fl;//empty
forward_list<int> fl1(5, 0); //0,0,0,0,0
forward_list<int> fl2(arr, arr + 3); //1,2,3
forward_list<int> fl3({1, 2, 3, 4, 5}); //1,2,3,4,5
forward_list<int> fl4(fl3);//1,2,3,4,5
fl=fl1;
fl={1,2,3,4,5};

/* Iterators
- [before_begin, cbefore_begin] -> Should not be dereferenced; Used as an argument in (insert_after, splice_after, erase_after), begin, end, cbegin, cend
*/

//Looping
for (int i : fl1)cout << i << " ";
//OR
for (forward_list<int>::iterator itr = fl1.begin(); itr != fl1.end(); ++itr)cout << *itr << " ";

//Capacity
fl.empty();//true|false

//Element access
fl.front();

//Modifiers
fl.push_front(99);
fl.pop_front();

fl.resize(3);//1,2,3
fl.resize(4);//1,2,3,0
fl.resize(5,99);//1,2,3,0,99

fl.assign(arr, arr+3);//1,2,3
fl.assign(5,0);//0,0,0,0,0
fl.assign({1,2,3,4,4});//1,2,3,4,5

forward_list<int>::iterator itr = fl.before_begin();
fl.insert_after(itr, 99);//->99 1 2 3 4 5
fl.insert_after(++itr, {0, 0, 0});//99 ->0 0 0 1 2 3 4 5
fl.insert_after(itr, 2, 1);//99 ->1 1 0 0 0 1 2 3 4 5
fl.insert_after(itr, arr, arr + 3);//99 ->1 2 3 1 1 0 0 0 1 2 3 4 5

fl.erase_after(itr);//->99 2 3 1 1 0 0 0 1 2 3 4 5
fl.erase_after(fl.before_begin(), (advance(itr, 5), itr));//range to clean; ->0 0 0 1 2 3 4 5

fl.clear();//empty

//Operations
advance(itr, 7);//fl->0 0 1 2 3 4 5<-
fl.splice_after(itr, fl4);//fl-> fl+fl4, fl4->empty
//OR
fl.splice_after(itr, fl4, fl4.begin());//fl->0 0 0 1 2 3 4 5 2 , fl4->1 3 4 5
//OR
forward_list<int>::iterator itr1 = fl4.begin();
fl.splice_after(itr, fl4, fl4.before_begin(), (advance(itr1, 3), itr1));//fl->0 0 0 1 2 3 4 5 1 2 3, fl4-> ->4 5

fl.remove(0);
/* unary predicate returns true if that element is to be removed */
bool removeEven(const int& val) {
	return (val & 1) == 0 ? true : false;
}

class removeOdd {
public:
	bool operator()(const int& val) {
		return (val & 1) == 1 ? true : false;
	}
} removeOddObj;
fl.remove_if(removeEven);
fl.remove_if(removeOddObj);
fl.remove_if(removeOdd());

fl.unique();//removes all the duplicates
/* binary predicate return true if the first element should be removed */
bool removeUniques(const int& val1, const int& val2) {
	return ((val1 < 2 and val2 < 2) & (val1 == val2)) == true ? true : false;
}

class removeUniques {
public:
	bool operator()(const int& val1, const int& val2) {
		return ((val1 >= 2 and val2 >= 2) & (val1 == val2)) == true ? true : false;
	}
} removeUniquesObj;
fl.unique(removeUniques);
fl.unique(removeUniquesObj);

/* Both containers should be ordered */
fl.merge(fl1);//fl1 becomes empty
/* Binary predicate returns true if first element should go before the second element */
fl.merge(fl1,greater<int>());

fl.sort();
/* Binary predicate returns true if the first element should go before the second elemnt */
fl.sort(greater<int>());

fl.reverse();

/* Relational operators
== != > < >= <=
*/
```

---

## &lt;stack&gt;

[View Index](#stl-components)

- It is a **container adaptor**
- By default the underlying container is **`deque`** but **`vector`** and **`list`** can also be used

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

[View Index](#stl-components)

- It is a **container adaptor**
- By default the underlying container is **`deque`** but **`list`** can also be used

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

[View Index](#stl-components)

- It is a **container adaptor**
- By default the underlying container is **`vector`** but **`dequeue`** can also be used

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

## &lt;set&gt;

[View Index](#stl-components)

- Store **unique elements** following a **specific order**
- The value of an element is the key(must be unique)
- Elements are always **const** - cannot be modified once in container
- Elements are **sorted**
- Slower than unordered_set
- Implemented as **BST**

```C++
/* Initialization */
class compareClass {
public:
	bool operator() (const int& lhs, const int& rhs) const
	{return lhs > rhs;}
} ;

bool compare(const int&val1, const int&val2) {
	return val1 > val2 ? true : false;
}

int arr[] {1, 2, 3, 4, 5};

set<int> s;
set<int> s1{1, 2, 3, 4, 5};
set<int> s2(arr, arr + 5);
set<int> s3(s2);
s=s1;
s={9,8,7};
bool(*fnPtr)(const int&, const int&) = compare;
set<int, bool(*)(const int&, const int&)> s4({1, 2, 3, 4, 5}, fnPtr);

set<int, compareClass> s5({4, 5, 6, 7, 8});

/* Iterators
- begin, end, rbegin, rend, cbegin, cend, crbegin, crend
*/

//Capacity
s.empty();
s.size();//number of elements

//Modifiers
s.insert(99);
s.insert(s.begin(),22);//position is the hint, iterator of the next element in order
s.insert(arr, arr+3);
s.insert({1,2,3,4,5});

s.erase(2);//1,3,4,5,22,99
s.erase(++s.begin());//1,4,5,22,99
set<int>::iterator itr = s.begin();
s.erase(s.begin(), (advance(itr, 3), itr));//22,99

s.clear();//empty
s.find(99);//return itr -> *itr=>99 or s.end() if not found
s.count(25);//returns number of times a value is present

s.lower_bound(10);//next element>=10
s.upper_bound(10);//next element > 10

s.equal_pair(10);//returns pair; first->lower_bound(10) second->upper_bound(10); can contain only one element in the range
```

---

## &lt;set&gt;->Multiset

[View Index](#stl-components)

- Store elements following a **specific order**, and where multiple elements **can have equivalent values**
- Value of the element is the key; It is **const** and cannot be modified once in the container
- Elements are in **sorted** order
- Slower than unorderd_multiset
- Implemented as **BST**

```C++
class compareClass {
public:
	bool operator() (const int& lhs, const int& rhs) const
	{return lhs > rhs;}
} ;

bool compare(const int&val1, const int&val2) {
	return val1 > val2 ? true : false;
}

int arr[] {1, 2, 3, 4, 5};

multiset<int> ms;
multiset<int> ms1{1, 2, 3, 4, 5};
multiset<int> ms2(arr, arr + 5);
multiset<int> ms3(ms2);
bool(*fnPtr)(const int&, const int&) = compare;
multiset<int, bool(*)(const int&, const int&)> ms4({1, 2, 3, 4, 5}, fnPtr);
multiset<int, compareClass> ms5({4, 5, 6, 7, 8});

/* Iterators
- begin, end, rbegin, rend, cbegin, cend, crbegin, crend
*/

//Capacity
ms.empty();
ms.size();//number of elements

//Modifiers
ms.insert(99);
ms.insert(ms.begin(),22);//position is the hint, iterator of the next element in order
ms.insert(arr, arr+3);
ms.insert({1,2,3,4,5});

ms.erase(2);//1 1 3 3 4 5 22 99
ms.erase(++ms.begin());//1 3 3 4 5 22 99
set<int>::iterator itr = ms.begin();
ms.erase(ms.begin(), (advance(itr, 3), itr));//4 5 22 99

ms.clear();//empty
ms.find(99);//return itr -> *itr=>99 or ms.end() if not found
ms.count(25);//returns number of times a value is present

ms.lower_bound(10);//next element>=10
ms.upper_bound(10);//next element > 10

ms.equal_pair(10);//returns pair; first->lower_bound(10) second->upper_bound(10); can contain more than one element in the range
```

---

## &lt;map&gt;

[View Index](#stl-components)

- Associative containers (key-value mapping)
- Follow a specific order
- The elements are **sorted by its key**
- Slower than unordered_map
- Typically implemented as **BST**

```C++
/* Initialization */
class compareClass {
public:
	bool operator() (const char& val1, const char& val2) const {
		return val1 > val2;
	}
} ;

bool compare(const char& val1, const char& val2) {
	return val1 > val2;
}

pair<char, int>arr[] {{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}};

map<char, int>mp;
map<char, int>mp1(arr, arr + 3);
map<char, int>mp2(mp1);
map<char, int>mp3({{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}});
bool(*fnPtr)(const char&, const char&) = compare;
map<char, int, bool(*)(const char&, const char&)>mp4(fnPtr);
mp4['a'] = 1;
mp4['b'] = 2;
mp4['c'] = 3;
map<char, int, compareClass>mp5({{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}});

/* Iterators
- begin, end, rbegin, rend, cbegin, cend, crbegin, crend
*/

//Looping
for (pair<char, int> p : mp5)cout << p.first << " " << p.second << endll;
//OR
for (map<char, int>::iterator itr = mp5.begin(); itr != mp5.end(); ++itr)cout << "(" << (*itr).first << "," << (*itr).second << ") ";

//Capacity
mp.empty();
mp.size();

//Element access
mp['a'];//gives 1
mp.at('a');//gives 1

//Modifiers
map<char, int, compareClass>::iterator itr = mp5.find('c');
mp5.erase(--mp5.end());//deletes last key-val pair
mp5.erase(itr, mp5.end());//deletes (c,3),(b,2) key-val pair
mp5.erase('d');//deletes (d,4) key-val pair

mp5.insert({'a', 1});
mp5.insert(hint,first_itr,last_itr);
mp5.insert(first_itr,last_itr);
mp5.insert({{'c', 3}, {'d', 4}});

mp.clear();//empty

//Operations
mp.find('a');//returns itr if element found, mp.end() otherwise; (*itr).first->'a',(*itr).second->1
mp.count('a');
mp.lower_bound('a');//iterator to lower bound
mp.upper_bound('a');//iterator to upper bound

typedef map<char, int, compareClass>::iterator itrType;
pair<itrType, itrType> itrRange;
itrRange = mp5.equal_range('c');//itrRange.first->('c',3), itrRange.second->('b',2)
```

---

## &lt;map&gt;->multimap

[View Index](#stl-components)

- Associative containers (key-value mapping)
- Follow a specific order
- Multiple elements **can have equivalent values**
- Elements always **sorted by its key**
- Slower than unordered_multimap
- Typically implemented as **BST**

```C++
/* Initialization */
class compareClass {
public:
	bool operator() (const char& val1, const char& val2) const {
		return val1 > val2;
	}
} ;

bool compare(const char& val1, const char& val2) {
	return val1 > val2;
}

pair<char, int>arr[] {{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}};

multimap<char, int>mmp;
multimap<char, int>mmp1(arr, arr + 3);
multimap<char, int>mmp2(mmp1);
multimap<char, int>mmp3({{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}});
bool(*fnPtr)(const char&, const char&) = compare;
multimap<char, int, bool(*)(const char&, const char&)>mmp4({{'a', 1}, {'b', 2}, {'c', 3}}, fnPtr);
multimap<char, int, compareClass>mmp5({{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}});

/* Iterators
- begin, end, rbegin, rend, cbegin, cend, crbegin, crend
*/

//Looping
for (pair<char, int> p : mmp5)cout << p.first << " " << p.second << endll;
//OR
for (map<char, int,compareClass>::iterator itr = mmp5.begin(); itr != mmp5.end(); ++itr)cout << "(" << (*itr).first << "," << (*itr).second << ") ";

//Capacity
mmp.empty();
mmp.size();

//Modifiers
multimap<char, int, compareClass>::iterator itr = mmp5.find('c');
mmp5.erase(--mmp5.end());//deletes last key-val pair
mmp5.erase(itr, mmp5.end());//deletes (c,3),(b,2) key-val pair
mmp5.erase('d');//deletes (d,4) key-val pair

mmp5.insert({'a', 1});
mmp5.insert(hint,first_itr,last_itr);
mmp5.insert(first_itr,last_itr);
mmp5.insert({{'c', 3}, {'d', 4}});

mmp.clear();//empty

//Operations
mmp.find('a');//returns itr if element found, mmp.end() otherwise; (*itr).first->'a',(*itr).second->1
mmp.count('a');
mmp.lower_bound('a');//iterator to lower bound
mmp.upper_bound('a');//iterator to upper bound

typedef multimap<char, int, compareClass>::iterator itrType;
pair<itrType, itrType> itrRange;
itrRange = mmp5.equal_range('c');
```

---

## &lt;unordered_map&gt;

[View Index](#stl-components)

- Associative containers (key-value mapping)
- Fast retrieval based on keys
- Elements are **not sorted** in any particular order
- Elements are **organized into buckets** based on their **hash values**

```C++
/* Initialization */
pair<char, int>arr[] {{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}};

unordered_map<char, int> um; //empty
unordered_map<char, int> um1({{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}}); //initializer list
unordered_map<char, int> um2(um1); //copy
unordered_map<char, int> um3(arr, arr + 3); //range
um=um1;
um={{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}};


//Capacity
um.empty();//true|false
um.size();//number of elements//

/* Iterators
begin, end, cbegin, cend
*/


//Element lookup
unordered_map<char, int>::iterator itr = um.find('c');//returns iterator or um.end(), *itr.first,*itr.second

um.count('c');//1 or 0

typedef unordered_map<char, int>::iterator itrType;
pair <itrType, itrType> itrPair = um.equal_range('b');


//Modifiers
um.clear();

um.insert({'e', 5});

unordered_map<char, int>::iterator itr = um1.begin();
advance(itr, 2);
um.insert(um1.begin(), itr);

um.insert({{'f', 6}, {'g', 7}});

um.erase('e');

um.erase(um.begin());

itr=um.begin();
advance(itr,2);
um.erase(um.begin(),itr);


//Buckets
/*
A bucket is a slot in the container's internal hash table to which elements are assigned based on the hash value of their key.
*/
int n = um.bucket_count();//number of buckets
for (int i = 0; i < n; ++i) {
	cout << "bucket #" << i << " contains: ";
	for (auto it = um.begin(i); it != um.end(i); ++it)
		cout << "[" << it->first << ":" << it->second << "] ";
	cout << endll;
}

int buckets = um.bucket_count();
for (int i = 0; i < buckets; ++i) {
	cout << um.bucket_size(i) << endll;//element in each bucket
}

um.bucket('e');//returns the bucket containing the key 'e'


//Hash policy
um.load_factor();//current load factor
um.max_load_factor();//max load factor; get
um.max_load_factor(0.5)//set
um.rehash(20);//20 -> number of buckets; 20>um.bucket_count() ->rehashed is forced else may not rehash
um.reserve(20);//sets the number of buckets to the most appropriate to contain atleast 20 elements; n>bucket_count*max_load_factor -> bucket_count is increased and rehash is forced else nothing happens

//Observers
unordered_map<char, int>::hasher hashFn = um.hash_function();//hashFn('a');

/* Relational operators
== !=
*/
```

---

## &lt;unordered_map&gt; -> unordered_multimap

[View Index](#stl-components)

- Associative containers (key-value mapping)
- Keys **can have** equivalent values
- Fast retrieval based on keys
- Elements are **not sorted** in any particular order
- Elements are **organized into buckets** based on their **hash values**

```C++
/* Initialization */
pair<char, int>arr[] {{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}};

unordered_multimap<char, int> umm; //empty
unordered_multimap<char, int> umm1({{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}}); //initializer list
unordered_multimap<char, int> umm2(umm1); //copy
unordered_multimap<char, int> umm3(arr, arr + 3); //range
umm = umm1;
umm = {{'a', 1}, {'b', 2}, {'c', 3}, {'d', 4}};


//Capacity
umm.empty();//true|false
umm.size();//number of elements//

/* Iterators
begin, end, cbegin, cend
*/


//Element lookup
unordered_multimap<char, int>::iterator itr = umm.find('c');//returns iterator or umm.end(), *itr.first,*itr.second

umm.count('c');//0 or the count of the element

typedef unordered_multimap<char, int>::iterator itrType;
pair <itrType, itrType> itrPair = umm.equal_range('b');


//Modifiers
umm.clear();

umm.insert({'e', 5});

unordered_multimap<char, int>::iterator itr = umm1.begin();
advance(itr, 2);
umm.insert(umm1.begin(), itr);

umm.insert({{'f', 6}, {'g', 7}});

umm.erase('e');

umm.erase(umm.begin());

itr=umm.begin();
advance(itr,2);
umm.erase(umm.begin(),itr);


//Buckets
/*
A bucket is a slot in the container's internal hash table to which elements are assigned based on the hash value of their key.
*/
int n = umm.bucket_count();//number of buckets
for (int i = 0; i < n; ++i) {
	cout << "bucket #" << i << " contains: ";
	for (auto it = umm.begin(i); it != umm.end(i); ++it)
		cout << "[" << it->first << ":" << it->second << "] ";
	cout << endll;
}

int buckets = umm.bucket_count();
for (int i = 0; i < buckets; ++i) {
	cout << umm.bucket_size(i) << endll;//element in each bucket
}

umm.bucket('e');//returns the bucket containing the key 'e'


//Hash policy
umm.load_factor();//current load factor
umm.max_load_factor();//max load factor; get
umm.max_load_factor(0.5);//set
umm.rehash(20);//20 -> number of buckets; 20>umm.bucket_count() ->rehashed is forced else may not rehash
umm.reserve(20);//sets the number of buckets to the most appropriate to contain atleast 20 elements; n>bucket_count*max_load_factor -> bucket_count is increased and rehash is forced else nothing happens

//Observers
unordered_multimap<char, int>::hasher hashFn = umm.hash_function();//hashFn('a');

/* Relational operators
== !=
*/
```

---

## &lt;unordered_set&gt;

[View Index](#stl-components)

- Stores **unique elements** in **no particular order**
- Elements is its key; Elements are **const**, Cannot be modified once inserted
- **Not sorted** in any particular order
- Elements are organized into **buckets** based on their **hash values**

```C++
/* Initialization */
int arr[] {1, 2, 3, 4, 5};

unordered_set<int> us;
unordered_set<int> us1({1, 2, 3, 4, 5});
unordered_set<int> us2(us1);
unordered_set<int> us3(arr, arr + 3);
us = us1;
us = {5, 6, 7, 8, 9};

//Capacity
us.empty();
us.size();

/* Iterators
begin, end, cbegin, cend
*/

//Element lookup
unordered_set<int>::iterator itr = us.find(8);//itr to element or us.end()
us.count(5);//0 or 1

typedef unordered_set<int>::iterator itrType;
pair<itrType, itrType> itrRange = us.equal_range(6);//gives pair of itr to lowerbound and upperbound

//Modifiers
us.clear();//empty

pair<itrType, bool> temp = us.insert(5);//return <itr,true|false>
itrType itr = us.insert(us.begin(), 10);//hint, value to insert ; returns iterator
us.insert(arr, arr + 3);//range
us.insert({1, 2, 3});

us.erase(2);
us.erase(us.begin());
us.erase(us.begin(), (advance(itr, 2), itr));

//Buckets
us.bucket_count();
us.bucket_size(3);//3<bucket_count; 3->bucket number
us.bucket(2);//2->element

//Hash policy
us.load_factor();
us.max_load_factor();//get
us.max_load_factor(2);//set
us.rehash(10);//10->bucket count; if 10>bucket_count -> rehash is forced with new bucket count >= 10 else no effect
us.reserve(10);//10-> number of elements; sets appropriate numbers of buckets for 10 elements; if 10>bucket_count*max_load_factor -> bucket count is increased and rehash is forced

//Observers
unordered_set<int>::hasher hashFn = us.hash_function();

/* Relational operators
== !=
*/
```

---

## &lt;unordered_set&gt; -> unordered_multiset

[View Index](#stl-components)

- Stores elements in **no particular order**
- Elements **can have** equivalent values
- Elements is its key; Elements are **const**, Cannot be modified once inserted
- **Not sorted** in any particular order
- Elements are organized into **buckets** based on their **hash values**

```C++
/* Initialization */
int arr[] {1, 2, 3, 4, 5};

unordered_multiset<int> ums;
unordered_multiset<int> ums1({1, 2, 3, 4, 5});
unordered_multiset<int> ums2(ums1);
unordered_multiset<int> ums3(arr, arr + 3);
ums = ums1;
ums = {5, 6, 7, 8, 9};

//Capacity
ums.empty();
ums.size();

/* Iterators
begin, end, cbegin, cend
*/

//Element lookup
unordered_multiset<int>::iterator itr = ums.find(8);//itr to element or ums.end()
ums.count(5);//0 or the count

typedef unordered_multiset<int>::iterator itrType;
pair<itrType, itrType> itrRange = ums.equal_range(6);//gives pair of itr to lowerbound and upperbound

//Modifiers
ums.clear();//empty

itrType temp = ums.insert(5);//return <itr,true|false>
itrType itr = ums.insert(ums.begin(), 10);//hint, value to insert ; returns iterator
ums.insert(arr, arr + 3);//range
ums.insert({1, 2, 3});

ums.erase(2);
ums.erase(ums.begin());
ums.erase(ums.begin(), (advance(itr, 2), itr));

//Buckets
ums.bucket_count();
ums.bucket_size(3);//3<bucket_count; 3->bucket number
ums.bucket(2);//2->element

//Hash policy
ums.load_factor();
ums.max_load_factor();//get
ums.max_load_factor(2);//set
ums.rehash(10);//10->bucket count; if 10>bucket_count -> rehash is forced with new bucket count >= 10 else no effect
ums.reserve(10);//10-> number of elements; sets appropriate numbers of buckets for 10 elements; if 10>bucket_count*max_load_factor -> bucket count is increased and rehash is forced

//Observers
unordered_multiset<int>::hasher hashFn = ums.hash_function();

/* Relational operators
== !=
*/
```

---

## &lt;algorithm&gt;

[View Index](#stl-components)

```C++
int arr[] {6, 3, 4, 5, 3, 2, 3, 1};

//Sorting - in range [a,b)
sort(arr, arr + sizeof(arr) / sizeof(int));
sort(arr, arr + sizeof(arr) / sizeof(int),compare);//return true if first element goes before second

//Binary search
lower_bound(arr, arr + size, 5);//returns iterator to an element; elemnt >= 5
lower_bound(arr, arr + size, 5, compare);

upper_bound(arr, arr + size, 5);//element > 5
upper_bound(arr, arr + size, 5, decrease);

pair<itrType, itrType> range = equal_range(arr, arr + size, 5);//gives pair of lowerbound and upperbound for 5
pair<itrType, itrType> range = equal_range(arr, arr + size, 5,compare);

binary_search(arr, arr + size, 0);//returns true|false
binary_search(arr, arr + size, 0,compare);

//Heap
vector<int> v{1, 2, 3, 4, 5};//1 2 3 4 5
make_heap(v.begin(), v.end());//5 4 3 1 2
v.push_back(20);//5 4 3 1 2 20
push_heap(v.begin(), v.end(),compare);//20 4 5 1 2 3
sort_heap(v.begin(), v.end(),compare);//1 2 3 4 5 20
make_heap(v.begin(),v.end(),compare);
pop_heap(v.begin(), v.end(),compare);
v.pop_back();//5 4 3 1 2
is_heap(v.begin(),v.end(),compare);//true|false

min(1,2,compare);
min({1, 2, 3, 4}, compare);
max(1,2,compare);
max({1, 2, 3, 4}, compare);

//Permuations
//returns true|false
prev_permutation(arr, arr + size, compare);//lexicographically smaller permutations
next_permutation(arr, arr + size, compare);//lexicographically larger permutations
```

---

## &lt;string&gt;

[View Index](#stl-components)

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

## &lt;iomanip&gt;

[View Index](#stl-components)

```C++
cout << setbase(16);//sets the base for outputting numbers
cout << setw(10);//sets the width of output
cout<<setfill('x');//sets the fill character for padding
cout << setfill('x') << setw(5);//xx100

cout << setprecision(4);
cout << 100.12345 << endll;//100.1

cout << fixed;
cout << setprecision(2);
cout << 100.12345 << endll;//100.12
```

---

## &lt;limits&gt;

[View Index](#stl-components)

```C++
numeric_limits<T>::max();
numeric_limits<T>::min();
numeric_limits<T>::digits;
numeric_limits<T>::digits10;
```

---

## &lt;utility&gt;

[View Index](#stl-components)

```C++
pair<int, int> p;
pair<int, int> p1(1, 10);
pair<int, int> p2(p1);
p = make_pair(10, 99);
cout << p.first << " " << p.second << endll;
```

---

## &lt;tuple&gt;

[View Index](#stl-components)

```C++
tuple<int, int> t(10, 20);
tuple<int, int, int> t1(1, 2, 3);
tuple<int, int, int, int>t2(1, 2, 3, 4);
tuple<int,int,int>t3(t1);
t2 = make_tuple(7, 8, 9, 0);
get<2>(t1);//3
int a, b, c;
tie(a, b, c) = t4;//a->1,b->2,c->3
```

---

## &lt;bitset&gt;

[View Index](#stl-components)

```C++
bitset<10> b;//0000000000
bitset<10> b1(12345);//0000111001
bitset<10>b2("10101010");//0010101010
cin>>b;
cout<<b;

/* Relational operators
&=,|=,^=,<<=,>>=,~,<<,>>,==,!=,&,|,^
*/

//Bit Access
b1[0]=1;
b.test(0);//0->pos, true|false
b.count();//no of set bits
b.size();//total bits
b.any();//true|false; atleast one bit set
b.none();//true|false; if 0 bits are set
b.all();//true|false; all bit set?

//Bit operations
b.set();//set all bits
b.set(2,0);//make 2nd bit 0
b.reset();//reset all bits
b.reset(2);//reset 2nd bit
b.flip();//flip all bits
b.flip(2);//flip bit at 2nd pos

//Bitset Operations
string s;
s=b.to_string();
unsigned long int uli;
uli = b1.to_ulong();
unsigned long long ulli;
ulli = b1.to_ullong();
```

---

## Functors

[View Index](#stl-components)

- Function objects - Functions wrapped in a class

```C++
class functor {
	int n;
public:
	functor() {
		n = 10;
	}
	functor(int n) {
		this->n = n;
	}
	bool operator()(const int& a, const int& b) {
		if(a<=n and b<=n)
			return a > b;
		return false;
	}
} compare;


bool compareFn(const int& a, const int& b) {
	return a > b;
}

int arr[] {1, 2, 3, 4, 5};
sort(arr, arr + 5, functor(3));//reverse sorting elements <=3
sort(arr, arr + 5, functor());//reverse sorting elements <=10
sort(arr, arr + 5, compare);
sort(arr, arr + 5, compareFn);
```

---
