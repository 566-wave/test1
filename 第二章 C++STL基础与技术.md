# 第二章 C++STL基础与技术

## 2.2函数模板

代码示例如下：

```c++
#include <iostream>
using namespace std;
template <class T>
T max(T, T);
int main()
{
	int a = 5;
	int b = 3;
	cout << max(a, b)<<endl;
	float c = 10.6;
	float d = 3.89;
	cout << max(c, d) << endl;
	char e = 'A';
	char f = 'B';
	cout << max(e, f) << endl;
	system("pause");
	return 0;
}
template <class T>
T max(T a,T b)
{
	if (a > b)
		return a;
	return b;
}

```

要注意，对于应用模板的函数的声明与定义，都要在前边加上 template<class T>这句话。否则编译不通过。

函数模板中使用多种类型：

```c++
#include <iostream>
using namespace std;
template <class T1,class T2>
void swap(T1& , T2& );
int main()
{
	int a = 3;
	double b = 4.5;
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;
	swap(a, b);
	cout << "交换后" << endl;
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;
	system("pause");
	return 0;
}
template <class T1,class T2>
void swap(T1& a, T2& b)
{
	T1 t = a;
	a = (T1)b;
	b = (T2)t;
}
```

## 2.3 类模板

```C++
#include <iostream>
using namespace std;
const int n = 10;
template <class T>
class Stack
{
private:
	int top;
	T stack[n];
	Stack()
	{
		top = -1;
	}
public:
	//入栈函数
	void push(T);
	//出栈函数
	T pop();
};
template <class T>
void Stack<T>::push(T num)
{
	if (top != n - 1)
	{
		stack[++top] = num;
	}
}
template <class T>
T Stack::pop()
{
	return stack[top--];
}

```

## 模板的特化

对于模板的泛化，如果判断(a==b)这种语句，那么模板的泛化只能针对例如char和int的这种数据有效果。当变量是字符数组时，则无法使用运算符==来比较，所以针对特定的数据类型要编写特定的程序代码加以处理。这就是函数模板的特化。

```C++
template <>
bool IsEqual(char* t1,char* t2)
{
 	if(strcmp(t1,t2)==0)
        return true;
    return false;
}
```

