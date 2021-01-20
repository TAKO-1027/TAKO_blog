---

categories:

   C++

title:  "关键字Static in C++"

---



Static关键字分为面向过程和面向对象，在两种模式下有不同的意思。

---

面向过程：

Static关键字声明后生活周期是从运行block开始直到程序结束，只定义一次，可见性只限制在当前block或translation unit。

1. 全局静态变量（Static Global Variable）

   ```{C++}
   /*全局静态变量在当前translation unit只定义一次，在程序运行时存储，结束时消失。
     并且只对当前translation unit可见*/
   
   // main.cpp
   int main(){
   	int a = 10;
   }
   
   // stat.cpp 有相同名称的变量会有duplicate error，可以用static关键字使a变量在文件层面变成“private”
   int a = 20;
   
   ```

2. 局部静态变量（Static Local Variable）

   ```{C++}
   /*局部静态变量在当前translation unit只定义一次，在程序运行时存储，结束时消失。
     并且只对当前block可见，作用域不变*/
   
   // main.cpp
   void foo(){
     static int timer = 0;
     timer++;
     std::cout<<timer;
   }
   
   int main(){
       foo();
       foo();
       foo();
   }
   //输出为1，2，3
   ```

   

3. 静态函数（Static Function）

   ```{C++}
   /*静态函数只对当前Translation Unit可见，对其他文件不可见*/
   // stat.cpp
   static void Function(){
     std::cout<<"Hello,world";
   }
   
   
   // main.cpp
   int main(){
     Function();
   }
   
   //error, main.cpp cannot access the static void Function, you should delete the static and add extern declearation in main.cpp
   ```

---

面向对象：

在类中的Static关键字被称为静态成员，一个类的静态成员与类的对象不绑定，静态成员是独立的。static关键字只在声明时使用，定义时不需要static

4. 类静态成员（Class Static Member）

   ```{C++
   class MyClass {
   private:
     static int n; 
   }; // declaration (uses 'static')
   
   int MyClass::n = 1;              // definition (does not use 'static')
   
   
   /*static member are share by the objects and have the same value*/
   ```

   }

5. 类静态方法（Class Static Methods）

   ```{C++}
   /*Static member functions are not associated with any object. When called, they have no this pointer.
   
   Static member functions cannot be virtual, const, or volatile.*
   
   A static member function can only access static member data, static member functions and data and functions outside the class.*/
   
   #include <iostream>
   using namespace std;
   
   class Student{
   private:
      char *name;
      int age;
      float score;
      static int num;  	//student amounts
      static float total;  //total score
   public:
      Student(char *, int, float);
      void say();
      static float getAverage();  //average score
   };
   
   int Student::num = 0;
   float Student::total = 0;
   
   Student::Student(char *name, int age, float score)
   {
      this->name = name;
      this->age = age;
      this->score = score;
      num++;
      total += score;
   }
   
   void Student::say()
   {
      cout<<name<<"age: "<<age<<"，score: "<<score<<"（total"<<num<<"students）"<<endl;
   }
   
   float Student::getAverage()
   {
      return total / num;
   }
   ```

   