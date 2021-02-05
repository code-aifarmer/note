 # 一·`部分库函数（随着用随着补充）`
  头文件：#include <ctype.h>  
  函数：
  1.tolower(),toupper()功能：实现大小写字母的转化；  
  2.isdigit()功能：判断是否为数字；  
  3.isalpha()功能:判断是否为字母；  
  4.islower()功能:判断是否为小写字母;  
  5.isupper()功能:判断是否为小写字母;  
# 二.`<algorithm>的常用函数介绍`    
  头文件：#include <algorithm>
  函数：
  1.max(x,y),min(x,y)功能：求出两个数最大和最小的数；  
  2.abs(x);功能：求x的绝对值，类似于<cmath>里面的fabs()函数；  
  3.reverse(begin,end);功能：将区间[begin,end)中的数逆序翻转  
  4.sort(begin,end);功能：将区间[begin,end)中的数排序，默认为增序排序，可自定义cmp()函数的规则进行排序  
  例如 bool cmp(int x,int y){return x>y}则为降序排序。  
  或者对结构体 bool cmp(node a,node b){return a.x>b.x}按照x值从大到小对结构体排序；  
  4.5 stable_sort()功能：与sort一致，区别是stable_sort函数遇到两个数相等时，不对其交换顺序；这个应用在数组里面不受影响，当函数参数传入的是结构体时，会发现两者之间的明显区别；  
  5.lower_bound(first,last,value),upper_bound(first,last,value)功能：  
  他们都要在一个有序数组或有序容器中使用，lower_bound在[first,last)中找第一个值大于等于value的元素的位置,upper_bound在[first,last)中找第一个值大于value的元素的位置，所以返回的是数组的指针或者是容器的迭代器，
  当然只要减去了首地址得到的也就是目标元素的下标了。 时间复杂度均为：O(log(last−first))  
  6.merge(first1,last1,first2,last2,result,cmp(可略写))功能：将两个有序的序列合并为一个有序的序列；  
  7.swap()功能：交换储存在两个对象中的值；  
  8.unique()功能：清除序列中重复的元素，和remove类似，他也不能真正的删除元素；  
  9.fill(first,end,x)功能：fill函数可以将数组或者是容器中的某一区间赋予某个相同的值，与memset函数不同的是，这里的赋值可以是数组类型对应范围中的任意值；  
# 三`STL详细用法介绍`：  
## 1.什么是STL?  
1.1STL（Standard Template Library），即标准模板库，是一个具有工业强度的，高效的C++程序库。它被容纳于C++标准程序库（C++ Standard Library）中，是ANSI/ISO C++标准中最新的也是极具革命性的一部分。该库包含了诸多在计算机科学领域里所常用的基本数据结构和基本算法。为广大C++程序员们提供了一个可扩展的应用框架，高度体现了软件的可复用性。  
1.2从逻辑层次来看，在STL中体现了泛型化程序设计的思想，引入了诸多新的名词，比如像需求（requirements），概念（concept），模型（model），容器（container），算法（algorithmn），迭代子（iterator）等。与OOP（object-oriented programming）中的多态（polymorphism）一样，泛型也是一种软件的复用技术；  
1.3从实现层次看，整个STL是以一种类型参数化的方式实现的，这种方式基于一个在早先C++标准中没有出现的语言特性--模板（template）。
## `STL内容介绍`:  
2.STL中六大组件：  
2.1容器（Container），是一种数据结构，如list，vector，和deques ，以模板类的方法提供。为了访问容器中的数据，可以使用由容器类输出的迭代器；  
2.2迭代器（Iterator），提供了访问容器中对象的方法。例如，可以使用一对迭代器指定list或vector中的一定范围的对象。迭代器就如同一个指针。事实上，C++的指针也是一种迭代器。但是，迭代器也可以是那些定义了operator*()以及其他类似于指针的操作符地方法的类对象；  
2.3算法（Algorithm），是用来操作容器中的数据的模板函数。例如，STL用sort()来对一个vector中的数据进行排序，用find()来搜索一个list中的对象，函数本身与他们操作的数据的结构和类型无关，因此他们可以在从简单数组到高度复杂容器的任何数据结构上使用；  
2.4仿函数（Functor）  
2.5适配器（Adaptor）  
2.6分配器（allocator）  
### `容器`：
STL中的容器有队列容器和关联容器，容器适配器（congtainer adapters：stack,queue，priority queue），位集（bit_set），串包(string_package)等等。  
#### 2.1.1 序列式容器：（Sequence containers），每个元素都有固定位置－－取决于插入时机和地点，和元素值无关，vector、deque、list；  
2.1.1.1 vector:将元素置于一个动态数组中加以管理，可以随机存取元素（用索引直接存取），数组尾部添加或移除元素非常快速。但是在中部或头部安插元素比较费时；  
2.1.1.2 Deque：是“double-ended queue”的缩写，可以随机存取元素（用索引直接存取），数组头部和尾部添加或移除元素都非常快速。但是在中部或头部安插元素比较费时；  
2.1.1.3 List：双向链表，不提供随机存取（按顺序走到需存取的元素，O(n)），在任何位置上执行插入或删除动作都非常迅速，内部只需调整一下指针；  
#### 2.1.2 关联式容器（Associated containers），元素位置取决于特定的排序准则，和插入顺序无关，set、multiset、map、multimap等。  
2.1.2.1 Set/Multiset：内部的元素依据其值自动排序，Set内的相同数值的元素只能出现一次，Multisets内可包含多个数值相同的元素，内部由二叉树实现，便于查找；  
2.1.2.2  Map/Multimap：Map的元素是成对的键值/实值，内部的元素依据其值自动排序，Map内的相同数值的元素只能出现一次，Multimaps内可包含多个数值相同的元素，内部由二叉树实现，便于查找；
容器类自动申请和释放内存，无需new和delete操作。  
### `STL迭代器`  
Iterator（迭代器）模式又称Cursor（游标）模式，用于提供一种方法顺序访问一个聚合对象中各个元素, 而又不需暴露该对象的内部表示。或者这样说可能更容易理解：Iterator模式是运用于聚合对象的一种模式，通过运用该模式，使得我们可以在不知道对象内部表示的情况下，按照一定顺序（由iterator提供的方法）访问聚合对象中的各个元素。    
迭代器的作用：能够让迭代器与算法不干扰的相互发展，最后又能无间隙的粘合起来，重载了*，＋＋，＝＝，！＝，＝运算符。用以操作复杂的数据结构，容器提供迭代器，算法使用迭代器；常见的一些迭代器类型：iterator、const_iterator、reverse_iterator和const_reverse_iterator.
### `算法`  
算法部分主要由头文件<algorithm>，<numeric>和<functional>组成。  
<algorithm>是所有STL头文件中最大的一个（尽管它很好理解），它是由一大堆模版函数组成的，可以认为每个函数在很大程度上都是独立的，其中常用到的功能范围涉及到比较、交换、查找、遍历操作、复制、修改、移除、反转、排序、合并等等。
<numeric>体积很小，只包括几个在序列上面进行简单数学运算的模板函数，包括加法和乘法在序列上的一些操作。
<functional>中则定义了一些模板类，用以声明函数对象。  
STL中算法大致分为四类：  
1.非可变序列算法：指不直接修改其所操作的容器内容的算法。  
2.可变序列算法：指可以修改它们所操作的容器内容的算法。  
3.排序算法：对序列进行排序和合并的算法、搜索算法以及有序序列上的集合操作。  
4.数值算法：对容器内容进行数值计算。 
#### `查找算法`(13个)：  
`adjacent_find`:在iterator对标识元素范围内，查找一对相邻重复元素，找到则返回指向这对元素的第一个元素的ForwardIterator。否则返回last。重载版本使用输入的二元操作符代替相等的判断。  
`binary_search`:在有序序列中查找value，找到返回true。重载的版本实用指定的比较函数对象或函数指针来判断相等。  
`count`:利用等于操作符，把标志范围内的元素与输入值比较，返回相等元素个数。  
`count_if`:利用输入的操作符，对标志范围内的元素进行操作，返回结果为true的个数。
`equal_range`:功能类似equal，返回一对iterator，第一个表示lower_bound，第二个表示upper_bound。  
`find`:利用底层元素的等于操作符，对指定范围内的元素与输入值进行比较。当匹配时，结束搜索，返回该元素的一个InputIterator。  
`find_end`:在指定范围内查找"由输入的另外一对iterator标志的第二个序列"的最后一次出现。找到则返回最后一对的第一个ForwardIterator，否则返回输入的"另外一对"的第一个ForwardIterator。重载版本使用用户输入的操作符代替等于操作。  
`find_first_of`:在指定范围内查找"由输入的另外一对iterator标志的第二个序列"中任意一个元素的第一次出现。重载版本中使用了用户自定义操作符。  
`find_if`:使用输入的函数代替等于操作符执行find。  
`lower_bound`:返回一个ForwardIterator，指向在有序序列范围内的可以插入指定值而不破坏容器顺序的第一个位置。重载函数使用自定义比较操作。  
`upper_bound`:返回一个ForwardIterator，指向在有序序列范围内插入value而不破坏容器顺序的最后一个位置，该位置标志一个大于value的值。重载函数使用自定义比较操作。  
`search`:给出两个范围，返回一个ForwardIterator，查找成功指向第一个范围内第一次出现子序列(第二个范围)的位置，查找失败指向last1。重载版本使用自定义的比较操作。  
`search_n`:在指定范围内查找val出现n次的子序列。重载版本使用自定义的比较操作。  
#### `排序算法`（13个):  
`inplace_merge`:合并两个有序序列，结果序列覆盖两端范围。重载版本使用输入的操作进行排序。  
`merge`:合并两个有序序列，存放到另一个序列。重载版本使用自定义的比较。  
`partial_sort`:对序列做部分排序，被排序元素个数正好可以被放到范围内。重载版本使用自定义的比较操作。  
`partial_sort_copy`: 与partial_sort类似，不过将经过排序的序列复制到另一个容器。  
`partition`:对指定范围内元素重新排序，使用输入的函数，把结果为true的元素放在结果为false的元素之前。  
`random_shuffle`:对指定范围内的元素随机调整次序。重载版本输入一个随机数产生操作。  
`reverse`:将指定范围内元素重新反序排序。  
`reverse_copy`:与reverse类似，不过将结果写入另一个容器。  
`rotate`:将指定范围内元素移到容器末尾，由middle指向的元素成为容器第一个元素。  
`rotate_copy`:与rotate类似，不过将结果写入另一个容器。  
`sort`:以升序重新排列指定范围内的元素。重载版本使用自定义的比较操作。  
`stable_sort`:与sort类似，不过保留相等元素之间的顺序关系。  
`stable_partition`:与partition类似，不过不保证保留容器中的相对顺序。  
#### `删除和替换算法`(15个):  
`copy`:复制序列
`copy_backward`: 与copy相同，不过元素是以相反顺序被拷贝。  
`iter_swap`:交换两个ForwardIterator的值。  
`remove`:删除指定范围内所有等于指定元素的元素。注意，该函数不是真正删除函数。内置函数不适合使用remove和remove_if函数。  
`remove_copy`:将所有不匹配元素复制到一个制定容器，返回OutputIterator指向被拷贝的末元素的下一个位置。  
`remove_if`:删除指定范围内输入操作结果为true的所有元素。  
`remove_copy_if`: 将所有不匹配元素拷贝到一个指定容器。  
`replace`:将指定范围内所有等于vold的元素都用vnew代替。  
`replace_copy`:与replace类似，不过将结果写入另一个容器。  
`replace_if`:将指定范围内所有操作结果为true的元素用新值代替。  
`replace_copy_if`: 与replace_if，不过将结果写入另一个容器。  
`swap`:交换存储在两个对象中的值。  
`swap_range`:将指定范围内的元素与另一个序列元素值进行交换。  
`unique`:清除序列中重复元素，和remove类似，它也不能真正删除元素。重载版本使用自定义比较操作。  
`unique_copy`:与unique类似，不过把结果输出到另一个容器。  
#### `排列组合算法(2个)：提供计算给定集合按一定顺序的所有可能排列组合`:  
`next_permutation`: 取出当前范围内的排列，并重新排序为下一个排列。重载版本使用自定义的比较操作。  
`prev_permutation`: 取出指定范围内的序列并将它重新排序为上一个序列。如果不存在上一个序列则返回false。重载版本使用自定义的比较操作。  
#### `算术算法(4个)`:  
`accumulate`:iterator对标识的序列段元素之和，加到一个由val指定的初始值上。重载版本不再做加法，而是传进来的二元操作符被应用到元素上。  
`partial_sum`:创建一个新序列，其中每个元素值代表指定范围内该位置前所有元素之和。重载版本使用自定义操作代替加法。  
`inner_product`:对两个序列做内积(对应元素相乘，再求和)并将内积加到一个输入的初始值上。重载版本使用用户定义的操作。  
`adjacent_difference`: 创建一个新序列，新序列中每个新值代表当前元素与上一个元素的差。重载版本用指定二元操作计算相邻元素的差。  
#### `生成和异变算法(6个)`:  
`fill`:将输入值赋给标志范围内的所有元素。  
`fill_n`:将输入值赋给first到first+n范围内的所有元素。  
`for_each`:用指定函数依次对指定范围内所有元素进行迭代访问，返回所指定的函数类型。该函数不得修改序列中的元素。  
`generate`:连续调用输入的函数来填充指定的范围。  
`generate_n`:与generate函数类似，填充从指定iterator开始的n个元素。  
`transform`:将输入的操作作用与指定范围内的每个元素，并产生一个新的序列。重载版本将操作作用在一对元素上，另外一个元素来自输入的另外一个序列。结果输出到指定容器。  
#### `关系算法(8个)`:  
`equal`:如果两个序列在标志范围内元素都相等，返回true。重载版本使用输入的操作符代替默认的等于操作符。  
`includes`:判断第一个指定范围内的所有元素是否都被第二个范围包含，使用底层元素的<操作符，成功返回true。重载版本使用用户输入的函数。  
`lexicographical_compare`: 比较两个序列。重载版本使用用户自定义比较操作。  
`max:返回两个元素中较大一个`。重载版本使用自定义比较操作。  
`max_element`:返回一个ForwardIterator，指出序列中最大的元素。重载版本使用自定义比较操作。  
`min`:返回两个元素中较小一个。重载版本使用自定义比较操作。  
`min_element`:返回一个ForwardIterator，指出序列中最小的元素。重载版本使用自定义比较操作。  
`mismatch`:并行比较两个序列，指出第一个不匹配的位置，返回一对iterator，标志第一个不匹配元素位置。如果都匹配，返回每个容器的last。重载版本使用自定义的比较操作。  
#### `集合算法(4个)`:  
`set_union`:构造一个有序序列，包含两个序列中所有的不重复元素。重载版本使用自定义的比较操作。  
`set_intersection`:构造一个有序序列，其中元素在两个序列中都存在。重载版本使用自定义的比较操作。    
`set_difference`:构造一个有序序列，该序列仅保留第一个序列中存在的而第二个中不存在的元素。重载版本使用自定义的比较操作。  
`set_symmetric_difference`: 构造一个有序序列，该序列取两个序列的对称差集(并集-交集)。  
#### `堆算法(4个)`:  
`make_heap`:把指定范围内的元素生成一个堆。重载版本使用自定义比较操作。    
`pop_heap`:并不真正把最大元素从堆中弹出，而是重新排序堆。它把first和last-1交换，然后重新生成一个堆。可使用容器的back来访问被"弹出"的元素或者使用pop_back进行真正的删除。重载版本使用自定义的比较操作。  
`push_heap`:假设first到last-1是一个有效堆，要被加入到堆的元素存放在位置last-1，重新生成堆。在指向该函数前，必须先把元素插入容器后。重载版本使用指定的比较操作。  
`sort_heap`:对指定范围内的序列重新排序，它假设该序列是个有序堆。重载版本使用自定义比较操作。  
### `仿函数`:  
仿函数(functor)，就是使一个类的使用看上去象一个函数。其实现就是类中实现一个operator()，这个类就有了类似函数的行为，就是一个仿函数类了。有些功能的的代码，会在不同的成员函数中用到，想复用这些代码。    
1）公共的函数，可以，这是一个解决方法，不过函数用到的一些变量，就可能成为公共的全局变量，再说为了复用这么一片代码，就要单立出一个函数，也不是很好维护。    
2）仿函数，写一个简单类，除了那些维护一个类的成员函数外，就只是实现一个operator()，在类实例化时，就将要用的，非参数的元素传入类中。  
#### ` 仿函数在STL中的定义`:  
##### `要使用STL内建的仿函数，必须包含<functional>头文件。而头文件中包含的仿函数分类包括`:
1）算术类仿函数  
加：plus<T>  
减：minus<T>  
乘：multiplies<T>  
除：divides<T>  
模取：modulus<T>  
否定：negate<T>  
2）关系运算类仿函数  
等于：equal_to<T>  
不等于：not_equal_to<T>  
大于：greater<T>  
大于等于：greater_equal<T>  
小于：less<T>  
小于等于：less_equal<T>  
3）逻辑运算仿函数  
逻辑与：logical_and<T>  
逻辑或：logical_or<T>  
逻辑否：logical_no<T>  
### `容器适配器`:  
`标准库提供了三种顺序容器适配器：queue(FIFO队列)、priority_queue(优先级队列)、stack(栈)`  
适配器是使一种事物的行为类似于另外一种事物行为的一种机制，适配器对容器进行包装，使其表现出另外一种行为。例如，stack<int, vector<int> >实现了栈的功能，但其内部使用顺序容器vector<int>来存储数据。（相当于是vector<int>表现出了栈的行为）。  
要使用适配器，需要加入一下头文件：  
#include <stack>//stack  
#include<queue>//queue、priority_queue  
1、初始化  
stack<int> stk(dep);  
2、覆盖默认容器类型  
stack<int,vector<int> > stk;  
使用适配器  
stack<int> s;  
stack< int, vector<int> > stk;  //覆盖基础容器类型，使用vector实现stk  
s.empty();  //判断stack是否为空，为空返回true，否则返回false  
s.size();   //返回stack中元素的个数  
s.pop();    //删除栈顶元素，但不返回其值  
s.top();    //返回栈顶元素的值，但不删除此元素  
s.push(item);   //在栈顶压入新元素item  
### `常用容器用法介绍 `:  
#### `vector`:  
1.构造函数  
vector():创建一个空vector  
vector(int nSize):创建一个vector,元素个数为nSize  
vector(int nSize,const t& t):创建一个vector，元素个数为nSize,且值均为t  
vector(const vector&):复制构造函数  
vector(begin,end):复制[begin,end)区间内另一个数组的元素到vector中  
2.增加函数  
void push_back(const T& x):向量尾部增加一个元素X  
iterator insert(iterator it,const T& x):向量中迭代器指向元素前增加一个元素x  
iterator insert(iterator it,int n,const T& x):向量中迭代器指向元素前增加n个相同的元素x  
iterator insert(iterator it,const_iterator first,const_iterator last):向量中迭代器指向元素前插入另一个相同类型向量的[first,last)间的数据  
3.删除函数  
iterator erase(iterator it):删除向量中迭代器指向元素  
iterator erase(iterator first,iterator last):删除向量中[first,last)中元素  
void pop_back():删除向量中最后一个元素  
void clear():清空向量中所有元素  
4.遍历函数  
reference at(int pos):返回pos位置元素的引用  
reference front():返回首元素的引用  
reference back():返回尾元素的引用  
iterator begin():返回向量头指针，指向第一个元素  
iterator end():返回向量尾指针，指向向量最后一个元素的下一个位置  
reverse_iterator rbegin():反向迭代器，指向最后一个元素  
reverse_iterator rend():反向迭代器，指向第一个元素之前的位置  
5.判断函数  
bool empty() const:判断向量是否为空，若为空，则向量中无元素  
6.大小函数  
int size() const:返回向量中元素的个数  
int capacity() const:返回当前向量张红所能容纳的最大元素值  
int max_size() const:返回最大可允许的vector元素数量值  
7.其他函数  
void swap(vector&):交换两个同类型向量的数据  
void assign(int n,const T& x):设置向量中第n个元素的值为x  
void assign(const_iterator first,const_iterator last):向量中[first,last)中元素设置成当前向量元素  
#### `deque`:
所谓的deque是”double ended queue”的缩写，双端队列不论在尾部或头部插入元素，都十分迅速。而在中间插入元素则会比较费时，因为必须移动中间其他的元素。双端队列是一种随机访问的数据类型，提供了在序列两端快速插入和删除操作的功能，它可以在需要的时候改变自身大小，完成了标准的C++数据结构中队列的所有功能。     
#include<deque>  // 头文件  
deque<type> deq;  // 声明一个元素类型为type的双端队列que  
deque<type> deq(size);  // 声明一个类型为type、含有size个默认值初始化元素的的双端队列que  
deque<type> deq(size, value);  // 声明一个元素类型为type、含有size个value元素的双端队列que  
deque<type> deq(mydeque);  // deq是mydeque的一个副本  
deque<type> deq(first, last);  // 使用迭代器first、last范围内的元素初始化deq  
##### `deque的常用成员函数`:  
deq[ ]：用来访问双向队列中单个的元素。  
deq.front()：返回第一个元素的引用。  
deq.back()：返回最后一个元素的引用。  
deq.push_front(x)：把元素x插入到双向队列的头部。  
deq.pop_front()：弹出双向队列的第一个元素。  
deq.push_back(x)：把元素x插入到双向队列的尾部。  
deq.pop_back()：弹出双向队列的最后一个元素。  
##### `deque的一些特点`:  
支持随机访问，即支持[ ]以及at()，但是性能没有vector好。  
可以在内部进行插入和删除操作，但性能不及list。  
deque两端都能够快速插入和删除元素，而vector只能在尾端进行。  
deque的元素存取和迭代器操作会稍微慢一些，因为deque的内部结构会多一个间接过程。  
deque迭代器是特殊的智能指针，而不是一般指针，它需要在不同的区块之间跳转。  
deque可以包含更多的元素，其max_size可能更大，因为不止使用一块内存。  
deque不支持对容量和内存分配时机的控制。  
在除了首尾两端的其他地方插入和删除元素，都将会导致指向deque元素的任何pointers、references、iterators失效。不过，deque的内存重分配优于vector，因为其内部结构显示不需要复制所有元素。  
deque的内存区块不再被使用时，会被释放，deque的内存大小是可缩减的。不过，是不是这么做以及怎么做由实际操作版本定义。  
deque不提供容量操作：capacity()和reverse()，但是vector可以。  
#### `list`:  
List是stl实现的双向链表，与向量(vectors)相比, 它允许快速的插入和删除，但是随机访问却比较慢。使用时需要添加头文件  
#include <list>  
##### `list定义和初始化`:    
list<int>lst1;          //创建空list  
list<int> lst2(5);       //创建含有5个元素的list  
list<int>lst3(3,2);  //创建含有3个元素的list  
list<int>lst4(lst2);    //使用lst2初始化lst4  
list<int>lst5(lst2.begin(),lst2.end());  //同lst4  
##### ` list常用操作函数`:  
Lst1.assign() 给list赋值   
Lst1.back() 返回最后一个元素   
Lst1.begin() 返回指向第一个元素的迭代器   
Lst1.clear() 删除所有元素   
Lst1.empty() 如果list是空的则返回true   
Lst1.end() 返回末尾的迭代器   
Lst1.erase() 删除一个元素   
Lst1.front() 返回第一个元素   
Lst1.get_allocator() 返回list的配置器   
Lst1.insert() 插入一个元素到list中   
Lst1.max_size() 返回list能容纳的最大元素数量   
Lst1.merge() 合并两个list   
Lst1.pop_back() 删除最后一个元素   
Lst1.pop_front() 删除第一个元素   
Lst1.push_back() 在list的末尾添加一个元素   
Lst1.push_front() 在list的头部添加一个元素   
Lst1.rbegin() 返回指向第一个元素的逆向迭代器   
Lst1.remove() 从list删除元素   
Lst1.remove_if() 按指定条件删除元素   
Lst1.rend() 指向list末尾的逆向迭代器   
Lst1.resize() 改变list的大小   
Lst1.reverse() 把list的元素倒转   
Lst1.size() 返回list中的元素个数   
Lst1.sort() 给list排序   
Lst1.splice() 合并两个list   
Lst1.swap() 交换两个list   
Lst1.unique() 删除list中相邻重复的元素  
#### `map/multimap`:  
map和multimap都需要#include<map>，唯一的不同是，map的键值key不可重复，而multimap可以，也正是由于这种区别，map支持[ ]运算符，multimap不支持[ ]运算符。在用法上没什么区别。

C++中map提供的是一种键值对容器，里面的数据都是成对出现的,如下图：每一对中的第一个值称之为关键字(key)，每个关键字只能在map中出现一次；第二个称之为该关键字的对应值。  
Map是STL的一个关联容器，它提供一对一（其中第一个可以称为关键字，每个关键字只能在map中出现一次，第二个可能称为该关键字的值）的数据 处理能力，由于这个特性，它完成有可能在我们处理一对一数据的时候，在编程上提供快速通道。这里说下map内部数据的组织，map内部自建一颗红黑树(一 种非严格意义上的平衡二叉树)，这颗树具有对数据自动排序的功能，所以在map内部所有的数据都是有序的。  
##### `基本操作函数`"    
     begin()         返回指向map头部的迭代器  

     clear(）        删除所有元素  

     count()         返回指定元素出现的次数  

     empty()         如果map为空则返回true  

     end()           返回指向map末尾的迭代器  

     equal_range()   返回特殊条目的迭代器对  

     erase()         删除一个元素  

     find()          查找一个元素  

     get_allocator() 返回map的配置器  

     insert()        插入元素  

     key_comp()      返回比较元素key的函数  

     lower_bound()   返回键值>=给定元素的第一个位置  

     max_size()      返回可以容纳的最大元素个数  

     rbegin()        返回一个指向map尾部的逆向迭代器  

     rend()          返回一个指向map头部的逆向迭代器  

     size()          返回map中元素的个数  

     swap()           交换两个map  

     upper_bound()    返回键值>给定元素的第一个位置  

     value_comp()     返回比较元素value的函数  
##### `声明`:  
#include<map>
 
map<int, string> ID_Name;
 
// 使用{}赋值是从c++11开始的，因此编译器版本过低时会报错，如visual studio 2012  
map<int, string> ID_Name = {  
                { 2015, "Jim" },  
                { 2016, "Tom" },  
                { 2017, "Bob" } };  
#### ` set/multiset `:  
std::set 是关联容器，含有 Key 类型对象的已排序集。用比较函数compare进行排序。搜索、移除和插入拥有对数复杂度。 set 通常以红黑树实现。

set容器内的元素会被自动排序，set与map不同，set中的元素即是键值又是实值，set不允许两个元素有相同的键值。不能通过set的迭代器去修改set元素，原因是修改元素会破坏set组织。当对容器中的元素进行插入或者删除时，操作之前的所有迭代器在操作之后依然有效。  
multiset特性及用法和set完全相同，唯一的差别在于它允许键值重复。set和multiset的底层实现是一种高效的平衡二叉树，即红黑树（Red-Black Tree）。  
##### ` set常用成员函数`:  
1. begin()--返回指向第一个元素的迭代器  

2. clear()--清除所有元素  

3. count()--返回某个值元素的个数  

4. empty()--如果集合为空，返回true  

5. end()--返回指向最后一个元素的迭代器  

6. equal_range()--返回集合中与给定值相等的上下限的两个迭代器  

7. erase()--删除集合中的元素  

8. find()--返回一个指向被查找到元素的迭代器  

9. get_allocator()--返回集合的分配器  

10. insert()--在集合中插入元素  

11. lower_bound()--返回指向大于（或等于）某值的第一个元素的迭代器  

12. key_comp()--返回一个用于元素间值比较的函数  

13. max_size()--返回集合能容纳的元素的最大限值  

14. rbegin()--返回指向集合中最后一个元素的反向迭代器  

15. rend()--返回指向集合中第一个元素的反向迭代器  

16. size()--集合中元素的数目  

17. swap()--交换两个集合变量  

18. upper_bound()--返回大于某个值元素的迭代器  

19. value_comp()--返回一个用于比较元素间的值的函数  

                

