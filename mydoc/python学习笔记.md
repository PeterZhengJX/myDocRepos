# python 学习笔记

## Python 基本语法

感觉基本语法好像没啥好写的？记住缩进<_<

### 输入输出

利用`print()`进行输出

```python
print('hello word')
```

在输出阶段需要注意的是字符串，它的一些格式，以及多个字符串的输出

利用逗号“,”输出多个字符串的时候会变成空格，也就是说在输出多个字符串的时候不用自己再考虑单独打空格的事情了

```python
print('hello','word')
```

这样之后会输出

> hello word



输入可以使用`input()`函数，同时再括号内可以加上提示字符串

```python
in = input('hint')
```

值得注意的是，**`input()`的返回值是`str`类型**，在与其它类型共同使用时，需要进行转换

### 一些格式

* 四个空格缩进
* 使用‘#’作为注释
* 使用‘:‘提示语句块

### 数据类型和变量

1. 整数：没什么特殊的，对于很大的数字可以用"_"分割，`10_000_000_000`

   **整数的大小没有限制，无限大`inf`**

2. 浮点数：需要注意的就是科学计数法，8×10<sup>10</sup>：`8e10`，8×10<sup>-10</sup>：`8e-10`

3. 字符串：可以用`''`也可以用`""`

   字符串内部包含`''`或者`""`的时候有两种方法

   * 使用`\`转义
   * 在字符串前加上`r`，表示为内部不转义，`r'字符串'`

   多行内容时，可以使用`'''...'''`表示多行内容

   ```python
   print('''第一行
   第二行
   第三行''')
   ```

4. 布尔值：True，False
5. **空值：None**

**注意：由于python是一种动态语言，变量本身的变量类型是不确定的，在运算中可以随意赋值**

另外python中可以使用`**`表示次幂，使用`/`表示除法，使用`//`表示整除

### 编码与字符串

编码：`ASCII`、`unicode`、`utf-8`

python中字符串以Unicode编码，对于单个的字符，可以用`ord()`获取其编码整数，也可以用`chr()`将编码整数转换为字符。

`str`类型和`byte`类型的表示不同，一个用`‘ABC’`，一个用`b’ABC‘`。它们之间的主要差别是，字符串类型在内存中使用Unicode存储，而字节型则是传输或保存时使用的。

在输出网络或者磁盘时，通过`encode()`方法可以把`str`类型变成`byte`类型

* 英文使用ASCII进行转换 `'str_EN'.encode("ascii")`
* 中文采用UTF-8进行转换`'str_CN'.encode("utf-8")`

同理，在从网络或者磁盘获取数据时，通过`decode()`将`byte`类型变成`str`类型

`decode()`也可以带`ascii`和`utf-8`进行有选择性的转换

**使用`len()`可以求得字符串长度**

对于`str`类型，可以求得其字符数量；对于`byte`类型可以求得其字节数量

**格式化问题**

使用`%s/d/f/x`进行占位，通过`%`和后边的数据进行连接

```python
'hello, %s' % 'peter'
'hi, %s, your %s is here.' % ('peter', 'phone')
```

注：如果不太确定用什么，`%s`可以把其它类型都转换为字符串，`%`的转义用法`%%`

也可以使用`format()`进行转换，它使用传入的参数替换占位符，占位符`{0},{1}...`

```python
'hello, {0}.'.format('peter')
```

最后一种方法是将字符串以`f`开头，这种字符串中可以用`{变量}`的形式将变量替换入字符串中。

### list和tuple

**list**

定义：`l = [e1, e2, e3]`

list就是列表，用`[]`表示，使用`len(list)`可获取其长度

如果要取其最后一个元素，可以使用`list[-1]`，从负一开始也可以获得其倒数的所有元素

* 增：`insert(index, e)`，`append(e)`
* 删：`pop()`，`pop(index)`
* 改：`list[index] = e`

list中的元素类型没有限制

**tuple**

定义：`tu = (e1, e2, e3)`

tuple也是一种列表，一旦初始化之后，每个元素指向不会改变

也可以使用`tu[index]`访问

定义只有一个元素的tuple`tu = (e1, )`，使用逗号区分括号和tuple的定义字符

如果要tuple可变的话，在其中装入一个list

### 条件判断和循环

**条件判断**

值得注意的是，判断条件不用括号，并且在判断条件之后必须加上冒号`:`，`else if`在python中被简写为`elif`

**循环**

python有两种循环：

1. `for...in...`，在这种写法种，通常使用`range(n)`生成一个从0~n - 1的序列
2. `while`循环

同样，两种循环的循环条件之后都要加上冒号`:`

### dict和set

**dict**

也就是字典，其实质就是一组组键值对，其格式通常为

```python
d = {key1:value1, key2:value2}
d[key1] = ?
```

增：`d[key3] = value3`

改：`d[key2] = value2`

删：`d.pop(key)`

判断某个值是否存在有两种方法：

1. 使用`in`判断，`key in d`，返回一个布尔值
2. 使用`get()`，`d.get(key)`，如果不存在返回一个None，同时`get`可以选择自己指定返回值，如`d.get(key, -1)`如果没找到返回-1

**dict通过哈希算法利用key计算位置，所以key的值应当是一个不可变对象**

在python种字符串和整数都是不可变的

**set**

创建时，利用一个list辅助创建，重复的元素自动过滤：`s = set([e1,e2,e2,e3])`

增：`s.add(e)`，可重复增加，但重复元素被忽略

删：`s.remove(e)`

运算：两个集合可以做数学上的并集和交集，并集利用`|`，交集利用`&`

**set本质上是没有value的dict，所以它的元素同样需要是不可变对象**

### 函数

函数的定义，使用`def`语句，`def my_func(x):`

不写返回值，不用规定形参类型，没有return语句时返回None

如果函数什么都没做，可以用一个`pass`语句来做占位符

函数的返回值是一个tuple

可以通过`return x, y`来返回，通过`x, y =  my_func()`来接受

**默认参数**

在函数调用的过程中可能使用多个参数，有时又不用

这时可以使用默认参数，设置几个参数的默认值，这时调用便不需要再传入值。

`def my_func(x, y = 1, z = 'c')`

**注：默认参数必须指向不变对象**

**可变参数**

通过在形参前加`*`，可以设置可变参数

通过在变量前加`*`，可以将list的所有元素作为可变参数传入

**关键字参数**

通过使用`**kw`，可以将dict作为关键字参数传入，同时，传入的kw是dict的拷贝，修改kw不影响dict

**命名关键字参数**

采用特殊分隔符`*`，`*`后边的阐述被视作命名关键字

命名关键字在调用时，必须通过键值对的形式输入

同时，如果函数定义中已经有了一个可变参数，那么后边的参数都是命名关键字参数

命名关键字参数也可以做缺省处理，通过默认参数的形式设置

**参数组合**

至此，我们知道了python中函数的参数一共有必选参数、默认参数、可变参数、关键字参数和命名关键字参数这五种，它们直接可以组合使用，但是组合的顺序固定。

**参数组合顺序：必选参数、默认参数、可变参数、命名关键字参数、关键字参数**

### 高级特性

**切片**

切片用于截取对象的部分数据，截取对象包括list、tuple和字符串

用法：

1. 从头开始 截取0~n的内容   `L[0:n + 1]`， 可见不包含结尾的数据
2. 从尾开始 末尾索引为-1，0~n的内容  `L[-n - 1:]`， 0~n - 1的内容`L[-n - 1:-1]`
3. 间隔着取，加入第三个参数，所有数，每隔n个取一个 `L[::n]`

**迭代**

使用`for...in`循环时，dict默认迭代key，迭代value，用`for value in d.values()`

字符串也可用于迭代

判断可迭代对象：

使用collections模块的Iterable类型，`isinstance('abc', Iterable)`

如果需要使用下标迭代呢？

通过python内置的`enumerate`函数完成

`for i, value in enumerate(l):`

同时引用两个变量的循环也很常见

`for x, y in [(x1, y1), (x2, y2)]:`

**列表生成式**

python中提供的快速生成list的表达式

生成一个0~n的list可以用`list(range(0, n + 1))`

但是如果有更加复杂的需求呢？

把元素生成表达式放在最前面，后边跟for循环，最后还可以加上过滤条件if

`[func1(x) for x in range(0: n + 1) if func2(x)]`

还可以搞两层的循环

由于for循环可以循环多变量，那么上述表达式中的x参数可以用多个参数替代

**生成器**

python提供的一种保存生成算法的机制，可以在循环中不断地生成元素

通过`next(g)`或者`for x in g:`可以不断提取其中元素

构造生成器的方法：

1. 把列表生成器的[]改成()，适用于简单的生成算法

2. 如果是复杂的生成算法，还可以用函数来表示生成器，使用yield返回数据

   即包含yeild语句的函数就是生成器

变成了生成器的函数，每次使用`next()`的时候会执行，遇到yield语句返回，下次执行的时候会在yield语句处继续执行

同时如果需要捕获这类生成器的return返回值，需要捕获StopIteration错误，通过获取错误的value值拿到返回值

**迭代器**

可以直接用于for循环的数据结构

1. 集合数据类型：list、tuple、dict、set、str
2. generator

可以被`next()`调用并不断返回下一个元素的对象叫做迭代器`Iterator`，如gennerator

集合数据类型都是`Iterable`，但是不是`Iterator`

可以使用`iter()`函数把`Iterable`对象变成`Iterator`对象

### 函数式编程

有副作用和没有副作用，这是函数式编程中的一个术语，指的是在函数中是否存在变量，如果存在变量，那么便是有副作用的。

python的函数式编程允许变量存在，所以python不是纯函数式编程语言

**高阶函数**

在python中，函数名其实是一个指向函数的变量，因此我们可以修改它的值，也可以把它当成变量来用

如果一个函数接受一个函数作为参数，那么这个函数就是高阶函数

*其实在数学意义上讲，高阶函数是指函数的幂比较大. 联系起来看，也就是指最外层的函数接受了别的函数作为其内层的变量*

**map/reduce**

`map()`函数接受两个参数，一个是函数，一个是Iterable，map将传入序列的元素依次通过函数处理，并返回一个新的Iterator

这实际上是一种对运算规则的抽象

`reduce()`同样也接受一个函数和一个Iterable序列，它将函数作用后的结果累积并返回

**filter**

`filter()`同样接收一个函数和一个序列，它所接收的函数需要返回一个布尔值决定元素是否保留

**sorted**

`sorted()`函数可以直接用于数字序列的从小到大排序，也可以传入一个key函数来实现自定义的排序

`sorted(L, key = func)`

key函数会作用于序列的每一个元素上，通过其返回结果进行排序

如果要反向排序，可以传入第三个参数`reverse = True`

**返回函数**

高阶函数除了可以把函数作为参数，还可以把函数作为返回值

*注：每一次外层函数返回的都是新的函数*

返回函数在调用时才执行，返回时是不执行的，如果返回函数包含了循环变量，那这个循环变量在函数执行时可能都是最终值。

**匿名函数**

使用lamda表示匿名函数，格式为`lamda *var: express`

**装饰器**

函数对象有一个`_name_`属性，可以拿到函数的名字

希望动态增加函数功能，但是又不希望修改函数定义的函数功能添加方式叫做装饰器decorator

两种模式，带参数和不带参数

不带参数模式：

```python
import functools
def func_outside(func):
	@functools.wraps(func)
	def func_inside(*args, **kw):
		pass
		return func(*args, **kw)
	return func_inside
```

带参数版本：

```python
import functools
def func_outside(txt):
	def decorator(func):
		@functools.wraps(func)
		def func_inside(*args, **kw):
			pass
			return func(*args, **kw)
		return func_inside
	return decorator
```

**偏函数**

利用`functools.partial`向函数传入函数对象、*args和**kw三类参数，返回的新函数叫偏函数

其作用为函数参数太多时，固定部分参数  

### 模块

对于python来说，一个文件就是一个模块，不同模块按包来组织

注意命名时不能和内置的模块起冲突，一个比较好的方法是，编写某个模块时首先`import moudle_name`，如果模块存在就会引用成功

模块的文档注释：任何模块代码的第一个字符串都会被视为模块的文档注释

文档注释之后可以加一些模块属性说明，比如`__author__`作者属性

**测试代码**

可以通过一个条件语句判断特性变量`__name__`的值，如果值是`__main__`那么说明是在命令行运行的模块文件，test可以执行

**作用域**

python中正常的函数和变量名都是公开的，如果想私有化，可以通过`__`前缀实现

通过`__`前缀和`__`后缀修饰的变量是特殊变量，可以直接引用

## 面向对象

### 面对对象基础

**类和实例**

构造方法`__init__(self, *args)`其中self是指向本身的变量

类的方法，都可以使用一个self，直接表示实例本身

在python中，还支持直接给实例绑定数据，例如`instance.age = 1`，如果实例中没有age这个数据，这可以表示给实例添加一个新的age数据

**访问限制**

通过`__`前缀可以限制属性的访问权限为私有

变量名如果类似`__veriable__`

**多态**

**多态中需要注意的是python是一种动态语言，所以没有检查，只要新对象有我们调用的方法，那就可以运行**

**获取对象信息**

使用`type()`可以获得对象类型

判断基本数据类型可以使用int、str进行判断，如`type(object) = int`

其它类型使用types模块中内置的类型

* 函数：types.FunctionType
* 内置函数：types.BuiltinFunctionType
* Lambda表达式：types.LambdaType
* 生成器：types.GeneratorType

使用`isinstance()`判断对象类型

`isinstance()`还可以判断某个变量是不是某些类型中的一种

````python
isinstance(x, (type1, type2))
````

使用`dir()`获取一个对象的所有属性和方法，返回一个包含字符串的list

通过`getattr()`、`setattr()`、`hasattr()`可以操作一个对象的状态

`getattr()`，可以获取一个对象的属性或方法，`getattr(obj, 'attr', default)`，在使用时，可以加上一个default值，用于属性不存在时返回

`setattr()`，可以为一个对象添加属性，`setattr(obj, 'new_attr', value)`

`hasattr()`，用来判断对象是否有这个属性或方法，`hasattr(obj, 'attr')`

**实例属性和类属性**

需要注意实例属性会覆盖类属性

### 面对对象高级特性

**\_\_slots\_\_**

python是动态语言，可以在运行中给实例添加属性和方法。添加属性`obj.attr = value`，添加方法`MethodType(method, obj)`

同时也可以给类直接添加方法，`class.method()`

为了限制属性的随意添加，可以使用`__slots__ = (attr)`来规定类中属性，规定之后，不在tuple中的属性便不能被添加

*注意：`__slots__`仅在当前类中有效，在子类中失效*

**@property**

把一个方法变成属性调用，用来限定某个属性的值的设置和获取，起到的是getter和setter的作用，但是在形式上，只需要在方法前加上`@property`便可以实现getter，在方法前加上`@attr.setter`便可以实现setter

**多重继承**

形式：`def Class(classlist)`，classlist中可以包含多个类

**定制类**

1. `__str__()`

   `print()`打印变量时调用的函数

2. `__repr__()`

   直接显示变量时调用的函数

3. `__iter__()`

   如果一个类想被用于`for...in`循环，则必须实现此方法，该方法返回一个迭代对象，通常和`__next__()`共同使用，通过`__next__()`不停地拿循环的下一个值

4. `__getitem__()`、`__setitem__`、`__delitem__`

   按下标获取元素，通过传入int或者slice切片来获取一个或者多个值

   设置元素值

   删除元素值

5. `__getattr__()`

   重写调用属性时的逻辑，如果找不到属性就调用此方法

6. `__call__()`

   以函数方式调用实例的处理逻辑，可以通过`callable()`判断哪些类是可调用对象

**枚举类**

形式：`v = Enum(typename, (enumlist))`

默认从1开始赋值

可以通过枚举类的派生类实现对枚举类更加灵活的使用，通过`@unique`可以限定枚举值唯一

**元类**

python可以通过`type()`动态创建类

创建方法，依次传入三个参数

1. class的名称
2. 继承的父类集合
3. 一个dict，将class的方法名称和函数绑定

要控制类的创建行为还可以使用`metaclass`，步骤是，首先创建元类，然后创建类，最终创建实例

元类从type类型派生，设置好元类之后，在创建类时，通过`metaclass = 元类`的命名关键字传入元类，在创建类时，python解释器就会调用元类的`__new__()`方法，加上新的方法，并返回修改后的定义

`__new__(cls, name, bases, attrs)`接收4个参数：当前准备创建的类对象，类的名字、类的父类集合、类的方法集合

## 错误、调试和测试

### 错误处理

**捕捉错误**

`try...except...finally`机制

如果要增加一个没有错误的处理，可以用`try...except...else...finally`

*出错分析一定要看异常栈，不然会被打死*

在捕获错误之后，可以使用python的`logging`模块记录错误信息，`logging.exception(e)`，错误会被记录到日志文件中

**抛出错误**

通过`raise`抛出错误，`raise xxxError()`

*注：尽量使用python内置的错误类型，不要自己瞎几把定义，主要怕别人和自己之后看不懂*

### 调试

**print()技术**

手动滑稽

**assert()**

`assert() express, str`，如果条件语句不符合，assert会抛出一个AssertionError的异常

通过在启动python解释器时使用`-O`，可以关闭assert

**logging**

通过logging把错误输出到文件，通过`logging.info()`可以输出一段文本

需要注意的时，logging在使用时需要通过`logging.basicConfig(level = ?)`，规定记录的异常级别，有debug、info、waring、error

**pdb**

python的调试器pdb可以使程序单步运行，通过`-m pdb`启动

输入n单步执行，输入`p v`输出v的内容

设置断点，`pdb.set_trace()`，通过命令`c`继续执行

### 单元测试

需要引用python的`unittest`模块，测试类继承于`unittest.TestCase`

在测试类中，以`test_`开头的方法被认为使测试方法，会被执行，`unittest`提供多种断言来判断测试结果

1. `assertEqual()`用于判断输出是否是期望值

2. `assertRaises()`用于判断是否抛出指定的异常

   ```python
   with self.assertRaises(errorType):
   	pass
   ```

**运行单元测试**

两种方法：

* 把测试文件当作正常的python脚本来运行，需要在文件最后加上main入口

  ```python
  if __name__ = '__main__':
  	unittest.main()
  ```

* 通过命令行参数-m unittest直接运行

  ```python
  python -m unittest filename
  ```

**setUp和tearDown**

这两个方法会在每次调用测试方法的前后分别被执行，用于一些每个测试都需要的重复操作

### 文档测试

python内置的文档测试模块可以直接提取注释中的代码并执行测试

doctest严格按照python交互式命令行的输入和输出来判断测试结果是否正确

*注：当模块正常导入的时候doctest不会执行，只有在命令行直接运行的时候才会执行*

## IO编程

### 文件读写

**读文件**

通过`open(filepath, openmode)`方法，可以打开一个文件对象，如果文件不存在，抛出IOError错误

*注：mode中，r为读权限，w为写权限，b为打开二进制文件。如果文件不是utf-8编码，还需要通过`encodeing`参数指定读取哪种编码*

文件打开之后，可以使用`read(size)`方法直接读取文件的全部内容，使用结束之后再通过`close()`方法关闭文件对象即可

```python
try:
    f = open(filepath, mode)
    print(f.read())
finally:
    if f:
        f.close()
```

由于上述方法较为繁琐，python提供了`with`语句的写法，自动关闭文件对象

```python
with open(filepath, mode) as f:
    print(f.read())
```

读取文件对象的方法还有`readline()`读取一行，`readlines()`读取全部并返回list

**file-like Object**

可以直接用`read()`直接读取的一类对象称为`file-like Object`，这些对象包括：字节流、网络流和自定义流，它们不需要继承特定的类，只需要实现`read()`方法即可

**写文件**

与读文件相同，通过`open()`打开文件对象，用`write()`写，最后关闭文件对象

### StringIO和BytesIO

**StringIO**

在内存中读写字符串

通过直接新建一个StringIO对象，相当于新在内存开辟了一个缓冲区，可以通过`getvalue()`获取对象中存储的字符串，也可以像文件读写一样读写该字符串

**BytesIO**

操作二进制串，使用方法和StringIO类似

### 操作文件和目录

**环境变量**

环境变量保存在`os.environ`变量中，以dict的形式保存

**创建删除目录**

```python
# 查看当前目录的绝对路径
os.path.abspath('.')
# 在某个目录下创建一个新目录，并显示新目录路径
os.path.join(dirpath,dirname)
# 创建一个新目录
os.mkdir(path)
# 删除一个目录
os.rmdir(path)
```

*注：os.path.join()会根据系统自动使用合适的拼接符号*

**拆分目录**

`os.path.split(path)`，把路径结尾的目录或者文件名单独拆分出来

`os.path.splitext(path)`，拆分得到文件拓展名

### 序列化(pickling)

**pickle模块**

通过`pickle.dump(obj, f)`方法可以将对象序列化成一个bytes，然后存入f文件对象

同时也可以通过`pickle.load(f)`方法从文件对象中分序列化对象

**json模块**

通过`dumps()`方法将JSON写入一个字符串，通过`loads()`或`load()`方法反序泪化

JSON在转化自定义对象的时候需要传入一个默认参数，`default = transfunc`通过函数进行转化工作，这类函数的作用就是把对象转化成dict对象

每个对象都有一个`__dict__`属性，可以通过写lamda的方法直接转化

```python
default = lamda obj: obj.__dict__
```

在反序列化时，同样需要使用`object_hook=func`绑定一个dict转对象方法

## 进程和线程

### 多进程

**在linux或者unix下创建进程**

可以直接使用os模块调用系统提供的`fork()`方法

**通用**

使用`multprocessing`模块提供的`Process`类，通过指定`target`方法和`args`形参，可以创建进程的实例，通过`start()`方法可以运行，通过`join()`方法使子进程获得cpu

```python
import os
from multiprocessing import Process

# 子进程所代表的分支流程
def sub_proc(name):
    print('sub process %s run, pid = %s' % (name, os.getpid()))
    
if __name__=='__main__':
    print ('parent process run, pid = %s' % (os.getpid(),))
    p = Process(target=sub_proc, args=('test',))
    p.start()
    p.join()
    print('back to parent process')
```

如果进程很多的情况下，可以通过进程池进行管理，python的`multiprocessing`中提供`Pool`类，在创建进程池时，可以通过传入参数控制进程池大小，通过`apply_async`方法可以加入进程。在`join`运行之前可以通过`close`方法关闭进程池不再添加线程。

```python
import os, time, random
from multiprocessing import Pool

# 子进程的分支流程
def sub_proc(name):
    print('sub process %s start, pid = %s' % (name, os.getpid()))
    start = time.time()
    times.sleep(random.random() * 10)
    end = tims.time()
    print('sub process %s end' % (name,))
    
if __name__=='__main__':
    print('parent process start, pid = %s' % (os.getpid()))
    p = Pool(4)	# 限制同时运行的大小, cpu核数决定上限
    for i in range(5):
        p.apply_async(sub_proc, args=(i,))
    p.close()
    p.join()
    print('parent process end')
```

**进程通信**

可以通过Queue、pipes等多种方式

### 多线程

python通过`_tread`和`threading`两个模块，对线程进行支持

启动一个线程就是通过传入一个函数并创建`Thread`实例，然后通过`start()`开始执行

通过`threading`模块的`current_thread()`方法可以获取线程实例

```python
import threading
t = threading.Thread(target=fun, name=porc_name)
name = threading.current_thread().name()
```

**线程锁lock**

通过`threading.lock()`可以创建一个锁，线程可以通过`lock.acquire()`竞争锁，只有一个线程可以获得锁，运行完成之后，通过`lock.release()`可以释放锁

**GIL**

python编辑器在涉及之初使用了GIL全局锁，使得任何线程在执行前必须获取此锁，而此锁在执行100条字节码之后会被编译器自动释放，所以python的多线程无法真正利用多核。

### ThreadLocal

通过`threading`模块提供的`local()`方法可以创建一个ThreadLocal对象

通过在threadlocal中添加变量的方式，可以实现线程的局部变量，在这个角度上，threadlocal有点像全局的dict变量，只不过针对每一个线程有局部变量

```python
thread_local = threading.local()
thread_local.var = var
```

### 分布式进程

通过`multiprocessing.managers`模块中的`BaseManager`实现

在master端：

* 首先需要继承这个管理器基类，构造自己的管理器MyManager

* 通过MyManager注册操作接口，以Queue为例

  ```python
  MyManager.register('queue_name', callable=lamda:my_queue)
  ```

* 之后创建MyManager的实例并绑定地址和密码

  ```python
  my_manager = MyManager(address=(ip, port), authkey=b'key')
  my_manager.start()
  ```

* 通过访问my_manager可以获取之前注册的操作接口

  ```python
  queue = MyManager.get_queue_name()
  ```

在slave端：

* 同样构造自己的管理器
* 注册操作接口，不用提供callable
* 创建管理器实例，并绑定地址和密码，通过`connect()`从网络连接
* 获取操作接口

## 正则表达式

**基础规则**

定长：

​	`\d`可以匹配一个数字，`\w`可以匹配一个字母或者数字，`.`可以匹配任意字符，`\s`表示一个空格

变长：

​	`*`标识任意个字符（包括0)，`+`表示至少一个字符，`?`表示0个或者1个字符，`{n}`表示n个字符，`{n,m}`表示n-m个字符

**进阶**

`[]`表示范围，`|`表示或者，`^`表示行开头，`$`表示行结尾

正则匹配默认是贪婪匹配，通过结尾加`?`可以使其采用非贪婪匹配

**re模块**

re模块提供`match()`方法判断是否匹配，如果匹配则返回一个Match对象，否则返回None

*注：通过正则表达式可以很轻松地划分字符串*

在正则表示式中，可以通过`()`进行分组，在返回的Match对象中，可以通过`group(n)`方法获取划为好的组，0为完整字符串，1~n

