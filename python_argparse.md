## python_argparse

```python
import argparse

parser = argparse.ArgumentParser() 

# прочитать аргументы командной строки, которые были переданы
args = parser.parse_args()

print(args)
```



### добавление аргумента

```python
parser.add_argument("test")
```

`./parser.py --help`

```
usage: parser1.py [-h] test

positional arguments:
  test

optional arguments:
  -h, --help  show this help message and exit
```

---

`./parser.py sam`

```
Namespace(test='sam')
```

**test** является позиционным аргументом, то что передаётся в указанной позиции, сохраняется в переменную **test**.



### Позиционные аргументы

```python
parser.add_argument("a")
parser.add_argument("b")
```

`./parser.py -h`

```
usage: parser1.py [-h] a b

positional arguments:
  a
  b

optional arguments:
  -h, --help  show this help message and exit
```

`./parser.py 3 4`

```
Namespace(a='3', b='4')
```

Если поменять переменные в коде местами, их очередность

```python
parser.add_argument("b")
parser.add_argument("a")
```

`./parser.py 3 4`

```
Namespace(a='4', b='3')
```

В **Namespace** аргументы автоматический сортируются по алфавиту, п не по позиции при вызове.

---

Обращение к элементам

```python
print(args)
print(args.a + args.b)
```

`./parser.py 3 4`

```
Namespace(a='4', b='3')
43
```

Такой вывод, всё потому что, по умолчанию с консоли всё считываемое, это текст.

Чтобы указать какого типа должны быть входящие элементы 

#### type

```python
parser.add_argument("a", type=int)
parser.add_argument("b", type=int)
```

`./parser.py 3 4`

```
Namespace(a=3, b=4)
7
```

---

#### help

```python
parser.add_argument("a", type=int, help="First argument")
parser.add_argument("b", type=int, help="Second argument")
```

`./parser.py -h`

```
usage: parser1.py [-h] a b

positional arguments:
  a           First argument
  b           Second argument

optional arguments:
  -h, --help  show this help message and exit
```

---

---

### Именованные, опциональные аргументы

```python
parser.add_argument("-a", "--action")
```

#### default

Можно добавить значение по умолчанию

```python
parser.add_argument("-a", "--action", default="Encom")
```

`./parser.py`

```
Namespace(action='Encom')
```

`./parser.py -a Sam`

```
Namespace(action='Sam')
```

---

#### required

```python
parser.add_argument("-a", "--action", help="What?", required=True)
```

Теперь указание этого аргумента стало обязательным. Не использовать его вместе с **default**, потому что они друг друга взаимоисключают.

---

#### action="store"

```python
parser.add_argument("-a", "--action", action="store")
```

`./parser.py`

```
Namespace(action=None)
```

`./parser.py -a 10`

```
Namespace(action='10')
```

**store** по сути ничего не меняет в поведении ожидаемом, он является параметром по умолчанию.

Но у него есть такие параметры как 

### action="store_const"

```python
parser.add_argument("-a", "--action", help="Why?", action="store_const", const=10)
```

Он говорит что нам не хватает допольнительного аргумента **const**

По сути это вляется флагом с постоянным значением, потому что например мы передали **-а**

`./parser.py -a`

```
Namespace(action='10')
```

А если мы не передадим ему этот флаг **-a**

`./parser.py`

```
Namespace(action=None)
```

То есть этот флаг говорит, поставить туда 10 или не поставить.

---

#### action="store_true"/action="store_false"

Это частный случай **store_const**, только тут чисто булевские значения

```python
parser.add_argument("-a", "--action", help="Why?", action="store_true")
```

`./parser.py -a`

```
Namespace(action=True)
```

`./parser.py`

```
Namespace(action=False)
```

---

```python
parser.add_argument("-a", "--action", action="store_false")
```

`./parser.py -a`

```
Namespace(action=False)
```

`./parser.py`

```
Namespace(action=True)
```

---

#### nargs

Он говорит какое количество аргументов к параметру нужно указать

```python
parser.add_argument("-a", "--action", nargs=2)
```

`./parser.py -a 23 99`

```
Namespace(action=['23', '99'])
```

Если какой то аргумент к параметру не передать то будет выводиться ошибка.

---

#### choices

Она говорит какие доступные опции есть у моего параметра

```python
parser.add_argument("-a", "--action", choices=['1', '2', '3'])
```

То есть мы можем передать параметру **-a** только один из трех доступных опций, иначе будет выводиться ошибка.

Если мы укажем, вот так:

```python
parser.add_argument("-a", "--action", choices=['1'], type=int)
```

То параметр становится полностью сломанным, мы так или иначе попадет в одну из ограничений

---

#### dest

```python
parser("-a", "--action", dest="number")
```

`./parser.py - 23`

```
Namespace(number='23')
```



