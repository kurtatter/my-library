## Pocketsphinx Python

### Linux

Перед сборкой необходимо удостовериться что в системе установлены следующие утилиты:

* gcc
* automake
* autoconf
* libtool
* bison
* swig (at least version 2.0)
* the Python development package
* the pulseaudio development package

О сборке все написано [здесь](https://cmusphinx.github.io/wiki/tutorialpocketsphinx/) 

Что важнее, не знаю всё вышеустановленное с этим связано или нет, но при попытке

```bash
pip3 install pocketsphinx
```

Вылазила ошибка и решением является, прежде:

```bash
sudo apt install libpulse-dev
```

Наверно это и есть последний пункт из вышеперечисленного списка.