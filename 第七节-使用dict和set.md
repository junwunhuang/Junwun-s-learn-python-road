### 1、字典（dict）

python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value\)存储，具有极快的查找速度。

举个例子，要根据同学的名字查找对应的成绩，如果用list实现，需要两个list:

```py
names = ['Tom', 'James', 'Bob']
scores = [94, 85, 60]
```

给定一个名字，要查找对应的成绩，就要先在names中找到对应的位置，再从scores取出对应的成绩，list越长，耗时越长。

如果用dict实现，只需要一个“名字"-"成绩“的对照表，直接根据名字查找成绩，无论这个表有多大，查找速度都不会变慢。

```py
>>> d = {'Tom': 94, 'James': 85, 'Bob': 60}
>>> d['Tom']
94
```

为什么dict查找速度这么快？因为dict的实现原理和查字典是一样的。dict这种key-value存储方式，在放进去的时候，必须根据key算出value的存放位置，这样，取的时候才能根据key直接拿到value。

把数据放入dict的方法，除了初始化时指定外，还可以通过key放入；而由于一个key只能对应一个value，所以，多次对一个key放入value，后面的后面的值会把前面的值冲掉：

```py
>>> d['Green'] = 90
>>> d['Green']
90
>>> d['Green'] = 99
>>> d['Green']
99
```

如果key不存在，dict就会报错：

```py
>>> d['Amy']
Traceback (most recent call last):
  File "<pyshell#47>", line 1, in <module>
    d['Amy']
KeyError: 'Amy'
```

要避免key不存在的错误，有两种办法，一是通过in判断key是否存在：

```py
>>> 'Amy' in d
False
```

二是通过dict提供的get方法，如果key不存在，可以返回None，或者自己指定的value：

```py
>>> d. get('Jim')
>>> d. get('Jim',111)
111
```

注意：返回None的时候python的交互式命令行不显示结果。

要删除一个key，用pop\(key\)方法，对应的value也会从dict中删除：

```py
>>> d.pop('James')
>>> d
{'Bob': 60, 'Tom': 94}
```

请务必注意，dict内部存放的顺序和key放入的顺序是没有关系的。

和list比较，dict有以下几个特点：

* 查找和插入速度极快，不会随着key的增加而变慢；
* 需要占用大量的内存，内存浪费多。

而list相反：
* 查找和插入的时间随着元素的增加而增加；
* 占用空间小，内存浪费很少。

所以，dict是用空间换取时间的一种方法。

### _dict可以用在高速查找的很多地方，在python代码中几乎无处不在，正确使用dict非常重要，要牢记的第一条就是dict的key必须死不可变对象。_

这是因为dict根据key来计算value的存储位置，如果每次计算相同的key得出的结果不同，那dict内部就完全混乱了。这个通过key计算位置的算法称为哈希算法（Hash）。

要保证hash的正确性，作为key的对象就就不能变。在python中，字符串、整数等都是不可变的，因此，可以放心的作为key。而list是可变的，就不能作为key：

```py
>>> key = [1, 2, 3]
>>> d[key] = 'a list'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

### 2、集合（set）

set和sict类似，也是一组Key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

要创建一个set，需要提供一个list作为输入集合：

```py
>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}
```

注意，出入的参数\[1, 2, 3\]是一个list，而显示的{1， 2， 3}只是告诉你这个set内部有1，2，3这3个元素，显示的顺序也不表示set是有序的。

重复元素在set中自动被过滤：

```py
>>> s = set([1, 1, 2, 3, 3])
>>> s
{1, 2, 3}
```

通过add\(key\)方法可以添加元素到set中，可以重复添加，但不会有效果：

```py
>>> s.add(4)
>>> s
{1, 2, 3, 4}
>>> s.add(4)
>>> s
{1, 2, 3, 4}
```

通过remove\(key\)方法可以删除元素：

```py
>>> s.remove(4)
>>> s
{1, 2, 3}
```

set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做成数学意义上的交集、并集等操作：

```py
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2
{2, 3}
>>> s1 | s2
{1, 2, 3, 4}
```

set和dict的唯一区别仅在于没有存储对应的value，但是，set的原理和dict一样，所以，同样不可以放入可变对象，因为无法判断两个可变对象是否相等，也就无法保证set内部”不会有重复元素“。

### 3、再议不可变对象

str是不可变对象，而list是可变对象。

对于可变对象，如list，对list进行操作，list内部的内容是会变化的：

```py
>>> a = ['c', 'b', 'a']
>>> a.sort()
>>> a
['a', 'b', 'c']
```

而对于不可变对象，比如str，对str进行操作：

```py
>>> n = 'abc'
>>> b = n.replace('a','A')
'Abc'
>>> a
'abc'
>>> b
'Abc'
```

要始终牢记：n是变量，而'abc'才是字符串对象！有时候，我们经常说，对象n的内容是'abc'，但其实是指，a本身是一个变量，它指向的对象的内容才是'abc'。

所以，这里调用a.replace\('a', 'A'\)方法没有改变字符串'abc'的内容，而是创建了一个新的字符串'Abc'。

