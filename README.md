# General-IT-Knowledge
## Object-Oriented Programming
### Inheritance (Kế thừa)
*Khái niệm*: Cho phép một hoặc nhiều lớp (`Derived class` - Lớp dẫn xuất) <b>kế thừa thuộc tính và phương thức của một lớp khác</b> (`Base class` - Lớp cơ sở) để tăng khả năng tái sử dụng và giảm thiểu việc lặp lại code. 

Ví dụ trong C#, ta có 1 lớp cha Phone là base class:
```
public class Phone // Base class
{
    public string? name;

    public void runGames()
    {
        Console.WriteLine($"{name} can run any games smoothly.");
    }
}
```
Ta có các lớp con là iPhone, Samsung,... là derived class thừa kế các thuộc tính của lớp cha Phone:
```
public class iPhone : Phone // Derived Class
{
   public void iPhonesCameras()
   {
       Console.WriteLine($"Cameras of {name} are great.");
   }
}

public class Samsung : Phone // Derived Class
{
    public void SamsungsDesigns()
    {
        Console.WriteLine($"Design of {name} is beautiful.");
    }
}
```
Ta tạo các dòng máy ở hàm chính:
```
iPhone myiPhone1 = new iPhone();
iPhone myiPhone2 = new iPhone();
Samsung mySamsung = new Samsung();

myiPhone1.name = "iPhone 15 Pro";
myiPhone2.name = "iPhone 15 Pro Max";
mySamsung.name = "Samsung Galaxy Note 10";

myiPhone1.runGames(); // iPhone 15 Pro can run any games smoothly.
myiPhone1.iPhonesCameras(); // Cameras of iPhone 15 Pro are great.
myiPhone2.iPhonesCameras(); // Cameras of iPhone 15 Pro Max are great.
mySamsung.runGames(); // Samsung Galaxy Note 10 can run any games smoothly.
mySamsung.SamsungsDesigns(); // Design of Samsung Galaxy Note 10 is beautiful.
```

Có 5 loại kế thừa (Đọc thêm):                                     
* <b>Đơn kế thừa</b> (Single inheritance).                               
* <b>Đa kế thừa</b> (Multiple inheritance).                              
* <b>Kế thừa đa cấp</b> (Multi-level inheritance).                       
* <b>Kế thừa phân cấp</b> (Hierachical inheritance).                     
* <b>Kế thừa lai</b> (Hybrid inheritance).

### Encapsulation (Đóng gói)
*Khái niệm*: <b>Che giấu thông tin chi tiết của các đối tượng, chỉ cho phép truy cập thông qua phương thức public</b>. Tính chất này giúp tăng tính bảo mật cho đối tượng và tránh tình trạng dữ liệu bị hư hỏng ngoài ý muốn, giúp duy trì tính ổn định và độ tin cậy của chương trình. 

Tính đóng gói được khai triển bằng cách sử dụng Access modifier, gồm:
* `public`: Có thể truy cập từ bất cứ đâu.
* `private`: Chỉ có thể truy cập ở bên trong class.
* `protected`: Chỉ có thể truy cập ở bên trong class và các class kế thừa từ class đó.                                                    
* `internal`: Giống như public nhưng chỉ hạn chế trong 1 assembly (Đọc thêm).

Ví dụ trong C#, ta có đối tượng <b>name</b> trong class Person:
```
public class Person
{
    private string? name; // Hidden variable

    public void SetName(string newName)
    {
        if (!string.IsNullOrEmpty(newName))
        {
            name = newName;
        }
        else
        {
            Console.WriteLine("Invalid name.");
        }
    }

    public string GetName()
    {
        return name;
    }
}
```
Ở trong hàm chính, nếu ta dùng giống thừa kế thì sẽ bị lỗi:
```
Person Person1 = new Person();

Person1.name = "Ho Manh Quan"; // Got error due to private
```
Thay vào đó, ta sẽ dùng:
```
Person Person1 = new Person();

Person1.setName("Ho Manh Quan");

Console.WriteLine("Your name is: " + Person1.GetName()); // Ho Manh Quan
```

### Polymorphism (Đa hình)
*Khái niệm*: Cho phép các đối tượng khác nhau thực thi chức năng giống nhau theo những cách khác nhau. Có 2 dạng đa hình:     

* <b>Đa hình tĩnh</b> (Static polymorphism): Xảy ra trong thời gian biên dịch (compile-time). Hai cơ chế phổ biến nhất để đạt được đa hình tĩnh là `Method overloading` và `Operator overloading`.    
  - <b>Nạp chồng phương thức</b> (Method overloading): Cho phép bạn định nghĩa nhiều phương thức trong cùng một lớp có cùng tên nhưng khác nhau về kiểu dữ liệu hoặc số lượng tham số.
  - <b>Nạp chồng toán tử</b> (Operator overloading): Cho phép bạn định nghĩa lại các toán tử để chúng có thể được sử dụng với các kiểu dữ liệu do người dùng định nghĩa.                           
* <b>Đa hình động</b> (Dynamic polymorphism): Xảy ra trong thời gian thực thi (runtime). Cơ chế chính để đạt được đa hình động là `Method overriding`.                                                         
  - <b>Ghi đè phương thức</b> (Method overriding): Cho phép một lớp con (Derived class) cung cấp một triển khai cụ thể cho một phương thức đã được định nghĩa trong lớp cha (Base class). Ta thường dùng `override` cho trường hợp này.
 
Ví dụ về <b>Nạp chồng phương thức</b>:
```
public class Math
{
    public int Add(int a, int b)
    {
        return a + b;
    }
    public double Add(double a, double b, double c)
    {
        return a + b + c;
    }
}
```
Ở hàm chính thì ta dùng:
```
Math Math1 = new Math();
Console.WriteLine("Total sum of a and b is: " + Math1.Add(1, 2)); // 4
Console.WriteLine("Total sum of a and b and c is: " + Math1.Add(1, 2, 3)); // 6
```

Ví dụ về <b>Nạp chồng toán tử</b>, ta sẽ làm phép toán cộng 2 số thực và ảo:
```
public class Complex
{
    public int Real { get; set; }
    public int Imaginary { get; set; }

    public Complex(int real, int imaginary)
    {
        Real = real;
        Imaginary = imaginary;
    }

    public static Complex operator + (Complex a, Complex b)
    {
        return new Complex(a.Real + b.Real, a.Imaginary + b.Imaginary);
    }
}
```
Ở hàm chính, ta thực hiện như sau:
```
Complex a = new Complex(1, 2);
Complex b = new Complex(3, 4);
Complex result = a + b; // Ở đây, 2 số thực là 1 và 3, 2 số ảo là 2 và 4
Console.WriteLine($"Real: {result.Real}, Imaginary: {result.Imaginary}"); // 4 + 6i
```

Ví dụ về <b>Ghi đè phương thức</b>, ta sẽ ghi đè phương thức Draw từ lớp cha cho lớp con:
```
public class Shape // Base class
{
    // Virtual Method
    public virtual void Draw()
    {
        Console.WriteLine("Drawing a shape.");
    }
}

public class Circle : Shape // Derived class
{
    // Override
    public override void Draw()
    {
        Console.WriteLine("Drawing a circle.");
    }
}

public class Rectangle : Shape // Derived class
{
    // Override
    public override void Draw()
    {
        Console.WriteLine("Drawing a rectangle.");
    }
}
```
Ở hàm chính thì ta thực hiện:
```
Shape Shape3 = new Circle();
Shape Shape4 = new Rectangle();

Shape3.Draw(); // Drawing a circle.
Shape4.Draw(); // Drawing a rectangle.
```

### Abstraction (Trừu tượng)
*Khái niệm*: <b>Ẩn đi các chi tiết triển khai của một lớp và chỉ hiển thị những tính năng cần thiết cho người sử dụng</b>. Tính chất này được thể hiện qua việc sử dụng `Interface` hoặc `Abstract class`. 

- <b>Lớp trừu tượng</b> (Abstract class): Là một lớp không thể được khởi tạo trực tiếp và chứa ít nhất một phương thức trừu tượng, được định nghĩa bằng từ khóa `abstract`. Các lớp con của lớp trừu tượng phải triển khai tất cả các phương thức trừu tượng này để có thể được sử dụng.
- <b>Giao diện</b> (Interface): Dùng để định nghĩa các phương thức mà các lớp phải triển khai mà không có bất kỳ logic nào. Nó chỉ định hành vi mà một đối tượng có thể thực hiện, mà không cung cấp bất kỳ thông tin về cách thức triển khai cụ thể nào.

Ví dụ về <b>Lớp trừu tường</b>:
```
public abstract class Animal_AC
{
    // Phương thức trừu tượng (không có thân hàm)
    public abstract void MakeSound();

    // Phương thức thông thường (có thân hàm)
    public void Sleep()
    {
        Console.WriteLine("Sleeping");
    }
}

public class Dog_AC : Animal_AC
{
    public override void MakeSound()
    {
        Console.WriteLine("Woof");
    }
}

public class Cat_AC : Animal_AC
{
    public override void MakeSound()
    {
        Console.WriteLine("Meow");
    }
}
```
Ở hàm chính thì ta dùng:
```
Animal_AC myDog_AC = new Dog_AC();
myDog_AC.MakeSound(); // Woof
myDog_AC.Sleep(); // Sleeping

Animal_AC myCat_AC = new Cat_AC();
myCat_AC.MakeSound(); // Meow
```

Ví dụ về <b>Giao diện</b>:
```
public interface Animal_I
{
    // Phương thức trừu tượng(không có phần thân)
    void MakeSound();

    // Phương thức mặc định (có phần thân)
    void Sleep()
    {
        Console.WriteLine("Sleeping");
    }
}

public class Dog_I : Animal_I
{
    public void MakeSound()
    {
        Console.WriteLine("Woof");
    }
}

public class Cat_I : Animal_I
{
    public void MakeSound()
    {
        Console.WriteLine("Meow");
    }
}
```
Ở hàm chính thì ta triển khai khá giống hệt Lớp trừu tượng:
```
Animal_I myDog_I = new Dog_I();
myDog_I.MakeSound(); // Woof
myDog_I.Sleep(); // Sleeping

Animal_I myCat_I = new Cat_I();
myCat_I.MakeSound(); // Meow
```
## SOLID
## Design Pattern
