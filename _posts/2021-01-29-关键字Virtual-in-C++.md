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

