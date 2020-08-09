## Python_sorter

```python
import os
print(os.stat('1.txt'))

os.stat_result(st_mode=33204, st_ino=15996114, st_dev=2050, st_nlink=1, st_uid=1000, st_gid=1000, st_size=0, st_atime=1596489117, st_mtime=1596489117, st_ctime=1596489117)
```

**st_atime** - время последнего доступа к файлу

**st_mtime** - время последнего изменения файла

**st_ctime** - время создания файла (Winfows), время последнего изменения файла (Unix)

Вывод списка с именами файлов и папок в текущей директории. 

```python
os.listdir()

['sorter.py', '1.txt', '3.txt', '2.txt', 'first']
```

Правда, я пока что не знаю как отличить по названию папку и файл без расширения.

! Еще одна проблема заключается в том в Линуксе, **st_mtime** и **st_ctime** совпадают, то есть при изменении файла, дата его создания тоже изменяется.

---

Для того чтобы перевести время в секундах в нормальный вид, для этого

```python
>>> datetime.datetime.fromtimestamp(os.stat('1.txt').st_ctime)
# datetime.datetime(2020, 8, 4, 2, 10, 50, 46134)
```

```python
>>> t_1 = os.path.getctime('1.txt')
>>> time.strftime("%d.%m.%Y %H:%M:%S", time.localtime(t_1))
'04.08.2020 00:58:23'
```

```python
>>> for f in os.listdir():
...     print(datetime.datetime.fromtimestamp(os.stat(f)[-1]))
... 
2020-08-04 00:18:51
2020-08-04 00:58:23
2020-08-04 00:11:57
2020-08-04 00:22:00
2020-08-04 00:11:57
```

---

Для того чтобы создать папку **first**

```python
os.mkdir('first')
```

Изменить имя папки

```python
os.rename('first', 'second')
```

Вывести размер файла в байтах

```python
>>> os.path.getsize('1.txt')
# 6
```

Чтобы переместить файл в папку

```python
>>> shutil.move(r"file4.txt", r"second")
```

Чтобы перейти в другую папку для этого нужно вызвать функцию, у которой описание в документации

> делает укзанный каталог текущим

```python
os.chdir('second') # сделать папку 'second' текущим
```

Возвращает кортеж из азвания файла и расширения

```python
>>> os.path.splitext('file4.txt')
# ('file4', '.txt')
```

Проверка, это файл или папка

```python
>>> os.path.isfile('1.txt')
# True
>>> os.path.isdir('second')
# True
```

