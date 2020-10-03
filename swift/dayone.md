# swift 基础
## 值的声明
`let` 声明常量
`var` 声明变量

```
var simpleValue = 42 //编译器推断是一个整数，因为 他得初始值是整数
let Constant = 34
```

变量或者常量的类型必须和你赋予给他们的值一样。然而，声明时类型是可选的，声明的同时赋值的花，编译器会自动推断类型。
如果初始值没有提供足够的信息（或者没有初始值），那需要在变量后面声明类型，用冒号分割。

```
let i = 70
let u = 70.0 //编译器推断
let db: Double = 70 //明确指定
let ff: Float = 4
```
值永远不会被隐式的转换为其他的类型那个。如果需要请显式转换

```
let label = "the with is "
let width = 95 //编译器推断
let withLable = label + String(width)
//TODO  类型转换的细节
```

有一种更简单的把值转换为字符串的方法：把值写到括号中，并且在括号之前加一个反斜杠。

```
let apple = 3
let orange = 95 //编译器推断
let apples = "I have \(apple) apples."
let oo = "i have \(apple+orange) pieces of fruit."

//输出
" I have 3 apples."
" i have 98 pieces of fruit."
```

### 数组和字典
1. 用户[] 来创建数组和字典。并使用下标或者key来访问
 
 ```
 var arr =[1,2,3,4,5]
 arr[1] = 10
 
 var dic = [
        "name":"jonas",
        "age":26
 ]
 dic["name"] = myrna
 ```
 
 2. 创建一个空得数组或者字典。
 
 ```
 let emptyArr = String[]()
 let emptyDic = Dictionary<String,Float>
 //如果类型信息可以被推断出来，则可以用[] 和[:] 来创建空数组
 list = []
 ```
 
 ## 控制流
if switch for-in for while do-while

```
let arr = [1,2,3,5,8,79,0]
var t = 0
for s in arr {
    if s >3{
        t+= 40
    }else{
        t+=80
    }
}
t
```

 在if 语句中，条件必须是一个布尔表达式。
 可以一起使用if和let 来处理值缺失的情况。
 在类型的后面加一个问号来标记这个变量值是可选的。
 
```
var optionalString: String? = "Hello"  optionalString == nil 
 var optionalName: String? = "John Ap pleseed" 
var greeting = "Hello!" 
if let name = optionalName {
    greeting = "Hello, \(name)" 
} 

```


###switch
switch 支持任意类型的数据以及各种比较操作
运行switch 中匹配到字句之后，程序会退出switch，因此不需要break；

```
let aa = [
    "monday": [2, 3, 5, 7, 11, 13],
    "tusday": [1, 1, 2, 3, 5, 8],   "friday": [1, 4, 9, 16, 25], 
]

l = 0
for (a, b) in aa{
    for c in b {
        if a >l {
            l = a
        }
    }
}
```

### while

## 函数 和 闭包
使用func 来声明一个函数 使用名字和参数来调用函数，使用->来制定返回值。

```
// define a function
 func greet(name: String, day: String) -> String {
    return "Hello \(name), today is \(day)."
 }
 // call the function
 greet("jack","Friday")
```

用元组来来返回多个值

```
func getPrice() ->(Double,Double,Double){
    return (3.59, 3.69, 3.79) 
}
getPrice()
```
函数才参数数量是可变的，使用一个数组来获取他们。

```
func sumOf(numbers: Int...)->Int{
    var sum = 0 
    for n in numbers{
        sum += n
    }
    return sum;
}

sumOf()
sumOf(1,2,3)
```

函数可以被嵌套，被嵌套的函数可以访问外侧函数的变量。

```
func re() -> Int{
    var i = 10
    func add(){
        i+=5
    }
    add()
    return y
}

re()
```

函数是一等公民，函数可以作为另一个函数的返回值。

```
func jj() -> (Int -> Int){
    func add(num:Int) -> Int{
        return num + 1
    }
    return add
}

var ii = jj()
ii(7)
```

函数也能当做参数传入另一个函数

```
func hasss(list: Int[], c: Int ->Bool) -> Bool{
    for item in list {
        if c(item){
            return true
        }
    }
    return false
}

func lesss(num: Int)-> Bool {
    return num >10
}

var num = [20,8,10,89]
hasss(num,lesss)
```

函数实际上是一种特殊的闭包，可以使用{}来创建一个匿名闭包。使用in来分割参数并返回类型。
```
    numbers.map({
        (number: Int)-> Int in
            let r = 3 * number
            return result
        })
```
