## Telegram bot python \#1



```bash
pip install pytelegrambotapi
```

## Bot Father


 В поиске telegram находим Bot Farher'a и создаем своего бота с помощью  команды /newbot. Затем вводим имя и юзернейм. Обратите внимание, что  юзернейм должен оканчиваться на bot! 

![image](https://habrastorage.org/webt/wo/5q/ol/wo5qol8zqfljoiv5qvpm83sm5ag.png)

Как вы видите нам выдали специальный api токен, с помощью которого вы сможете управлять своим ботом (в моём случае это: *776550937:AAELEr0c3H6dM-9QnlDD-0Q0Fcd65pPyAiM*). Свой токен Вы можете запомнить, но я рекомендую его записать.

## Код


 Настал момент, которого ждали все. Открываем PyCharm и создаем новый проект.

![image](https://habrastorage.org/webt/wv/x1/ek/wvx1ekh5i4fzwmohaedrqrdsuf4.png)

 Тут рекомендую поставить всё как у меня (название, конечно можно  изменить). После создания проекта, давайте создадим файл, в котором  будет наш код. Кликните правой кнопкой по папке с вашем проектом, затем  New → Python File. Отлично, начнем писать код. Импортируем библиотеку  telebot, с помощью:



```
import telebot
```


 Теперь нужно создать переменную bot. На самом деле имя переменной может быть каким угодно, но я привык писать bot.



```
bot = telebot.TeleBot('ваш токен')
```


 Напишем декоратор [bot](https://habr.com/ru/users/bot/).message_handler(), с помощью которого наш бот будет реагировать на команду /start. Для  этого в круглых скобках пишем commands=['start']. В итоге у нас должно  получиться это:



```
@bot.message_handler(commands=['start'])
```


 Если Вы попробуете запустить своего бота (ПКМ->Run), то у вас ничего  не выйдет. Во первых в конце кода мы должны прописать bot.polling(). Это нужно для того, чтобы бот не выключился сразу, а работал и проверял,  нет ли на сервере нового сообщения. А во вторых наш бот если уж и будет  проверять наличие сообщений, то всё равно ничего ответить не сможет.  Пора это исправлять! После нашего декоратора создаем функцию  start_message, которая будет принимать параметр message (название  функции может быть любым). Далее давайте реализуем отправку сообщения от самого бота. В функции пропишем bot.send_message(message.chat.id,  'Привет, ты написал мне /start'). Смотрите, что у Вас должно получиться:



```
import telebot

bot = telebot.TeleBot('776550937:AAELEr0c3H6dM-9QnlDD-0Q0Fcd65pPyAiM')

@bot.message_handler(commands=['start'])
def start_message(message):
    bot.send_message(message.chat.id, 'Привет, ты написал мне /start')

bot.polling()
```


 Проверим…

![image](https://habrastorage.org/webt/yc/j_/ib/ycj_iba4bvugurlniy1vbbwsahi.png)

 Отлично, наш бот работает! Чтобы он отвечал не только на команды, но и на сообщения, создадим новый декоратор [bot](https://habr.com/ru/users/bot/).message_handler(), а в круглые скобочки напишем content_types=['text']. Вообще существует  множество видов контента, к примеру location, photo, audio, sticker и  т.д. Но нам же нужно отвечать на текст, верно? Поэтому создаём функцию  send_text, принимающую параметр message. В функции пропишем условие:



```
@bot.message_handler(content_types=['text'])
def send_text(message):
    if message.text == 'Привет':
        bot.send_message(message.chat.id, 'Привет, мой создатель')
    elif message.text == 'Пока':
        bot.send_message(message.chat.id, 'Прощай, создатель')
```


 Если текст сообщения будет равен «Привет», то бот отвечает «Привет, мой  создатель», а если текст сообщения будет равен «Пока», то бот ответит  «Прощай, создатель». Тут думаю всё понятно. Но вы скорее всего задались  вопросом, а если пользователь пропишет «привет», ну или «пРиВет», как  быть в этой ситуации? Всё достаточно просто! В условии, после  message.text напишите функцию .lower(), а в тексте все заглавные буквы  замените на строчные. Теперь наш бот отвечает не только на «привет», но и на «ПривеТ», и даже «пРиВеТ».

![image](https://habrastorage.org/webt/fj/4f/ha/fj4fhaph66c_szwnv6vy4n4ytqu.png)

 Вот что у вас должно получиться:



```
import telebot

bot = telebot.TeleBot('776550937:AAELEr0c3H6dM-9QnlDD-0Q0Fcd65pPyAiM')

@bot.message_handler(commands=['start'])
def start_message(message):
    bot.send_message(message.chat.id, 'Привет, ты написал мне /start')

@bot.message_handler(content_types=['text'])
def send_text(message):
    if message.text.lower() == 'привет':
        bot.send_message(message.chat.id, 'Привет, мой создатель')
    elif message.text.lower() == 'пока':
        bot.send_message(message.chat.id, 'Прощай, создатель')

bot.polling()
```


 Отлично, с текстом мы разобрались, но как же отправить к примеру стикер? Всё просто! У каждого стикера есть свой id, соответственно зная id мы  сможем его отправить. Получить id стикера можно двумя способами. Первый  (простой) — через специального бота «What's the sticker id?»

![image](https://habrastorage.org/webt/qy/aa/r2/qyaar20gutlmozp-q82sq5v4r1u.png)

 Ну и второй способ, для тех, кто не ищет лёгких путей. Создаем новый декоратор [bot](https://habr.com/ru/users/bot/).message_handler(), вот только в скобочки пишем content_types=['sticker']. Далее всё как  обычно. Создаем функцию, принимающую параметр message, а вот в ней  пропишем print(message). Запускаем бота.

![img](https://habrastorage.org/webt/kc/2i/4b/kc2i4bybrgm7wxpn9iivds0rspa.png)

 Смотрите, как только я отправил стикер, он сразу же вывел информацию в  консоль, и в самом конце будет наш id стикера (file_id). Давайте сделаем так, чтобы когда пользователь отправил боту «я тебя люблю», то бот ему  ответил стикером. Создавать новый декоратор не нужно, мы просто допишем  условие, которое было до этого. Вот только вместо bot.send_message()  пропишем bot.send_sticker(), а вместо текста напишем id стикера.

![image](https://habrastorage.org/webt/ko/vd/nu/kovdnuuzi4vtdzqv8pbwxxep4mi.png)

 Поздравляю, всё получилось! Думаю как отправить аудио, фото, и  геолокацию, вы разберетесь сами. Я же хочу показать вам, как сделать  клавиатуру, которую бот покажет вам при старте. Это уже будет сделать  сложнее. Создаем переменную keyboard1, в которую запишем  telebot.types.ReplyKeyboardMarkup(). Эта функция вызывает клавиатуру.  Далее создадим ряды, но помните, что рядов может быть не больше 12! Для  того, чтобы их создать, пишем keyboard1.row(). В круглые скобочки  запишите всё что хотите, лично я напишу «Привет» и «Пока». Теперь, чтобы вызвать клавиатуру, допишем reply_markup=keyboard1 к функции отправки  сообщения при старте. Вот, что у вас должно получиться:



```
keyboard1 = telebot.types.ReplyKeyboardMarkup()
keyboard1.row('Привет', 'Пока')

@bot.message_handler(commands=['start'])
def start_message(message):
    bot.send_message(message.chat.id, 'Привет, ты написал мне /start', reply_markup=keyboard1)
```


 Запускаем бота…

![img](https://habrastorage.org/webt/wk/_w/zm/wk_wzmzm2escg0e4mllmymems0y.png)

 Вы видите, что клавиатура какая-то большая. Чтобы это исправить, нужно  просто в ReplyKeyboardMarkup() прописать True. Ну а если вы хотите,  чтобы клавиатура скрывалась, как только пользователь нажал на нее, то  напишите еще один True. Подробнее прочитать, что означают эти True вы  можете в [официальной документации](https://core.telegram.org/bots/api).



```
keyboard1 = telebot.types.ReplyKeyboardMarkup(True, True)
```


 Ну а на этом всё! Конечно, это не все возможно ботов в telegram, но основные возможности я вам показал. Спасибо за внимание.

 Исходный код:



```
import telebot

bot = telebot.TeleBot('<ваш токен>')
keyboard1 = telebot.types.ReplyKeyboardMarkup()
keyboard1.row('Привет', 'Пока')

@bot.message_handler(commands=['start'])
def start_message(message):
    bot.send_message(message.chat.id, 'Привет, ты написал мне /start', reply_markup=keyboard1)

@bot.message_handler(content_types=['text'])
def send_text(message):
    if message.text.lower() == 'привет':
        bot.send_message(message.chat.id, 'Привет, мой создатель')
    elif message.text.lower() == 'пока':
        bot.send_message(message.chat.id, 'Прощай, создатель')
    elif message.text.lower() == 'я тебя люблю':
        bot.send_sticker(message.chat.id, 'CAADAgADZgkAAnlc4gmfCor5YbYYRAI')

@bot.message_handler(content_types=['sticker'])
def sticker_id(message):
    print(message)

bot.polling()
```



 Если у вас возникли вопросы — можете мне написать в telegram [dimagorovtsov](https://habr.com/ru/users/dimagorovtsov/)