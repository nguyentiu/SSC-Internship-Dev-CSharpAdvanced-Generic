# SSC-Internship-Dev-CSharpAdvanced-Generic
# Hướng Dẫn Về Generics trong C#
## 1. Giới thiệu
Generics là một trong những tính năng mạnh mẽ nhất trong C#, cho phép các lập trình viên tạo ra các thành phần mã tái sử dụng, linh hoạt và an toàn về kiểu dữ liệu. Các thành phần này có thể là lớp, phương thức, giao diện hoặc đại biểu có thể hoạt động với bất kỳ kiểu dữ liệu nào mà không làm mất tính an toàn kiểu hoặc yêu cầu sao chép mã. Trong hướng dẫn này, chúng ta sẽ khám phá khái niệm về Generics, lý do tại sao chúng quan trọng và tìm hiểu về các loại Generics thường được sử dụng trong lập trình C#.
## 2. Vấn đề cần giải quyết
```csharp
public class IntegerList
{
    private List<int> items = new List<int>();

    public void Add(int item)
    {
        items.Add(item);
    }

    public void DisplayItems()
    {
        foreach (var item in items)
        {
            Console.WriteLine(item);
        }
    }
}

class Program
{
    static void Main()
    {
        IntegerList list = new IntegerList();
        list.Add(1);
        list.Add(2);
        list.DisplayItems();
    }
}
```
Mã này hoạt động tốt với số nguyên. Nhưng nếu bạn cần quản lý một danh sách các chuỗi, hoặc thậm chí là một đối tượng tùy chỉnh thì sao? Không có Generics, bạn sẽ phải tạo các lớp riêng biệt cho từng kiểu dữ liệu:
```csharp
public class StringList
{
    private List<string> items = new List<string>();

    public void Add(string item)
    {
        items.Add(item);
    }

    public void DisplayItems()
    {
        foreach (var item in items)
        {
            Console.WriteLine(item);
        }
    }
}
```
Cách tiếp cận này không chỉ lặp lại mà còn khó bảo trì. Hãy tưởng tượng nếu bạn cần quản lý mười kiểu khác nhau; bạn sẽ phải kết thúc với mười lớp khác nhau, tất cả đều có cấu trúc giống nhau nhưng với các kiểu dữ liệu khác nhau. Rõ ràng, đây không phải là một giải pháp hiệu quả.
### 2.1 Giải pháp với Generics
Generics cho phép chúng ta định nghĩa một lớp duy nhất có thể làm việc với bất kỳ kiểu dữ liệu nào. Đây là cách bạn có thể cải thiện ví dụ trước bằng cách sử dụng Generics:
```csharp
public class GenericList<T>
{
    private List<T> items = new List<T>();

    public void Add(T item)
    {
        items.Add(item);
    }

    public void DisplayItems()
    {
        foreach (var item in items)
        {
            Console.WriteLine(item);
        }
    }
}

class Program
{
    static void Main()
    {
        GenericList<int> intList = new GenericList<int>();
        intList.Add(1);
        intList.Add(2);
        intList.DisplayItems();

        GenericList<string> stringList = new GenericList<string>();
        stringList.Add("Hello");
        stringList.Add("World");
        stringList.DisplayItems();

        GenericList<double> doubleList = new GenericList<double>();
        doubleList.Add(1.23);
        doubleList.Add(4.56);
        doubleList.DisplayItems();
    }
}
```
Chỉ với một lớp, bạn có thể xử lý các kiểu dữ liệu khác nhau, giảm đáng kể lượng mã và làm cho nó dễ bảo trì hơn.

## 3. Các loại Generics trong C#
### 3.1 Tham số kiểu Generics
Tham số kiểu Generics cho phép bạn tạo các phương thức, lớp và giao diện có thể hoạt động với bất kỳ kiểu dữ liệu nào. Điều này được thực hiện bằng cách định nghĩa một chỗ trống cho kiểu dữ liệu, có thể được thay thế bằng một kiểu dữ liệu cụ thể khi lớp hoặc phương thức được khởi tạo.

Ví Dụ:
```csharp
public class Pair<T, U>
{
    private T first;
    private U second;

    public Pair(T first, U second)
    {
        this.first = first;
        this.second = second;
    }

    public void DisplayPair()
    {
        Console.WriteLine($"First: {first}, Second: {second}");
    }
}

class Program
{
    static void Main()
    {
        Pair<int, string> pair = new Pair<int, string>(1, "One");
        pair.DisplayPair();
    }
}
```
Giải thích: Trong ví dụ này, Pair<T, U> là một lớp Generics với hai tham số kiểu, T và U. Lớp Pair này có thể được sử dụng để giữ một cặp bất kỳ hai kiểu dữ liệu nào.

### 3.2 Lớp Generics
Lớp Generics là một lớp được định nghĩa với một hoặc nhiều tham số kiểu. Điều này cho phép lớp hoạt động với bất kỳ kiểu dữ liệu nào trong khi vẫn đảm bảo an toàn về kiểu.

Ví dụ
```csharp
public class Box<T>
{
    private T content;

    public void Add(T item)
    {
        content = item;
    }

    public T GetContent()
    {
        return content;
    }
}

class Program
{
    static void Main()
    {
        Box<int> intBox = new Box<int>();
        intBox.Add(123);
        Console.WriteLine($"Box contains: {intBox.GetContent()}");

        Box<string> strBox = new Box<string>();
        strBox.Add("Generics are powerful!");
        Console.WriteLine($"Box contains: {strBox.GetContent()}");
    }
}
```
Giải thích: Lớp Box<T> có thể lưu trữ bất kỳ kiểu dữ liệu nào, làm cho nó có thể tái sử dụng cho các kiểu dữ liệu khác nhau mà không cần viết lại lớp.

### 3.3 Giao diện Generics
Giao diện Generics định nghĩa một hợp đồng mà các lớp thực hiện giao diện phải tuân theo, nhưng với sự linh hoạt khi xác định kiểu dữ liệu khi thực hiện giao diện.

Ví dụ
```csharp
public interface IRepository<T>
{
    void Add(T item);
    T Get(int id);
}

public class MemoryRepository<T> : IRepository<T>
{
    private List<T> items = new List<T>();

    public void Add(T item)
    {
        items.Add(item);
    }

    public T Get(int id)
    {
        return items[id];
    }
}

class Program
{
    static void Main()
    {
        IRepository<string> repo = new MemoryRepository<string>();
        repo.Add("C#");
        repo.Add("Generics");
        Console.WriteLine(repo.Get(0));
        Console.WriteLine(repo.Get(1));
    }
}
```
Giải thích: Giao diện IRepository<T> định nghĩa một hợp đồng Generics cho các lớp repository. Lớp MemoryRepository<T> thực hiện giao diện này, cung cấp một cách linh hoạt để lưu trữ và truy xuất các mục của bất kỳ kiểu dữ liệu nào.

### 3.4 Phương thức Generics
Phương thức Generics là các phương thức có tham số kiểu, làm cho chúng có thể áp dụng cho các kiểu dữ liệu khác nhau mà không cần định nghĩa nhiều phương thức.

Ví dụ
```csharp
public class Utilities
{
    public static void Swap<T>(ref T a, ref T b)
    {
        T temp = a;
        a = b;
        b = temp;
    }
}

class Program
{
    static void Main()
    {
        int x = 1, y = 2;
        Console.WriteLine($"Before swap: x = {x}, y = {y}");
        Utilities.Swap(ref x, ref y);
        Console.WriteLine($"After swap: x = {x}, y = {y}");

        string first = "Hello", second = "World";
        Console.WriteLine($"Before swap: first = {first}, second = {second}");
        Utilities.Swap(ref first, ref second);
        Console.WriteLine($"After swap: first = {first}, second = {second}");
    }
}
```
Giải thích: Phương thức Swap<T> có thể hoán đổi giá trị của bất kỳ kiểu dữ liệu nào, làm cho nó trở thành một phương thức tiện ích linh hoạt.

## 4. So sánh Generics và Non-Generics
Để làm nổi bật lợi ích của việc sử dụng Generics, hãy so sánh chúng với các giải pháp không sử dụng Generics:

- Tái sử dụng mã: Không có Generics, bạn cần tạo nhiều lớp hoặc phương thức cho các kiểu dữ liệu khác nhau. Với Generics, bạn có thể định nghĩa một lớp hoặc phương thức duy nhất hoạt động cho mọi kiểu, giảm bớt sự trùng lặp mã.

- An toàn kiểu dữ liệu: Các collection không sử dụng Generics, như ArrayList, lưu trữ các phần tử dưới dạng object, có thể dẫn đến lỗi thời gian chạy nếu bạn cố gắng ép kiểu sai. Generics đảm bảo an toàn kiểu dữ liệu tại thời gian biên dịch, ngăn chặn các lỗi như vậy.

- Hiệu suất: Các collection không sử dụng Generics yêu cầu boxing và unboxing cho các kiểu giá trị, điều này có thể làm giảm hiệu suất. Generics tránh điều này bằng cách làm việc trực tiếp với các kiểu dữ liệu cụ thể.

So sánh mã
```csharp
// Non-Generic collection
ArrayList arrayList = new ArrayList();
arrayList.Add(1);
arrayList.Add("Two");

// Generic collection
List<int> list = new List<int>();
list.Add(1);
// list.Add("Two"); // Compile-time error
```
## 5. Nguồn tham khảo
- https://viblo.asia/p/su-dung-generics-trong-c-924lJDvNKPM
- https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/generics
