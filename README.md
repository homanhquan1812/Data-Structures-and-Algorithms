﻿# General-IT-Knowledge
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

* <b>Đa hình tĩnh (Static polymorphism)</b>: Xảy ra trong thời gian biên dịch (compile-time). Hai cơ chế phổ biến nhất để đạt được đa hình tĩnh là `Method overloading` và `Operator overloading`.    

  - <b>Nạp chồng phương thức (Method overloading)</b>: Cho phép bạn định nghĩa nhiều phương thức trong cùng một lớp có cùng tên nhưng khác nhau về kiểu dữ liệu hoặc số lượng tham số.
  * <b>Nạp chồng toán tử (Operator overloading)</b>: Cho phép bạn định nghĩa lại các toán tử để chúng có thể được sử dụng với các kiểu dữ liệu do người dùng định nghĩa.                           
* <b>Đa hình động (Dynamic polymorphism)</b>: Xảy ra trong thời gian thực thi (runtime). Cơ chế chính để đạt được đa hình động là `Method overriding`.                                                         
  * <b>Ghi đè phương thức (Method overriding)</b>: Cho phép một lớp con (Derived class) cung cấp một triển khai cụ thể cho một phương thức đã được định nghĩa trong lớp cha (Base class). Ta thường dùng `override` cho trường hợp này.

### Abstraction (Trừu tượng)
*Khái niệm*: <b>Ẩn đi các chi tiết triển khai của một lớp và chỉ hiển thị những tính năng cần thiết cho người sử dụng</b>. Tính chất này được thể hiện qua việc sử dụng `Interface` hoặc Lớp trừu tượng `Abstract class`. 

- Lớp trừu tượng (Abstract class): Là một lớp không thể được khởi tạo trực tiếp và chứa ít nhất một phương thức trừu tượng, được định nghĩa bằng từ khóa `abstract`. Các lớp con của lớp trừu tượng phải triển khai tất cả các phương thức trừu tượng này để có thể được sử dụng.
- Giao diện (Interface): Dùng để định nghĩa các phương thức mà các lớp phải triển khai mà không có bất kỳ logic nào. Nó chỉ định hành vi mà một đối tượng có thể thực hiện, mà không cung cấp bất kỳ thông tin về cách thức triển khai cụ thể nào.
  
## SOLID
## Design Pattern
