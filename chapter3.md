# <a name="3-Functions"></a> 函数

## <a name="3.1-Function-calls"></a> 3.1 函数调用

在程序上下文环境里, 函数是指一系列呈现如何进行计算的语句. 当你定义一个函数的时候, 你需要指明函数的名和这些语句. 然后你才可以通过"呼叫"函数名来调用函数. 我们已经看过一个函数调用的例子了:

    >>> type(32)
    <type 'int'>

这个函数的函数名是 "type". 括号里的表达式被称为__函数的形参(argument of the function)__. 这个函数调用的结果是告诉你形参是什么类型. 

我们通常说函数 "采用(take)" 一个形参, 并且 "返回(return)" 结果. 这个被返回的结果称为"返回值".

## <a name="3.2-Type-conversion-functions"></a> 3.2 类型转换函数

Python 提供了能将数据从一个类型转换到另一个类型的内置函数. `int()` 函数能够获取任何值,如果获得的值能够转换,那么它将转换成一个整型数据.

    >>> int('32')
    32
    >>> int("Hello")
    ValueError: invalid literal for int(): Hello
    
`int()` 函数能够将浮点型数据转换成整型数据, 但它并不是采用四舍五入的方法,而是舍弃尾数.

    >>> int(3.99999)
    3
    >>> int(-2.3)
    -2
    
`float()` 能够将整型数据或字符串转换成浮点数字:

    >>> float(32)
    32.0
    >>> float("3.14159")
    3.14159
    
最后, `str()` 能够将他的参数转换成字符串:

    >>> str(32)
    '32'
    >>> str(3.14159)
    '3.14159'

## <a name="3.3-Math-functions"></a> 3.3 数学运算函数

Python 有一个数学模块提供了几乎所有数学函数. __模块__是指一个包含了相关函数集合的文件.

在我们使用模块之前,我们需要导入(import)它:

    >>> import math

这个语句创建了一个名为 math 的模块对象. 如果你打印模块对象, 你会得到一些关于它的信息:

    >>> print math
    <module 'math' (built-in)>

模块对象包含了定义在模块里的函数和变量. 为了访问一个函数, 你需要指定模块名和函数名, 并且用一个点分割开(也就是著名的句号). 这种格式被称为点符号.

    >>> ratio = signal_power / noise_power
    >>> decibels = 10 * math.log10(ratio)

    >>> radians = 0.7
    >>> height = math.sin(radians)

第一个例子利用 log10 来计算信噪比(假定 signal_power 和 noise_power 已经定义). 数学模块同时也提供 log 函数来计算基于 e 的对数.

第二个例子计算 radians 的正弦值. 变量名已经暗示了比如 `sin` 等其他三角函数(如 `cos`, `tan`) 是以弧度为单位计算的. 从角度转换成弧度需要除以 360 并乘上 2π .

    >>> degrees = 45
    >>> radians = degrees / 360.0 * 2 * math.pi
    >>> math.sin(radians)
    0.707106781187

表达式 `math.pi` 会从数学模块中取得 π 的值的近似值, 精确 15 个数字.
如果你了解三角函数, 你可以对比 2 的平方根除以 2 的值:

    >>> math.sqrt(2) / 2.0
    0.707106781187

## <a name="3.4-Composition"></a> 3.4 组合使用

到此为止, 我们已经了解了程序的一些元素 -- 变量, 表达式以及语句. 但我们没有讨论如何组合使用他们.

程序的一个有用的特性是能够将各个小块组合起来. 例如一个函数的参数可以是任何类型的表达式, 包括算术运算操作符.

    x = math.sin(degrees / 360.0 * 2 * math.pi)

甚至是以函数调用作为参数:

    x = math.exp(math.log(x+1))

除了赋值语句的左边必须是一个变量名之外, 几乎任何你能够放置一个值,放置一个任意的表达式的地方. 任何表达式放在赋值语句左边都会产生语法错误

    >>> minutes = hours * 60        # right
    >>> hours * 60 = minutes        # wrong
    SyntaxError: can't assign to operator

## <a name="3.5-Adding-new-functions"></a> 3.5 定义新函数

到目前为止, 我们已经知道如何调用函数, 但是这些函数都是来自 Python, 但我们也有可能需要添加新的函数. 定义一个函数需要指明新函数的名称还有它被调用时候被执行的语句序列. 

这是一个例子:

    def print_lyrics():
        print "I'm a lumberjack, and I'm okay"
        print "I sleep all night and I work all day."

`def` 是定义新函数的关键词. 这个函数的函数名是 `print_lyrics` . 函数名的规则与变量名规则是一样的: 字母, 数字还有一些标点符号是合法的, 但第一个字符不能是数字.你也不能使用关键词作为函数名, 并且要避免函数名与变量名重名的情况.

函数名后带着空括号表示这个函数不需要任何参数. 函数定义的第一行称为头部, 其他部分称为主体. 头部必须以冒号结尾, 而主体部分必须有缩进. 按照惯例, 缩进一般使用四个空格. 而主体部分可以包含任意数量的语句.

`print` 语句中的字符串需用使用双引号包含住. 单引号和双引号的作用是一样的, 大多数人使用单引号, 除非是在字符串里已经有单引号了.

如果你在交互模式下定义函数, 解释器会输出 `...` 让你知道你的定义还没结束.

## <a name="3.6-Definitions and uses"></a> 3.6 定义与调用

将上一章节的代码片段放在一起, 整个程序看起来就像:

    def print_lyrics():
        print "I'm a lumberjack, and I'm okay."
        print "I sleep all night and I work all day."

    def repeat_lyrics():
        print_lyrics()
        print_lyrics()

    repeat_lyrics()

这个程序包含两个函数定义: `print_lyrics` 和 `repeat_lyrics`. 函数定义以如其他语句一样的方式被执行, 但他的作用是创建一个函数对象. 只有当函数被调用的时候, 函数内部的语句才会被执行, 并且函数定义不会生成输出.

如你所料, 在你执行函数之前, 你必须要创建函数. 换句话说, 在你调用函数之前, 函数定义代码必须已被执行. 

练习 3.1 将这段程序的最后一行移到最开始, 也就是使得函数调用在函数定义之前, 运行程序, 看看你会得到怎样的错误信息.

练习 3.2 将这段程序的 `repeat_lyrics` 函数定义移到 `priny_lyrics` 函数定义的前面, 运行程序会发生什么事?