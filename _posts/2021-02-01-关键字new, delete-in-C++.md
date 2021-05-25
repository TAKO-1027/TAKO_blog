---
*d
categories:

   C++

title:  "关键字new, delete-in-C++"

---

# new, delete

new 是一个operator，与+，-等地位相同，所以new可以被重载。

```{C++}
int a = 2;
int *b = new int;
int *c = new int(4);
int *d = new int[50];
int *p = new Classname();

delete b;
delete c;
delete[] d;
delete p;

//简化程序
typedef int* IntPtr;

IntPtr a = new int;
```

