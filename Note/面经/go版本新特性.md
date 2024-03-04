## Go 1.8加入了泛型

```go
func Example[T any](v T) T {
    return v
}
intExample := Example[int](10)
stringExample := Example[string]("hello")
```

它允许在函数、接口和类型上指定类型参数，以实现更通用和灵活的编程。Go 语言的泛型是通过类型参数来实现的，类型参数可以在函数、接口和类型定义中使用。在定义泛型函数时，可以在函数的参数列表和返回类型中使用类型参数，在调用泛型函数时，需要指定实际的类型参数值。

除了函数，Go 语言的泛型也可以用于接口和类型定义。在定义泛型接口时，可以在接口的方法列表中使用类型参数，在实现泛型接口时，需要指定实际的类型参数值。在定义泛型类型时，可以在类型定义中使用类型参数，并在实例化泛型类型时指定实际的类型参数值。

总的来说，Go 语言的泛型可以帮助我们实现更通用和灵活的编程，提高代码的可读性和可维护性。但是需要注意的是，Go 语言的泛型是实验性的，在生产环境中使用泛型需要谨慎。

## Go 1.20新特性

- 对泛型的规则做了一个小小的修改。有了 Go 泛型，你可以通过一个函数获取任何map的键：


```go
func keys[K comparable, V any](m map[K]V) []K {
    var keys []K
    for k := range m {
        keys = append(keys, k)
    }
    return keys
}
```


在这段代码中，K comparable, V any 为“类型约束”。这意味着 K 可以是任何 comparable 的类型，而 V 则没有类型限制。comparable 类型为数字、布尔、字符串和由 comparable（可比较类型） 元素组成的固定大小的复合类型等。因此，K 为 int，V 为一个 bytes 切片是合法的，但 K 是一个 bytes 切片是非法的。

- 一个切片可以很容易转换为一个固定长度的数组

```go
s := []string{"a", "b", "c"}
a := [3]string(s)
```

## Go 1.21新特性

- **新增一个clear预定义函数用来用作切片和map的clear操作**

1. 针对slice，clear保持slice的长度和容量，但将所有slice内已存在的元素(len个)都置为元素类型的零值；
2. 针对map，clear则是清空所有map的键值对，clear后，我们将得到一个empty map

- **go test -c支持为多个包同时构建测试二进制程序**

Go 1.21版本之前，go test -c仅支持将单个包的测试代码编译为测试二进制程序，Go 1.21版本则允许我们同时为多个包构建测试二进制程序。下面是官方给出的例子：

```go
$ go test -c -o /tmp ./pkg1 ./pkg2 ./pkg2
$ ls /tmp
pkg1.test pkg2.test pkg3.test
```

- **sync包增加OnceFunc、OnceValue和OnceValues**

在sync.Once的基础上，这个issue增加了三个与Once相关的"语法糖"API，用在一些对Once有需求的最常见的场景中。

1. OnceFunc：返回一个只调用 f 一次的函数。返回的函数可以同时调用。如果 f panic，则返回的函数在每次调用时都会死机相同的值
2. OnceValue：返回一个只调用 f 一次的函数，并返回值 f 返回。返回的函数可以同时调用。如果 f panic，则返回的函数在每次调用时都会死机相同的值。
3. OnceValues：返回一个只调用 f 一次的函数，并返回值 返回。返回的函数可以同时调用。如果 f panic，则返回的函数在每次调用时都会死机相同的值。