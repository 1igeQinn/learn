# swift 基础

##  对象和类
### 类
使用class 和类型来创建一个类。类中属性的声明和常量变量的声明一样，构造器函数init 在删除对象之前进行一些清理工作使用deinit创建一个析构函数。
```
 class Shape{
    var age = 20
    //构造函数
    init(age: Int){
        self.age = age
    }

    func getSalary(){
        return age *1000
    }
 }

```

### 创建一个对象

```
var shape = Shape()
shape.age
```

###子类
子类的定义方法是在他们的类名后面加上父类名字。用冒号（:）分割.

```
class Square: Sharp{
    var len: Double
    var age: Int
    init(len){
        super.init(age:age)
        self.len = len
    }

    func area()->Double{
        return len*age
    }
}
```

###get set 方法

```
    class Atest{
        var a: Int
        var b: Int

        init(a,b){
            self.a = a
            self.b = b
        }

        var perimeter: Double{
            get{
                return 3.0 * a
            }
            set{
                b = newValue / 3
            }
        }

        override func area()->Double{
            a*b;
        }
    }
```

如果不需要计算属性，但是需要在设置一个新值之前运行一些代码，使用`willSet`,`didSet`

##枚举和结构体

###enum

```
enum Rank: Int{
    case Ace = 1
    case Two, Three, Four,Five,Six,Seven,Eight,Nine,Ten
    case Jack, Queen, King
    func simpleDesc()->String{
        switch self{
        case .Ace:
            return "ace"
        case .Jack:
            return "jack"
        case .Queen:
            return "queen"
        case .King:
            return "king"
        default:
            return String(self.rawValue)        
        }
    }
}

let ace = Rank.Ace
var ace2 = Rank.Jack
var ace2v = ace2.rawValue
let acer = ace.rawValue
```

###struct
```
    struct Card{
        var rank: Rank
        var b :Int
    }
```

## 接口和扩展

使用 `protocol` 来声明一个接口

```
protocol ExampleProtocol{
    var sinas:String{get}
    mutating func adjust()
}
```

类 枚举 结构体 都能实现接口

```
class Inplee:ExampleProtocol{
    var sinas: String = "simple class"
    var asd = 69105
    func adjust(){
        sin += "now 100% adjust" 
    } 
}

var sdo = Inplee()
sdo.sinas
sdo.asd
sdo.adjust()
sdo.sinas
```


使用 extension 来为现有的类型添加功能。

```
extension Int:ExampleProtocal{
    var sinas:String{
        return "the number \(self)"
    }
    mutating func adjust(){
        self += 42
    }
}

7.sinas // "the number 7"
```

## 泛型
在`<>`里面写一个名字来创建一个泛型函数或者类型

```
func repeat<ItemType>(item:ItemType,times: Int) ->ItemType[] {
    var result = ItemType[]()
    for i in 0..times{
        result += item 
    }
    return result
}
repeat("knock",4)
```

### 基础部分
#### 数据类型？
Int Float Double Bool String 
集合类型 Array Dictionary 
元组 Tuple 
Optional 类型处理值缺失的情况，表示那儿有一个只，并且他等于x或者那儿没有值

####变量和常量

let 声明常量 var 声明变量

####类型标注
说明一个变量或者常量的类型的时候使用冒号+一个空格(`: `)加类型名称。
` var a: String`

***一般来说很少需要写类型标注。如果你再声明变量或者常量的时候赋予了一个初始值。swif可以推断出这个常量或者变量的类型***

#### 常量变量的命名
可以使用任何喜欢的字符作为常量或者变量名包括Unicode字符，
>常量变量名不能包含数学符号，箭头保留的（非法的）Unicode码位，连线与制表符。也不能以数字开头。
>
>一旦讲变量或者常量声明为确定的类型，就不能使用相同的名字再次进行声明，或者改变存储值的类型。同时也不能将常量与变量进行互转。



