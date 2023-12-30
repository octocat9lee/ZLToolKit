# mini

 `variant` 类是一个继承自 `std::string` 的类，用于存储和操作多种类型的值。

- 关于构造函数的说明
``` C++
    template<size_t N>
    variant(const char (&s)[N]) :
            std::string(s, N) {
    }

这是 variant 类的一个构造函数模板，它接受一个固定大小的字符数组作为参数。

模板参数 N 表示字符数组的大小。

构造函数的参数 const char (&s)[N] 是一个对字符数组的引用，这意味着它可以接受字符串字面量作为参数。

这个构造函数将字符数组转换为字符串，并用它初始化 variant 对象。

下面是一个使用这个构造函数的示例：
variant v = "Hello, world!";

在这个示例中，字符串字面量 "Hello, world!" 是一个包含 14 个字符（包括空字符）的字符数组。
所以，模板参数 N 被替换为 14，构造函数的参数 s 是对这个字符数组的引用。
然后，构造函数使用这个字符数组和它的大小创建一个字符串，并用这个字符串初始化 variant 对象。
```

- `operator T() const` 是一个类型转换运算符，它允许 `variant` 对象被转换为任何类型 `T`。这是通过调用 `as<T>()` 方法实现的。

``` C++
variant v1 = "123"; // 使用字符串初始化
variant v2 = "4.56"; // 使用字符串初始化

int i = v1; // 使用类型转换运算符将 variant 转换为 int
double d = v2; // 使用类型转换运算符将 variant 转换为 double

std::cout << i << std::endl; // 输出 123
std::cout << d << std::endl; // 输出 4.56
```

- `operator==` 是一个比较运算符，用于比较 `variant` 对象和其他类型的对象。这个运算符使用了模板，这意味着它可以接受任何类型的参数。

- `as()` 方法是一个模板方法，它用于将 `variant` 对象转换为任何类型 `T`。这个方法有两个版本，一个用于类类型，一个用于非类类型。这是通过 `std::enable_if` 和 `std::is_class` 实现的，这两个都是 C++ 的类型特性库中的工具。`std::enable_if` 可以根据条件启用或禁用函数模板，`std::is_class` 可以检查一个类型是否是类类型。
  
``` C++
variant v1 = "123"; // 使用字符串初始化
variant v2 = "4.56"; // 使用字符串初始化

int i = v1.as<int>(); // 使用 as 方法将 variant 转换为 int
double d = v2.as<double>(); // 使用 as 方法将 variant 转换为 double

std::cout << i << std::endl; // 输出 123
std::cout << d << std::endl; // 输出 4.56
```

- `as_default()` 方法是一个私有的模板方法，它用于将 `variant` 对象转换为非类类型。这个方法创建一个 `T` 类型的对象，然后使用 `std::stringstream` 将 `variant` 对象的字符串表示形式转换为 `T` 类型。

- `as<bool>()` 和 `as<uint8_t>()` 是 `as()` 方法的特化版本，它们用于将 `variant` 对象转换为 `bool` 类型和 `uint8_t` 类型。这些特化版本在类定义外部声明，通常在类定义的下方或者源文件中定义。

- `mINI` 是一个类型别名，它是 `mINI_basic<std::string, variant>` 的简化名称。这意味着你可以使用 `mINI` 来创建一个键类型为 `std::string`，值类型为 `variant` 的 `mINI_basic` 对象。
