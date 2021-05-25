---

categories:

   C++

title:  "关键字Virtual-in-C++"

---

# 虚函数

Virtual在C++中为虚函数，在面向对象程序设计中的继承和多态使用。虚函数在父类中声明(declearation)，函数和方法在子类中被覆盖(override)。通过virtual关键字可以获得run-time polymorphism。总而言之，虚函数指出有一个方法可以调用，但具体调用哪个方法在运行时才能知道。



Virtual在子类中可写可不写，继承的virtual方法也会变成virtual 方法，写virtual override增加可读性。

```{C++}
class Animal
{
    public:
        void eat() { std::cout << "I'm eating generic food."; }
};

class Cat : public Animal
{
    public:
        void eat() { std::cout << "I'm eating a rat."; }
};

int main(){
Animal *animal = new Animal;
Cat *cat = new Cat;

animal->eat(); // Outputs: "I'm eating generic food."
cat->eat();    // Outputs: "I'm eating a rat."
}

// Passing in a Animal pointer, without virtual function, this pointer invoke Animal.eat(), early binding.
void func(Animal *xyz) { xyz->eat(); }
Now our main function is:

Animal *animal = new Animal;
Cat *cat = new Cat;

func(animal); // Outputs: "I'm eating generic food."
func(cat);    // Outputs: "I'm eating generic food."


// however, with virtual function we have late binding
class Animal
{
    public:
        virtual void eat() { std::cout << "I'm eating generic food."; }
};

class Cat : public Animal
{
    public:
        void eat() { std::cout << "I'm eating a rat."; }
};
Main:

func(animal); // Outputs: "I'm eating generic food."
func(cat);    // Outputs: "I'm eating a rat."
```

# 纯虚函数

纯虚函数是在基类中声明的虚函数，它在基类中没有定义，但要求任何派生类都要定义自己的实现方法。在基类中实现纯虚函数的方法是在函数原型后加 =0。

```{C++}
virtual void func()=0
```

在父类中定义纯虚函数，子类必须重载以实现多态性。

定义了纯虚函数的类称为抽象类，不能生成对象。继承了纯虚函数但是没有重载的派生类还是抽象类，无法建立具体的对象。

定义虚函数的目的只是声明一个接口，告诉子类的设计者，你必须提供一个纯虚函数的实现，但是我不知道你会怎样实现它。

# 虚拟Destructor

拥有虚函数的基类需要定义虚拟Destructor。原因如下：

```{C++}
class num_sequence { 
public: 
virtual ~num_sequence(); 
// ... 
};

class Fibonacci: public num_sequence{
public:
  virtual ~Fibonacci();
  //...
}

num_sequence *ps = new Fibonacci(12); 
// ... use the sequence 
delete ps;

/*此刻需要动态绑定，调用Fibonacci的Destructor而不是num_sequence的。*/
```





