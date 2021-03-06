## Notes book python

Внешний вид приглашений определяется специальными символами

```python
>>> import sys
>>> print(sys.ps1)
#$ '>>> '
>>> print(sys.ps2)
#$ '... '
```

***

Компьютер мыслит логично, и если ваши требования ему непонятны, он мо-
жет предупредить вас, действовать иррационально (или, по крайней мере, вам
так покажется) или вообще зависнуть. Не принимайте это близко к сердцу;
помните, что в языках есть правила, и весь код, который вы пишете, должен
эти правила соблюдать.

***

```python
#!/usr/bin/env python3
print("hello world")
```

```bash
chmod +x hello.py
./hello.py
```

Можно переименовать файл и убрать расширение и он всё равно будет работать

```bash
./hello
```

***

```python
>>> print('I am', 10, 'years old')
#$ I am 10 years old
```

***

В программировании существует две важные концепции: состояния
и изменения. Состояние связано с цифровым представлением модели.
Например, если вы хотите моделировать лампочку, можно хранить
в программе ее текущий статус — включена лампочка или нет? Среди
других интересных вариантов состояния можно хранить тип лампочки
(люминесцентная, лампа накаливания), потребляемую мощность, размер,
возможность регулировки яркости и т. д.
Концепция изменения связана с переходом в новое состояние. Скажем,
в примере с лампочкой было бы полезно иметь переключатель, который
переводит лампочку в противоположное состояние: если лампочка вы-
ключена, то она включается, и наоборот.

***

Когда в программе появляются объекты с состоянием, которое может
изменяться, перед вами открывается целый мир новых возможностей.
В программе можно смоделировать практически все, что угодно, — если
вы сможете определить, каким состоянием должна обладать модель
и какие действия (или изменения) к ней должны применяться.

***

Этот объект обладает рядом интересных свойств. Во-первых, у него есть
*идентификатор*. Можно считать, что идентификатор указывает на место,
в котором Python хранит этот объект в памяти. У объекта также имеется
*тип* (в данном случае это строка). Наконец, у объекта есть *значение*.

***

Создавая переменную, Python приказывает объекту увеличить свой
счетчик ссылок. Если на объект указывают переменные или другие
объекты, то у этого объекта счетчик ссылок положителен. Когда пере-
менные перестают существовать (например, при выходе из функции
переменные из этой функции исчезают), счетчик ссылок уменьша-
ется. Когда счетчик уменьшается до 0, интерпретатор Python делает
вывод, что объект больше никому не нужен, и подвергает его уборке
мусора. Это означает, что объект удаляется из памяти, чтобы ваши
программы не выходили из-под контроля и не занимали всю память
на компьютере.

Если вы захотите узнать значение счетчика ссылок для объекта, вызовите
для него функцию **sys.getrefcount** :

```python
>>> import sys
>>> names = []
>>> sys.getrefcount(names)
#$ 2
```

Обратите внимание: значение счетчика может показаться слишком высо-
ким, но в документации этой функции говорится:

> ...Возвращает счетчик ссылок объекта. Возвращаемое значение обычно
> на 1 выше ожидаемого, потому что оно включает (временную) ссылку
> для аргумента getrefcount().

***

![image-20200427175220645](/home/sam/.config/Typora/typora-user-images/image-20200427175220645.png)

![image-20200427175245455](/home/sam/.config/Typora/typora-user-images/image-20200427175245455.png)

Рис. 6.1. Два этапа присваивания литерала. Сначала Python создает
объект. У этого объекта есть значение “off”, тип (строка) и идентификатор
(местонахождение объекта в памяти). После того как объект будет создан, Python
ищет переменную с именем status. Если такая переменная существует, Python
изменяет объект, на который указывает эта переменная; в противном случае
Python создает переменную и связывает ее с объектом

***

```python
>>> 23 + 34
#$ 57
>>> _
#$ 57
>>> _ + 9
#$ 66
```

***

![image-20200427180732029](/home/sam/.config/Typora/typora-user-images/image-20200427180732029.png)

Рис. 6.2. Повторное связывание переменных. Переменная может быть заново
связана с любым типом; Python не пытается этому как-то помешать и не выдает
предупреждений. Если с объектом не связана ни одна переменная, Python
уничтожает этот объект в процессе уборки мусора

***

Ключевые слова зарезервированы для языковых конструкций Python, поэто-
му при попытке использования их в качестве переменных Python приходит
в замешательство.
Модуль **keyword** содержит атрибут **kwlist** со списком всех ключевых слов
Python:

```python
>>> import keyword
>>> print(keyword.kwlist)
#$ 
['False', 'None', 'True', 'and', 'as', 'assert',
'break', 'class', 'continue', 'def', 'del', 'elif',
'else', 'except', 'finally', 'for', 'from', 'global',
'if', 'import', 'in', 'is', 'lambda', 'nonlocal',
'not', 'or', 'pass', 'raise', 'return', 'try',
'while', 'with', 'yield']
```

***

Правила и соглашения назначения имен в Python перечислены в документе
[«PEP 8 — Style Guide for Python Code»](https://www.python.org/dev/peps/pep-0008/). Сокращение PEP означает «Python
Enhancement Proposal», то есть «Предложение по улучшению Python» —
так называется процесс документирования функции, усовершенствования
или передовой практики для Python. Документы PEP доступны на сайте
Python.

***

Ниже перечислены встроенные имена Python, которые не следует исполь-
зовать в качестве имен переменных:

```python
>>> dir(__builtins__)
#$
['ArithmeticError', 'AssertionError',
'AttributeError', 'BaseException',
'BlockingIOError', 'BrokenPipeError',
'BufferError', 'BytesWarning', 'ChildProcessError',
'ConnectionAbortedError', 'ConnectionError',
'ConnectionRefusedError', 'ConnectionResetError',
'DeprecationWarning', 'EOFError', 'Ellipsis',
'EnvironmentError', 'Exception', 'False',
'FileExistsError', 'FileNotFoundError',
'FloatingPointError', 'FutureWarning',
'GeneratorExit', 'IOError', 'ImportError',
'ImportWarning', 'IndentationError', 'IndexError',
'InterruptedError', 'IsADirectoryError',
'KeyError', 'KeyboardInterrupt', 'LookupError',
'MemoryError', 'NameError', 'None',
'NotADirectoryError', 'NotImplemented',
'NotImplementedError', 'OSError', 'OverflowError',
'PendingDeprecationWarning', 'PermissionError',
'ProcessLookupError', 'RecursionError',
'ReferenceError', 'ResourceWarning',
'RuntimeError', 'RuntimeWarning',
'StopAsyncIteration', 'StopIteration',
'SyntaxError', 'SyntaxWarning', 'SystemError',
'SystemExit', 'TabError', 'TimeoutError', 'True',
 'TypeError', 'UnboundLocalError',
'UnicodeDecodeError', 'UnicodeEncodeError',
'UnicodeError', 'UnicodeTranslateError',
'UnicodeWarning', 'UserWarning', 'ValueError',
'Warning', 'ZeroDivisionError', '_',
'__build_class__', '__debug__', '__doc__',
'__import__', '__loader__', '__name__',
'__package__', '__spec__', 'abs', 'all', 'any',
'ascii', 'bin', 'bool', 'bytearray', 'bytes',
'callable', 'chr', 'classmethod', 'compile',
'complex', 'copyright', 'credits', 'delattr',
'dict', 'dir', 'divmod', 'enumerate', 'eval',
'exec', 'exit', 'filter', 'float', 'format',
'frozenset', 'getattr', 'globals', 'hasattr',
'hash', 'help', 'hex', 'id', 'input', 'int',
'isinstance', 'issubclass', 'iter', 'len',
'license', 'list', 'locals', 'map', 'max',
'memoryview', 'min', 'next', 'object', 'oct',
'open', 'ord', 'pow', 'print', 'property', 'quit',
'range', 'repr', 'reversed', 'round', 'set',
'setattr', 'slice', 'sorted', 'staticmethod',
'str', 'sum', 'super', 'tuple', 'type', 'vars',
'zip']
```

***

![image-20200427182916609](/home/sam/.config/Typora/typora-user-images/image-20200427182916609.png)

***

при помощи идентификатора можно показать время создания объектов
и возможно ли их изменение. Кроме того, идентификаторы косвенно
используются для проверки тождественности оператором is 

***

Многие объекты являются изменяемыми, другие неизменяемы. Изменяемые объекты
допускают изменение своего значения «на месте» — иначе говоря, их состояние можно изменить, но их идентификатор останется неизменным.
Неизменяемые объекты не позволяют изменить свое значение. Вместо
этого их переменная связывается с новым объектом, но это также приводит к изменению идентификатора переменной.
В языке Python словари и списки являются изменяемыми типами.
Строки, кортежи, целые числа и числа с плавающей точкой относятся к неизменяемым типам.

***

Python включает модуль operator с функциями для основных математиче-
ских операций. В частности, он пригодится вам при использовании таких
расширенных возможностей Python, как лямбда-функции или генераторы
списков:

```python
>>> import operator
>>> operator.add(2, 3)
#$ 5
```

***

```python
>>> 'Name: {}'.format('Paul')
#$ 'Name: Paul'
>>> 'Name: {name}'.format(name='John')
#$ 'Name: John'
>>> 'Name: {[name]}'.format({'name': 'George'})
#$ 'Name: George'
>>> 'Last: {2} First: {0}'.format('Paul', 'George', 'John')
#$ 'Last: John First: Paul'
```

***

### F-strings

```python
>>> name = 'matt'
>>> f'My name is {name}'
#$ My name is matt
>>> f'My name is {name.capitalize()}'
#$ My name is Matt

```

***

В Python также включен отладчик для пошагового выполнения кода.
Он находится в модуле с именем **pdb** .

***

### join

Нередко имеется список (см. далее в книге), и вы хотите что-то вставить
между существующими элементами. Метод .join создает новую строку
из последовательности, вставляя строку между каждой парой элементов
списка:

```python
>>> ', '.join(['1', '2', '3'])
#$ '1, 2, 3'
```

В большинстве интерпретаторов Python .join работает быстрее, чем много-
кратная конкатенация с использованием оператора + . Приведенная идиома
является стандартной.

***

None является одиночным (синглетным) экземпляром (то есть в интерпрета-
торе Python всегда хранится только одна копия None ). Идентификатор этого
значения всегда остается одним и тем же:

```python
>>> a = None
>>> id(a)
#$ 140575303591440
>>> b = None
>>> id(b)
#$ 140575303591440
>>> a is b
#$ True
```

***

Можно использовать диапазонную проверку

```python
>>> if 90 < score <=100:
    	print(score)
```

Вместо

```python
>>> if score > 90 and score <= 100:
    	print(score)
```

***

Если у нас есть множество значений и нужно проверить есть ли там определенное значение

```python
>>> name = 'Vlad'
>>> beatles = {'George', 'Ringo', 'John', 'Paul'}
>>> beatle = name in beatles
```

***

В Python списки в действительности реализуются в виде массива указателей.
Такая реализация обеспечивает быстрый произвольный доступ к элемен-
там по индексам. Кроме того, операции присоединения и удаления в конце
списка выполняются быстро (O(1)), тогда как операции вставки и удаления
в середине списка выполняются медленнее (O(n)). Если окажется, что вам
часто приходится вставлять и извлекать элементы в начале списка, лучше
использовать структуру данных **collections.deque** .

***

Для удаления элементов из списка используется метод .remove :

```python
>>> names.remove('Paul')
```

Также возможно удаление по индексу с использованием синтаксиса
с квадратными скобками:

```python
>>> del names[1]
```

***

### Сортировка

Сохраняет изменения на месте

```python
>>> names.sorted()
```

Возвращает новый сортированный список

```python
>>> sorted(names)
```

Сортировать как строки

```python
>>> things.sort(key=str)
>>> print(things)
#$ ['1', 2, 'Zebra', 'abc']
```

***

```python
>>> nums = range(5)
>>> nums
#$ range(5)
>>> list(nums)
#$ [0, 1, 2, 3, 4]

>>> even = range(2, 6)
>>> list(even)
#$ [2, 3, 4, 5]

>>> even = range(0, 11, 2)
>>> list(even)
#$ [0, 2, 4, 6, 8, 10]
```

***

Операция исключающего ИЛИ ( ^ ) возвращает множество с элементами,
присутствующими только в одном из двух множеств:

```python
>>> first_five = set([0, 1, 2, 3, 4])
>>> two_to_six = set([2, 3, 4, 5, 6])
>>> in_one = first_five ^ two_to_six
>>> print(in_one)
#$ {0, 1, 5, 6}
```

***

Сайт с бесплатными книгами

https://www.gutenberg.org/

***

Вывод элемента с его индексом

```python
>>> animals = ["cat", "dog", "bird"]
>>> for index in range(len(animals)):
    	print(index, animals[index])
#$
0 cat
1 dog
2 bird
```

***

```python
>>> animals = ["cat", "dog", "bird"]
>>> for index, value in enumerate(animals):
    	print(index, value)
#$
0 cat
1 dog
2 bird
```

***

```python
>>> animals = ["cat", "dog", "bird"]
>>> 'bird' in animals
#$ True
```

***

Если мы с помощью итерации хотим как-то изменять итерируемый список, то мы должны итерироваться либо по копии списка и изменять оригинал, либо таким образом чтобы итерируемый список во время итерации не менялся

***

Метод словаря .get('key', 'default_value') возвращает значение по заданному ключу, либо если такого ключа нет, то возвращает значение по умолчанию

***

Метод словаря .setdefault('key', 'default_value') возвращает значение со словаря по ключу, также как и предыдущий метод .get, но в отличие от него если ключ не найден, то он добавляет в словарь этот ключ и присваивает ему указанное значение по умолчанию

***

Метод .setdefault может использоваться для создания накопителя или
счетчика ключей. Например, если вы хотите подсчитать количество
людей с одним именем, это можно сделать так:

```python
names = ['Ringo', 'Paul', 'John', 'Ringo']
count = {}
for name in names:
    count.setdefault(name, 0)
    count[name] += 1
```

Без метода .setdefault программа выглядела бы так

```python
names = ['Ringo', 'Paul', 'John', 'Ringo']
count = {}
for name in names:
    if name not in count:
        count[name] = 1
    else:
        count[name] += 1
```

***

Класс defaultdict омжет автоматический назначать ноль как значение любому ключу, который еще не имеет значения. Например создади словарь который считает, сколько раз было использовано каждое слово в предложении.

```python
from collections import defaultdict

sentence = "The red for jumped over the fence and ran to the zoo for food"
words = sentence.split(' ')

d = defaultdict(int)
for word in words:
    d[word] += 1

print(d)
```

***

### Удаление из словаря

```python
>>> del my_dict['Ringo']
```

---

### Словарь

Эта структура данных играет важную роль, потому что она является одним из «строительных блоков» Python. Классы, пространства имен и модули — все это во внутренней реализации Python строится на базе словарей.