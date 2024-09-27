# Object-Oriented Programming
## Kiến thức căn bản về Lập trình hướng đối tượng (OOP)
### OOP là gì?
<div align="center">
  <img src="https://github.com/homanhquan1812/General-IT-Knowledge/assets/130955957/2e703da8-ea0b-456e-8022-b02581da4079" alt="YOLOHOME Logo" width="600" style="">
</div>

OOP là viết tắt của Object-Oriented Programming, có nghĩa là `lập trình hướng đối tượng`. Lập trình hướng đối tượng (OOP) là một mô hình lập trình dựa trên khái niệm "đối tượng", được tạo ra dựa trên khuôn mẫu của các lớp. 

OOP gồm 2 thành phần chính: `Class` và `Object`.

<div align="center">
  <img src="https://github.com/homanhquan1812/General-IT-Knowledge/assets/130955957/f84049e8-26bb-4d9a-a82e-5d7aae499666" width="600" style="">
</div>


### Class (Lớp)
Là một khuôn mẫu để tạo ra các đối tượng (Object). Nó định nghĩa các trường (thường được gọi là thuộc tính) và phương thức mà các đối tượng của lớp đó sẽ có.

Các thành phần thường gặp trong Class:
* `Field`: Còn được gọi là **trường**, là những thông tin, đặc điểm của đối tượng (Tên, tuổi,...); ta thường dùng `private` để tăng tính bảo mật.
  
Ví dụ, một class Person có 2 trường <b>name</b> và <b>age</b>:
```
public class Person
{
    // Fields
    private string name;
    private int age;  
}
```
* `Constructor`: Hay còn được gọi là **hàm khởi tạo**, là một loại phương thức đặc biệt dùng để khởi tạo đối tượng của một lớp. Tên của Constructor phải trùng với tên lớp và không có kiểu trả về. Các Constructor có thể sử dụng các `Access modifiers` (Đọc ở dưới) để kiểm soát quyền truy cập.
  
Ví dụ về 1 constructor trong class Person:
```
public class Person
{
    // Constructor
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }
}
```
* `Method`: Gọi là **phương thức** (hoặc là hàm trong Class), được dùng để mô tả hành vi hoặc hành động mà các đối tượng của lớp đó có thể thực hiện.
  
Ví dụ, một class Person có 1 phương thức <b>Information</b>:
```
public class Person
{
    public void Information()
    {
        Console.WriteLine($"Your information includes name: {name} and age: {age}");
    }
}
```     

Các định nghĩa khác:
* `Destructor`: Còn gọi là hàm hủy, là một loại phương thức đặc biệt được thực thi khi một đối tượng của class đó bị hủy. Hàm này được sử dụng để giải phóng bộ nhớ (Trong C# thì không cần hàm này nhờ tính năng **Garbage Collector**).
* `Property`: Gọi là thuộc tính, khái niệm giống với trường, chỉ khác nhau cách dùng và có tính đóng gói. Chỉ có vài ngôn ngữ lập trình có thuộc tính (C#, Python,...).
  
Ví dụ về 1 đoạn code dùng field:
```
class Person
{
    // Fields
    private string name;
    public int age;           
    
    // Constructor
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }

    public string getName()
    {
        return name;
    }
    
    public void setName(string value)
    {
        name = value;
    }

    // Methods
    public void Information()
    {
        Console.WriteLine($"Your information includes name: {name} and age: {age}");
    }
}
```
Ta thấy rằng phải dùng **getName** và **setName** nếu biến **name** là **private**. C# có tính năng thay thế mà tốt hơn:
* `Full property`: Tính năng này giúp kiểm soát dữ liệu tốt nhất với những điều kiện ta đặt.

```
class Person
{
    // Fields
    private string name;
    public int age;           
    
    // Constructor
    public Person(string name, int age)
    {
        Name = name;
    }

    // Full property
    public string Name
    {
        get { return name; }
        set 
        { 
            if (!string.IsNullOrEmpty(value))
            {
                name = value;
            }
            else
            {
                throw new ArgumentException("Name cannot be null or empty");
            }
        }
    }

    // Methods
    public void Information()
    {
        Console.WriteLine($"Your information includes name: {name} and age: {age}");
    }
}
```

* `Auto-implemented property`: Nếu ta không cần kiểm soát chặt chẽ, ta chỉ cần dùng `{ get; set; }`.
  
```
class Person
{
    // Fields
    private string name;
    public int age;           
    
    // Constructor
    public Person(string name, int age)
    {
        Name = name;
    }

    // Auto-implemented property
    public string Name { get; set; }

    // Methods
    public void Information()
    {
        Console.WriteLine($"Your information includes name: {name} and age: {age}");
    }
}
```

### Object (Đối tượng)
Đối tượng là 1 thực thể được tạo ra từ Lớp, chứa dữ liệu và hành vi cụ thể. Đối tượng thường được tạo ở hàm chính.

Từ ví dụ ở đoạn code này:
```
class Person
{
    // Fields
    private string name;
    public int age;           
    
    // Constructor
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }

    public string getName()
    {
        return name;
    }
    
    public void setName(string value)
    {
        name = value;
    }

    // Methods
    public void Information()
    {
        Console.WriteLine($"Your information includes name: {name} and age: {age}");
    }
}
```

Ta sẽ khai báo ở hàm chính như sau:
```
string myName = "Ho Manh Quan";
int myAge = 23;

Person Person1 = new Person(myName, myAge); // Ta đã tạo ra Person1 từ class Person

Console.WriteLine($"My name is {Person1.getName()} and I'm {Person1.age} years old.");

Person Person2 = new Person("Sussy Boy", 25);

Console.WriteLine($"My name is {Person2.getName()} and I'm {Person2.age} years old.");

Person2.Information();
```
## 4 khái niệm cơ bản của OOP
### Inheritance (Kế thừa)

<div align="center">
  <img src="https://github.com/homanhquan1812/General-IT-Knowledge/assets/130955957/fa33b350-b284-445f-81b3-050695176ab0" alt="YOLOHOME Logo" width="600" style="">
</div>

Cho phép một hoặc nhiều lớp (`Derived class` - Lớp dẫn xuất) <b>kế thừa thuộc tính và phương thức của một lớp khác</b> (`Base class` - Lớp cơ sở) để tăng khả năng tái sử dụng và giảm thiểu việc lặp lại code. 

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

<div align="center">
  <img src="https://github.com/homanhquan1812/General-IT-Knowledge/assets/130955957/235a0eec-50e8-4647-9f7d-56720ba5f871" alt="YOLOHOME Logo" width="600" style="">
</div>

<b>Che giấu thông tin chi tiết của các đối tượng, chỉ cho phép truy cập thông qua phương thức public</b>. Tính chất này giúp tăng tính bảo mật cho đối tượng và tránh tình trạng dữ liệu bị hư hỏng ngoài ý muốn, giúp duy trì tính ổn định và độ tin cậy của chương trình. 

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

<div align="center">
  <img src="https://github.com/homanhquan1812/General-IT-Knowledge/assets/130955957/f7692ae8-06bd-422f-83eb-09ca75c726d4" alt="YOLOHOME Logo" width="600" style="">
</div>

Cho phép <b>các đối tượng khác nhau thực thi chức năng giống nhau theo những cách khác nhau</b>. Có 2 dạng đa hình:     

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
Shape BaseShape = new Shape(); // Class Base vẫn có thể được sử dụng
Shape Shape3 = new Circle();
Shape Shape4 = new Rectangle();

BaseShape.Draw(); // Drawing a shape.
Shape3.Draw(); // Drawing a circle.
Shape4.Draw(); // Drawing a rectangle.
```

### Abstraction (Trừu tượng)

<div align="center">
  <img src="https://github.com/homanhquan1812/General-IT-Knowledge/assets/130955957/20670605-e175-4fd1-800a-0b42afcb658a" alt="YOLOHOME Logo" width="600" style="">
</div>

<b>Ẩn đi các chi tiết triển khai của một lớp và chỉ hiển thị những tính năng cần thiết cho người sử dụng</b>. Tính chất này được thể hiện qua việc sử dụng `Interface` hoặc `Abstract class`. 

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

# Algorithmic Complexity

Độ phức tạp thuật toán là một thước đo dùng để xác định hiệu suất của một thuật toán, đánh giá lượng tài nguyên cần thiết (thời gian và bộ nhớ) để thực hiện thuật toán đó dựa trên kích thước đầu vào. 

<div align="center">
  <img src="https://github.com/user-attachments/assets/1dbacde5-7196-40cf-8371-d3fbc08616f1" alt="YOLOHOME Logo" width="600" style="">
  
  *Hình minh họa các mức độ phức tạp thuật toán dựa trên số lượng phép tính (Operations) theo kích thước đầu vào (Elements)*
</div>

Có hai loại độ phức tạp chính:

* **Độ phức tạp thời gian** (Time Complexity): Thường được biểu diễn bằng `Big-O notation` (kí hiệu O lớn), giúp chúng ta ước lượng thời gian chạy của thuật toán theo hàm của kích thước đầu vào. Một số ví dụ phổ biến:
  - `O(1)`: Thời gian chạy không đổi, bất kể kích thước đầu vào (constant time).
  - `O(log n)`: Thời gian chạy tăng theo logarit của kích thước đầu vào (logarithmic time). Ví dụ: thuật toán tìm kiếm nhị phân.
  - `O(n)`: Thời gian chạy tỉ lệ thuận với kích thước đầu vào (linear time).
  - `O(n.log n)`: Thời gian chạy phổ biến cho các thuật toán sắp xếp hiệu quả như Merge Sort và Quick Sort.
  - `O(n^2)`: Thời gian chạy tỉ lệ với bình phương của kích thước đầu vào, thường gặp trong các thuật toán sử dụng hai vòng lặp lồng nhau (quadratic time).
  - `O(2^n)`: Thời gian chạy tăng theo hàm mũ, rất kém hiệu quả, thường xuất hiện trong các bài toán như đệ quy trên tập hợp con (exponential time).
  - `O(n!)`: Thời gian chạy theo giai thừa; Đây là mức độ phức tạp rất lớn, gần như không thể áp dụng cho các bài toán lớn vì số phép tính tăng rất nhanh.

* **Độ phức tạp không gian** (Space Complexity): Cũng được biểu diễn bằng Big-O notation và đo lường lượng bộ nhớ mà thuật toán yêu cầu khi kích thước đầu vào tăng lên. Các yếu tố ảnh hưởng đến độ phức tạp không gian bao gồm:
  - Bộ nhớ dùng để lưu trữ biến.
  - Bộ nhớ dùng cho các cấu trúc dữ liệu như mảng, danh sách, cây,...
  - Bộ nhớ đệ quy (stack).
    
# Linked List
Danh sách liên kết là 1 cấu trúc dữ liệu được sử dụng để lưu trữ 1 tập hợp các dữ liệu. Danh sách liên kết có các tính chất sau:

* Các **phần tử `node`** trong danh sách liên kết được kết nối bằng con trỏ.
* Phần tử cuối trỏ tới `NULL`.
* Có thể tăng hoặc giảm số lượng phần tử trong quá trình thực thi chương trình.
* Tối ưu dung lượng bộ nhớ.

Có 2 giải thuật chính đối với danh sách liên kết là:

* `Insert`: Chèn một phần tử vào vị trí bất kỳ trong danh sách liên kết.
* `Delete`: Xóa một phần tử ở vị trí bất kỳ trong danh sách liên kết.

Khác biệt chính giữa **Linked List** và **Array List**: 

| | Linked List | Array List |
|---|---|---|
| Cấu trúc dữ liệu | <ul><li>Dữ liệu được lưu trữ trong các node riêng biệt, mỗi node chứa dữ liệu và một con trỏ (pointer) đến node tiếp theo (hoặc cả node trước trong doubly linked list).</li><li>Kích thước có thể thay đổi động, không cần bộ nhớ liên tục.</li><li>Không có chỉ số để truy cập trực tiếp; phải duyệt qua các node để tìm phần tử.</li></ul> | <ul><li>Dữ liệu được lưu trữ trong một mảng (array), với các phần tử được sắp xếp liền kề nhau trong bộ nhớ.</li><li>Kích thước của mảng cố định khi tạo.</li><li>Truy cập phần tử bằng chỉ số **index**.</li></ul> |
| Truy cập dữ liệu | Truy cập phần tử O(n) (thời gian tuyến tính), phải duyệt qua danh sách từ đầu đến cuối để tìm phần tử. | Truy cập phần tử O(1) (thời gian hằng số), vì có thể truy xuất trực tiếp bằng chỉ số. |
| Thao tác chèn và xóa phần tử | <ul><li>Chèn hoặc xóa phần tử ở giữa danh sách có thể nhanh hơn (O(1)) nếu có con trỏ đến node liên quan, vì không cần dời các phần tử khác.</li><li>Tuy nhiên, nếu cần duyệt để tìm vị trí cần chèn/xóa, thao tác có thể mất O(n).</li></ul> | <ul><li>Thao tác chèn hoặc xóa phần tử ở giữa mảng tốn kém (O(n)) vì phải dời các phần tử khác để duy trì tính liên tiếp của mảng.</li><li>Chèn/xóa phần tử ở cuối có thể nhanh hơn (O(1) trong trường hợp tốt nhất) nếu mảng còn đủ chỗ.</li></ul> |
| Sử dụng bộ nhớ | <ul><li>Bộ nhớ được cấp phát cho từng node riêng lẻ, không cần liên tục.</li><li>Mỗi node có thêm bộ nhớ cho con trỏ, dẫn đến việc sử dụng nhiều bộ nhớ hơn so với array list.</li></ul> | <ul><li>Bộ nhớ được cấp phát liên tục, có thể dẫn đến lãng phí bộ nhớ nếu có nhiều chỗ trống.</li><li>Nếu bộ nhớ mảng đầy, cần phải tạo một mảng mới với kích thước lớn hơn, và sao chép toàn bộ dữ liệu.</li></ul> |
| Tính linh hoạt | <ul><li>Phù hợp khi cần thường xuyên chèn/xóa phần tử, đặc biệt là ở đầu hoặc giữa danh sách.</li><li>Không phù hợp khi cần truy cập ngẫu nhiên các phần tử.</li></ul> | <ul><li>Phù hợp khi cần truy cập nhanh các phần tử bằng chỉ số.</li><li>Không phù hợp khi cần thường xuyên chèn/xóa các phần tử ở giữa.</li></ul> |

  
Danh sách liên kết được chia làm nhiều loại:
* **Singly Linked List** (Danh sách liên kết đơn).
* **Doubly Linked List** (Danh sách liên kết đôi).
* **Circular Linked List** (Danh sách liên kết vòng đơn). => Đọc thêm
* **Circular Doubly Linked** List (Danh sách liên kết vòng đôi). => Đọc thêm

## Singly Linked List
Mỗi một phần tử trong danh sách liên kết đơn gồm có `data` và `next`, **next** sẽ trỏ tới **node** kế tiếp trong danh sách liên kết đơn. Và nếu **next** trỏ tới **NULL** thì có nghĩa là node đó là node cuối cùng trong danh sách liên kết đơn.

<div align="center">
  <img src="https://github.com/user-attachments/assets/8847a1b1-d8f4-4ae7-924a-6dbf89d8638f" alt="YOLOHOME Logo" width="600" style="">
</div>

## Doubly Linked List
Mỗi node trong danh sách liên kết đôi gồm có `prev`, `data` và `next`, **prev** trỏ tới phần tử đứng trước, **next** trỏ tới phần tử phía sau. Nếu **prev** trỏ tới **NULL** thì có nghĩa node đó là node đầu tiên trong danh sách liên kết đôi, còn nếu **next** trỏ tới **NULL** thì đó là node cuối trong danh sách liên kết đôi.

<div align="center">
  <img src="https://github.com/user-attachments/assets/647e6280-6af8-407e-afa1-af72adf146a0" alt="YOLOHOME Logo" width="600" style="">
</div>
