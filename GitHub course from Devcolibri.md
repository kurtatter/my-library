## GitHub course from Devcolibri

### lesson 0

В начале необходимо пройти глобальную инициализацию

```bash
git config --global user.name "Sam"
```

Данное имя будет отображаться для всех наших коммитов, то есть другие разработчики будут видеть данное имя.

```bash
git config --global user.email "sam@encom.com"
```

После заходим в директорию где мы бы хотели создать свой проект

```bash
mkdir git-sample
cd git-sample/
git init 
```

Ответ

```
Инициализирован пустой репозиторий Git в /home/sam/git-sample/.git/
```

Чтобы увидеть новую папку и зайти на неё

```bash
ls -a
cd .git
```

Тут есть файл конфиг в котором сохраняются некоторые данные. Попробуем сделать локальную конфигурацию.

```bash
git config user.name "Test User"
git config user.email "test@encom.com"
```

После этого мы увидем в файле ```config``` изменения

```
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[user]
	name = Test User
	email = test@encom.com
```



### lesson 1 "Первый коммит"

Создадит местовый файл `test.txt`, напишем там что угодно. После

```bash
git add test.txt
```

Сделаем теперь коммит и сразу укажем комментарий к нашему коммиту

```bash
git commit -m "First Commit"
```

Скачаем дефолтный интерфейсный редактор в котором мы можем смотреть все наши коммиты.

```bash
sudo apt install gitk
```

После давай редактируем `test.txt` и снова закоммитим его

После изменения сначала добавляем его

```bash
git add test.txt
git commit -m "Secondary Commit"
```

Теперь наинтерес открой `gitk` и посмотри изменения.

### lesson 2 "Проверка состояния"

```bash
git status
```

### lesson 3 "Индексация файлов"

Когда мы вводим `git add test.txt`, то мы на самом деле индексируем его. То есть до индексации утилита не может видеть изменения связаные с этим файлов и может отображать неточные данные данные в `git status`,  но после индексации, она будет видеть изменения которые были сделаны с файлом.

Также если мы переименовали файл, например `test.txt` в `testio.txt`. Для гита это означает что мы удалили файл `test.txt` и создали новый файл `testio.txt`. При проверке статуса при индексации, она именно так и будет отображать. Однако после индексации она отобразит что файл был переименован. Причем если мы добавляем в индексации по именам файлов то старое имя тоже надо индексировать.

Либо есть команды для быстрой индексации файлов

Добавляем на коммит кондидат (индексируем) все файлы во всех папках

```bash
git add *
```

Индексируем файлы только в текущей директории

```bash
git add .
```



### lesson 4 "История коммитов"

Посмотреть историю коммитов

```bash
git log
```

```
commit bce5b1c485a4b67ac98dcbdc27d005b216010251 (HEAD -> master)
Author: Test User <test@encom.com>
Date:   Sun Apr 26 15:29:24 2020 +0300

    Secondary commit

commit ef87d1f2072268554149946a187bc2e3a1608feb
Author: Test User <test@encom.com>
Date:   Sun Apr 26 14:29:42 2020 +0300

    Secondary commit

commit 40b66df75bcffd66ad8b277b34516ec7cc78bd0e
Author: Test User <test@encom.com>
Date:   Sun Apr 26 14:27:00 2020 +0300

    First Commit
```

Если вводить с некоторыми настройками

```bash
git log --pretty=oneline
```

```
bce5b1c485a4b67ac98dcbdc27d005b216010251 (HEAD -> master) Secondary commit
ef87d1f2072268554149946a187bc2e3a1608feb Secondary commit
40b66df75bcffd66ad8b277b34516ec7cc78bd0e First Commit
```

```bash
git log --pretty=oneline --max-count=2
```

```
bce5b1c485a4b67ac98dcbdc27d005b216010251 (HEAD -> master) Secondary commit
ef87d1f2072268554149946a187bc2e3a1608feb Secondary commit
```

```bash
git log --pretty=oneline --all
git log --pretty=oneline --author="Test User"
```

```bash
git log --pretty=format:"%h - %s : %ad [%an]"
```

```
bce5b1c - Secondary commit : Sun Apr 26 15:29:24 2020 +0300 [Test User]
ef87d1f - Secondary commit : Sun Apr 26 14:29:42 2020 +0300 [Test User]
40b66df - First Commit : Sun Apr 26 14:27:00 2020 +0300 [Test User]
```

```bash
git log --pretty=format:"%h - %s : %ad [%an]" --date=short
```

```
bce5b1c - Secondary commit : 2020-04-26 [Test User]
ef87d1f - Secondary commit : 2020-04-26 [Test User]
40b66df - First Commit : 2020-04-26 [Test User]
```

### lesson 5 "Git checkout"

Checkout нужен для того чтобы переключиться на определенный коммит определенной ветки дерева. Точки остановы snapshot's.

Для того чтобы вернуться на определенный коммит, нужно знать хэш коммита (из логов)

```bash
git checkout 40b66df
```

Если что-то пошло не так и какой-то функционал перестал работать, то с помощью данной команды. Чекаем и находим коммит когда всё работало и после переходим обратно в текущее состояние и исправляем всё.

```bash
git checkout master
```

вместо master мы сможем написать название нашей ветки если нужно  будет.



### lesson 6 "Отмена индексированных файлов"

Мы можем вернуть состояние либо всей ветки, либо всего коммита, либо отдельного файла

```bash
git reset HEAD testos.txt
```

HEAD - это то последнее состояние в котором был, в нашем случае файл, до того как были произведены в нём изменения. Либо вместо HEAD можно указать хэш нужного коммита как в предыдущем уроке.

Теперь гит забыл про изменения в указанном файлов, будто он его и не индексировал. Но состояние самого файла не вернулось к нужному значению. И чтобы окончательно удалить изменения, нужно

```bash
git checkout testos.txt
```



### lesson 7 "Revert - Отмена коммита"

Если нам нужно вернуться в состояние прошлого коммита

```bash
git revert HEAD --no-edit
```

Реверт останется в истории. Есть другой способ без сохранения в истории но лучше этим не пользоваться. Если выполнять эту команду то он будет всё дальше и дальше откатываться в коммита, вплоть до изначального состояния. Либо вместо HEAD можно указать хэш нужного коммита. Но вполне вероятно возникнет конфликтная ситуация которую гит не смог сразу решить.



### lesson 8 "Решение простого конфликта"

Если не хотим исправлять конфликт и поняли что сделали это ошибочно, то можно ввести

```bash
git revert --abort
```

Но если хотим исправить, то

Исправляем сначала ошибку, потом 

```bash
git revert --continue
```

либо коммитим, я если честно совсем не понял этот урок, в комментах куча замечаний, так что может это и не так страшно.



### lesson 9 "Ветки и их применение"

Посмотреть все ветки

```bash
git branch
```

Создадим новую ветку testbranch

```bash
git checkout -b testbranch
```

Git Flow

Переключиться на ветку master

```bash
git checkout master
```

