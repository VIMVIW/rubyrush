# Первая версия «Виселицы» 

В этом уроке используем все, что знаем из предыдущих. 
Напишем нашу первую более-менее 
сложную программу — игру «Виселица».

Узнаем много новых инструментов (методы массивов `include?`, `join` и `split`), научимся проектировать сложные программы, разбивая их на методы, а методы выделять в отдельный файл и подключать его с помощью команды `require`.

Эту программу будем использовать далее для освоения других тем. 
Поэтому отнеситесь к уроку особенно внимательно и ответственно.

### План урока

1. Описание игры, проектируем виселицу
1. Подключение файлов в программах, инструкция require
1. Настройка программы, улучшения и украшения

![Весёлая игра «Виселица»!](http://goodprogrammer.ru/system/rich_texts/000/000/1773de5c6bec4d07d8c2a5b1cf1e5db1d2e6b3ca227/1.jpg?1429733479 "Весёлая игра «Виселица»!")


<!-- youtube starts here -->
<script>
var video_plan = {}
</script>

<div class="embed-responsive embed-responsive-16by9 rubyrush-video" id="video-0">
<iframe src="https://www.youtube.com/embed/Xe0DrDiuLC8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<script>
video_plan["video-0"] = [{"begin":"0:06","comment":"Приветствие и план урока"},{"begin":"1:12","comment":"Виселица v. 1: Проектируем игру"},{"begin":"2:40","comment":"Учимся разбивать программу на несколько файлов, метод “require”"},{"begin":"4:20","comment":"Виселица v. 1: Пишем основную логику программы, придумывая методы, которые нам понадобятся"}]
</script>
</div>


<div class="embed-responsive embed-responsive-16by9 rubyrush-video" id="video-1">
<iframe src="https://www.youtube.com/embed/3mb_pD8f2Js" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<script>
video_plan["video-1"] = [{"begin":"0:09","comment":"Виселица v. 1: метод “get_letters”"},{"begin":"3:25","comment":"Виселица v. 1: метод “get_user_input”"},{"begin":"4:50","comment":"Виселица v. 1: метод “check_results”"}]
</script>
</div>


<div class="embed-responsive embed-responsive-16by9 rubyrush-video" id="video-2">
<iframe src="https://www.youtube.com/embed/0NnO7awYgrw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<script>
video_plan["video-2"] = [{"begin":"0:10","comment":"Виселица v. 1: метод “print_status”"},{"begin":"11:10","comment":"Запускаем программу «Виселица» в первый раз"},{"begin":"11:43","comment":"Виселица v. 1: метод “cls”"},{"begin":"12:55","comment":"Играем в Виселицу!"},{"begin":"14:04","comment":"Итоги урока"}]
</script>
</div>

 <!-- youtube ends here --> 

### Описание игры «Виселица»

Игра заключается в том, что один человек загадывает слово, а другой человек отгадывает его по буквам: отгадал — буква открывается (как в «Поле чудес»), не отгадал — засчитывается ошибка и рисуется «Виселица»: 7 ошибок и готово! :)

Если кто не понял, это была постановка задачи, которую мы уже давным-давно привыкли делать перед тем, как начинать что либо писать. Как и все программы в этом курсе, наша игра будет работать только в консоли (командной строке).

Ещё немного подготовительных работ: опишем цикл работы программы в виде блок-схемы:

![Блок-схема программы «Виселица»](http://goodprogrammer.ru/system/rich_texts/000/000/178a110a6f6e518f28cc10b9bdf1809eda00f5ce784/2.png?1429780033 "Блок-схема программы «Виселица»")

Такие блок-схемы удобно рисовать для мало-мальски сложных программ, разбивая действия программы на логически-независимые блоки.

Забегая вперёд скажем, что мы будем писать для каждого блока на этой схеме отдельный метод. Такое разбиение программы на блоки и обдумывание, из каких методов будет состоять программа называется «Проектирование программы», мы сейчас описали только самый простейший пример.

Очень важно приучить себя к этому этапу проектирования еще на несложных примерах — это значительно облегчит жизнь в будущем.

### Проектирование программы на примере виселицы

Итак, давайте рассмотрим действия на блок-схеме:

**1. Загадать слово**

Для того, чтобы загадать слово, программа будет считывать то слово, которое ввели при вызове программы из консоли

```sh
ruby viselitsa.rb Слово
```

Это `Слово` будет сохраняться в переменную для дальнейшей игры. 

О том, что слово загадано, программа сообщает пользователю, выводя соответствующую информацию на экран: «Типа слово загадано, и всё такое». Сделаем еще, чтобы программа как-то визуально подсказывала, сколько в загаданном слове букв. Для этого просто будем выводить что-то на экран подчёркивание вместо каждой буквы.

```sh
_ _ _ _ _
```

**2. Спросить букву**

После того, как слово загадано, программа должна начать процесс общения с игроком: у игрока есть только одно действие — предложить букву для проверки.

Программа будет спрашивать у игрока букву с помощью консольного ввода и команды `gets`. Как это делается, мы также разбирали в предыдущих уроках. 

**3. Проверить букву**

«Ход» пользователя, то есть, названную букву мы также будем хранить. Но сначала мы проверим, есть ли буква в загаданном слове. О том, как проверить, есть ли буква в слове мы расскажем в этом уроке дальше.

А для хранения букв (отгаданных, которые назвали и которые есть в загаданном слове, и для промахов - букв, которые были предложены, но которых в загаданном слове не оказалось) мы заведём два массива `good_letters` и `bad_letters` соответственно.


**4. Нарисовать часть виселицы**

Если игрок не угадал букву, то ему нужно об этом сообщить.

Во-первых, мы будем писать об этом обычным текстом, во-вторых, с помощью псевдографики мы будем рисовать виселицу, которая будет дорисовываться по мере увеличения количества ошибок.

Виселицу и обычный текст мы будем выводить в консоль ставшей для нас уже дежурной командой `puts`. Мы использовали её в каждом уроке, я уверен, вы помните, о чём идёт речь.

После рисования виселицы нужно либо вернуться на пункт 2 (спросить букву), если число ошибок меньше семи, либо, если ошибок 7 или больше — закончить игру, написав пользователю о том, что он проиграл.

Решать, куда двинуться после хода пользователя мы будем с помощью конструкции `if-else`, освежите в памяти, как она работает.

**5. Открыть букву**

Если игрок назвал букву, которая в слове есть, то необходимо эту букву открыть. Например, если он назвал букву «о», то загаданное ранее слово «слово» будет выглядеть вот так:

```sh
_ _ о _ о
```

Посмотрите, оно как будто немного удивилось, что его почти отгадали. Выводить слово мы будем командой `puts`.

Если после отгадывания очередной буквы в слове ещё остались прочерки, то нужно вернуть игрока на пункт 2 (спросить букву), а если игрок отгадал всё слово, то ему нужно также об этом сообщить.

Выяснять, что произойдёт дальше мы также будем с помощью конструкции `if-esle`.

**6. Вывести результат**

Если пользователь назвал последнюю букву в слове — он выиграл, если он совершил седьмую ошибку — проиграл. Мы сообщим ему об этом в конце игры с помощью всё той же команды `puts`.

Таким образом, мы примерно представили, как будем выполнять каждый этап нашей задачи на написание консольной игрушки "Виселица".

Конечно, этот проект довольно простой и в реальной жизни программисты делают всё куда бюрократичнее и писанины иногда больше, но мы сейчас лишь приблизительно описали процесс, что бы вы привыкали к важной культурной особенности написания хороших программ: перед написанием кода необходимо сесть и хотя бы немного подумать, как и что у вас будет устроено.

Теперь давайте ненадолго оставим наш план в стороне и займёмся ещё одной важной темой.

### Подключение файлов

![Янтарь с инклюзом](http://goodprogrammer.ru/system/rich_texts/000/000/179c65ba4263e6b8ea9651b75ae9d7a145304cde478/3.jpg?1429780033 "Янтарь с инклюзом")

Если вы увидели программу, состоящую из одного файла, то это либо какая-то тривиальная команда-скрипт, написанная программистом на скорую руку, либо автор программы новичок или сознательно не хочет делать всё по-человечески.

По мере увеличения объёма вашей программы, становится сложно ориентироваться в её тексте, вы начинаете забывать, что вы написали сверху, что снизу, что за чем следует и на какой строчке у вас какой метод.

Представьте, что у вас длинный-длинный рулон бумаги (не туалетной, к счастью), на котором написаны мелким шрифтом какие-то записи, связанные каким-то образом друг с другом. Сориентироваться в этом ворохе не сможет даже автор подобного шедевра.

![Паника!](http://goodprogrammer.ru/system/rich_texts/000/000/1813991024a70a7ea8c2dac1766ebed1fa14b7b915f/4.png?1429780033 "Паника!")

С другой стороны, если каждый кусочек текста аккуратно написан на отдельном листе бумаге и эти листочки логично сгруппированы по папкам, то ориентироваться в этой картотеке становится делом понимания принципов её устройства.

![Папочки для аккуратных](http://goodprogrammer.ru/system/rich_texts/000/000/182b65dc86c0516a937e178baf02768bf4481ce33e4/5.jpg?1429780033 "Папочки для аккуратных")

Различные стратегии организации файлов в проекте — предмет дискуссий суровых программистов. Это принято называть частью так называемой «Архитектуры» приложения.

Конечно, в базовом блоке мы и заикаться об этом не будем, вам это сейчас ни к чему. Главное сейчас уяснить, что делить код вашей программы на отдельные файлы — очень просто и стоит завести себе эту полезную привычку.

Как обычно, в нашей свежесозданной папке `c:\rubytut\lesson10` мы создадим два файла `methods.rb` и `viselitsa.rb`.

В первом будут лежать описания наших методов, а во втором — основная логика нашей программы, вызовы методов.

Понятно, что второй файл является более главным, значит, именно в нём мы будем подключать файл `methods.rb`.

Делается это с помощью команды `require`:

```ruby
require "./methods.rb"
```

После команды `require` необходимо указать путь к подключаемому файлу.

Вот эти два символа `./` перед названием файла указывают на то, что подключаемый файл лежит в той папке откуда запускается программа. Это значит, что программу в консоли надо будет запускать из папки с этими файлами. Пока просто учтите этот важный нюанс, в других уроках мы еще вернемся к нему.

Если бы мы положили `methods.rb` в под-папку `included`, то необходимо было бы написать в файле `viselitsa.rb` вот так:

```ruby
require "./included/methods.rb"
```

Что означает: «посмотри в той же папке, откуда запущена программа, папку `included`, а в ней посмотри файл `methods.rb`».

Не бойтесь, если Ruby не найдёт файл, который вы указали после команды `require`, он выдаст ошибку и вы сможете проверить путь.

Как же работает `require`?

Очень просто, она говорит Ruby «а теперь скопируй содержимое указанного файла в то место, где написана инструкция `require`». То есть получается один общий файл, склеенный из содержимого всех файлов, на которые написана инструкция `require`.

То есть если мы в файле `methods.rb` напишем

```ruby
puts "Подключаем методы"
```

А в файле `viselitsa.rb` напишем

```ruby
require "./methods.rb"
```

И запустим последний файл

```sh
ruby viselitsa.rb
```

То мы увидим в консоли надпись, ничего сложного и неожиданного.

```sh
Подключаем методы
```

### Основная часть программы «Виселица»

Люди придумали молоток как что-то тяжёлое, чем удобно стучать по тем местам и предметам, по которым нужно стучать.

То есть сначала люди поняли, какая стоит задача, а потом под эту задачу придумали инструмент, метод её решения.

Также и мы, сейчас напишем основную часть нашей программы, считая как будто все методы у нас уже написаны.

Во-первых, мы придумаем метод `get_letters`, который будет откуда-то брать слово загаданное и возвращать его в виде массива его букв (нам так будет удобнее). Так, чтобы мы могли сохранить его в переменную `letters`.

```ruby
letters = get_letters
```

Мы также создадим отдельные переменные для количества ошибок, угаданных букв и названных букв, которых в слове не оказалось. Первая переменная будет хранить просто число и мы запишем в неё ноль, а две других будут массивами и мы пока запишем в них по пустому массиву, которые потом будем наполнять.

```ruby
errors = 0
good_letters = []
bad_letters = []
```

Потом напишем «цикл отгадывания», который будет крутиться, пока число ошибок не станет равным 7 или слово не будет отгадано. В этом цикле нам нужно общаться с пользователем, показывая ему, что происходит, а также спрашивая у него новые буквы.

```ruby
while errors < 7 do
  # тут будем отгадывать слово
end
```

Второй метод, который мы придумаем, называется `print_status`, он будет выводить на экран текущее состояние игры, со всеми отгаданными и неотгаданными буквами, количеством ошибок и так далее. Этому методу потребуются все наши переменные (`letters`, `good_letters`, `bad_letters` и `errors`), поэтому мы передадим ему их в качестве 4-х параметров.

```ruby
print_status(letters, good_letters, bad_letters, errors)
```

В-третьих, мы придумаем метод `get_user_input`, который будет спрашивать у пользователя букву. Ему никакие параметры не нужны, но он возвращает указанную букву, которую мы сохраняем в локальную переменную `user_input`, которая доступна только внутри цикла.

```ruby
puts "\nВведите следующую букву"
user_input = get_user_input
```

И, наконец, нам нужен ещё один метод: `check_result`, который будет проверять, есть ли загаданная буква в слове. Ему, понятное дело, нужны все те же переменные, т.к. он будет не только проверять, есть ли буква из `user_input` среди букв в переменной `letters`, но и добавлять её в один из массивов `good_letters` или `bad_letters` в зависимости от того, угадал пользователь или нет.

```ruby
result = check_input(user_input, letters, good_letters, bad_letters)
```

Ещё мы решили прощать игрока, если он называет одну и ту же букву во второй раз. Чтобы это понять, нам также нужно знать, какие он загадывал буквы — для этого у нас уже есть массивы `good_letters` и `bad_letters`, которые мы передаём в наш ненаписанный пока метод `check_result`.

Чтобы в основной программе понять, попал пользователь или нет, нужно, чтобы метод `check_result` как-то об этом сообщал. Наверное вы уже догадались, что он будет что-то возвращать.

Давайте договоримся, что он будет возвращать такие значения

- 0 — пользователь отгадал букву или такая буква уже была
- 1 — пользователь отгадал букву и всё слово
- -1 — пользователь ошибся и такой буквы нет

Осталось проверить результат: если `check_input` возвращает 0, нужно просто вернуться в начало цикла, то есть мы ничего не делаем.

Если `check_input` вернул -1, то нужно увеличить счётчик ошибок на 1 (командой `+=`, освежите в памяти) и пойти дальше.

Если же `check_input` вернул 1, то нужно срочно выходить из цикла (как мы уже знаем, это можно сделать командой `break`) и поздравлять игрока с победой.

Теперь, когда наша программа уже написана, можно приступать к написанию методов. Обратите внимание, мы про каждый их них знаем все три вещи:

1. Название
2. Параметры
3. Возвращаемое значение


### Метод get_letters — загадываем слово

Перед написанием метода, как обычно, заполняем небольшую «анкету метода».

1. Название:			`get_letters`
2. Параметры:			—
3. Возвращаемое значение:	массив загаданных букв загаданного слова

Внутренняя реализация для основной программы совершенно не важна. 
Если мы захотим поменять метод ввода слова (а мы захотим это сделать в следующих уроках), 
код основной программы нам менять не придётся. В этом вся прелесть методов.

```ruby
def get_letters
  # реализация метода
end
```

Сейчас мы реализуем этот метод так: он будет брать слово из параметров запуска программы, о том, как это сделать, читайте в 8-м уроке, если забыли.

```ruby
slovo = ARGV[0]
```

Также, прямо в этом методе мы проверим, что слово вообще указали. Делаем это также, как мы это делали в 8-м уроке.

В этом случае, понятное дело, дальше мы работать не можем, поэтому выходим и пишем пользователю об этом с помощью команды `abort`, о которой мы узнали в 5-м уроке.

```ruby
if (slovo == nil || slovo == "")
  abort "Для игры введите загаданное слово в качестве аргумента при запуске программы"
end
```

И наконец, нам нужно разбить слово на буквы и вернуть командой `return`. Для этого воспользуемся методом `split`, который есть у любой строки в Ruby.

### Метод строки split

Любую строку в Ruby (да и не только в Ruby) очень легко можно разбить на части и записать их в массив. Например, если у нас есть строка, в которой через запятую записаны какие-то слова:

```ruby
"ночь,улица,фонарь,аптека"
```

То с помощью метода `split` мы можем переделать эту строку в массив с отдельными словами.

Этому методу всего лишь нужно указать, что слова разделены запятой. Мы знаем, что у методов есть параметры и именно они при вызове указываются в скобочках. Поэтому в качестве параметра методу `split` мы передаём строку, содержащую разделитель, в нашем случае, **запятую**. Смотрите.

```ruby
a = "Ночь,улица,фонарь,аптека".split(",")
b = ["ночь","улица","фонарь","аптека"]
```

Переменные `a` и `b` после этого будут указывать на абсолютно одинаковые объекты. А команда

```ruby
puts "Ночь,улица,фонарь,аптека".split(",")[2]
```

Выведет в консоль слово «фонарь», потому что если нам нужен третий элемент массива, нам нужно после него в квадратных скобках указать цифру 2.

Если же методу `split` в качестве параметра передать пустую строку (то есть, просто две кавычки `""`), то он разобьёт слово по буквам (типа разделитель — пустота между буквами, не пробелы, а именно пустота):

```ruby
puts "фонарь".split("")[0]
```

Выведет в консоль букву «ф».

Вообще, в Ruby со строками можно много чего делать, подробнее смотрите по [ссылке](http://ruby-doc.org/core-2.2.0/String.html).

Наконец, когда мы знаем, как работает метод `split`, можем вернуться к написанию нашего метода `get_letters` и завершить его.

Как мы уже помним, в системе Windows все данные в консоли передаются в программы в собственной кодировке, поэтому нам нужно будет конвертировать указанное слово в кодировку UTF-8 с помощью знакомой нам конструкции.

```ruby
slovo.encode("UTF-8")
```

Вот так метод должен выглядеть в конце концов:

```ruby
def get_letters
  slovo = ARGV[0]

  if (slovo == nil || slovo == "")
    abort "Для игры введите загаданное слово в качестве аргумента при запуске программы"
  end

  return slovo.encode("UTF-8").split("")
end
```

### Метод get_user_input — спрашиваем букву

1. Название:			`get_user_input`
2. Параметры:			—
3. Возвращаемое значение:	буква, которую ввёл пользователь

Мы хорошо знаем как пользоваться командой `STDIN.gets`, но есть один нюанс: 
если пользователь просто случайно нажал `Enter`, не введя буквы, 
мы простим ему эту оплошность и спросим букву ещё раз, даже не переходя к проверке.

Ну и, как обычно для Windows нужно поменять кодировку введённой буквы в UTF-8 с помощью метода `encode`, а также, обрезать символ переноса строки `\n`, который также будет передан при нажатии клавиши `Enter` вместе с введённой буквой.

Наконец, выйдя из цикла мы вернём букву с помощью команды return.

```ruby
def get_user_input
  letter = ""

  while letter == "" do
    letter = STDIN.gets.encode("UTF-8").chomp
  end

  return letter
end
```

### Метод check_result — проверяем букву игрока

1. Название:			`check_result`
2. Параметры:			`user_input` — введённая пользователем буква,
				`letters` — массив букв загаданного слова,
				`good_letters` — массив отгаданных букв,
				`bad_letters` — массив букв, которые пользователь вводил, но которых нет в слове
3. Возвращаемое значение:	`1`, если буква, которую ввёл игрок есть в слове и игрок отгадал всё слово,
				`-1`, если буквы, которую ввёл игрок, нет в загаданном слове,
				`0` во всех других случаях

Это самый сложный метод (это видно по его анкете, кстати). Для начала проверим, не повторяется ли пользователь, посмотрим, нет ли его буквы в одном из массивов `good_letters` или `bad_letters`. Мы делаем это с помощью метода `include?`.

### Метод массива include?

Этот метод есть у любого массива в Ruby. Он возвращает `true`, если переданный в качестве параметра элемент есть в массиве, и `false`, если такого элемента в массиве нет.

```ruby
puts ["orange","banana"].include?("apple")
```

Выведет в консоль `false`, а такая строчка:

```ruby
puts ["улица","фонарь","аптека"].include?("аптека")
```

Выведет в консоль `true`. Всё довольно прозрачно, не так ли?

Итак, наш метод `check_result` с помощью встроенного в Ruby метода `include?` определяет, не вводил ли пользователь уже эту букву ранее.

Мы используем также конструкцию `if` и передаём в качестве проверочного условия два выражения, соединённые оператором ИЛИ, который записывается в коде программы как две палочки `||`:

```ruby
if good_letters.include?(user_input) || bad_letters.include?(user_input)
  return 0
end
```

Мы обещали (сами себе), что метод будет возвращать `0` если пользователь вводит букву, которую уже вводил. Так и поступим.

Теперь пора проверить, есть ли введённая буква в загаданном слове. Мы снова пользуется методом `include?` — именно поэтому мы и решили хранить наше загаданное слово в виде массива букв, а не в виде строчки (к слову, у строк в Ruby тоже есть метод `include?` — информация для любознательных).

Если введённая буква есть в загаданном слове, мы добавляем эту букву к отгаданным, в массив `good_letters`, с помощью клювиков:

```ruby
if letters.include? user_input
  good_letters << user_input
end
```

Теперь нам надо проверить, не отгадал ли игрок всё слово. Проверка на то, что пользователь отгадал всё слово требует от читателя небольшого логического рассуждения.

Из каких букв РАЗНЫХ состоит, например слово «книга»: `к`, `н`, `и`, `г`, `а` — всё просто, 5 разных букв, столько же, сколько и в слове. Но, например, слово «перец» состоит из меньшего количества разных букв: `п`, `е`, `р`, `ц`. Если бы кто-то загадал слово «перец» в «Виселице», а отгадывающий назвал бы букву «е», пришлось открыть бы сразу две буквы (все смотрели передачу «Поле чудес», там именно так и происходит).

Таким образом, чтобы отгадать слово «перец», нужно отгадать всего четыре разные буквы, а не пять.

Именно поэтому нам нужно проверить, что в `good_letters` букв столько, сколько РАЗНЫХ букв в загаданном слове.

### Метод массива uniq

Для того, чтобы получить массив уникальных букв загаданного слова мы воспользуемся встроенным в Ruby методом массивов `uniq`. Этот метод просто выкидывает из массива повторяющиеся объекты. В частности, если передать ему массив букв, то из всех повторяющихся букв он оставит только одну.

```ruby
puts ["a","p","p","l","e"].uniq.to_s
```

Выведет в консоль

```sh
["a", "p", "l", "e"]
```

С помощь этого метода мы и проверим, совпадает ли число отгаданных букв `good_letters.size` с числом уникальных букв загаданного слова `letters.uniq.size` (метод `size` просто возвращает число элементов в массиве, не будем останавливаться на нём подробно):

```ruby
if good_letters.uniq.size == letters.uniq.size
  return 1
else
  return 0
end
```

Мы обещали сами себе, что метод будет возвращать `1` при отгадывании всего слова. Если же пользователь отгадал букву, но игра продолжается, то мы возвращаем `0`, тоже как и обещали.

А если пользователь не отгадал букву, то мы добавляем её в неудачные попытки `bad_letters` и возвращаем `-1`, опять же, как и обещали. Поэтому в `else`-части того `if`-а, который проверял, есть ли введённая буква в загаданном слове, мы пишем:

```ruby
bad_letters << user_input
return -1
```

В результате метод `check_input` будет выглядеть вот так:

```ruby
def check_input(user_input, letters, good_letters, bad_letters)
  if good_letters.include?(user_input) || bad_letters.include?(user_input)
    return 0
  end

  if letters.include? user_input
    good_letters << user_input

    if good_letters.uniq.size == letters.uniq.size
      return 1
    else
      return 0
    end
  else
    bad_letters << user_input
    return -1
  end
end
```

### Метод print_status — вывод текущего статуса игры

Наконец, мы дошли до последнего метода, который нам надо написать. Он используется в нескольких местах — для отображения промежуточного статуса игры и для вывода результата в конце игры (проигрыш или выигрыш).

1. Название:			`print_status`
2. Параметры:			`user_input` — введённая пользователем буква,
				`letters` — массив букв загаданного слова,
				`good_letters` — массив отгаданных букв,
				`bad_letters` — массив букв, которые пользователь вводил, но которых нет в слове
3. Возвращаемое значение:	—

Когда поведение метода нетривиальное, полезно перед его реализацией записать в комментариях перед ним, что этот метод должен делать.

В этом методе нам необходимо:

1. Вывести загаданное слово, отметив в нём прочерками закрытые (ещё не отгаданные буквы), как в «Поле чудес», что-то типа

    ```sh
    _ о л о _ о
    ```

2. Показать игроку количество ошибок и уже названные буквы, которых нет в слове (те, что были названы и оказались в слове, уже указаны в первом пункте).

3. Если мы совершили семь ошибок, то метод должен написать игроку о том, что тот проиграл и наоборот, если слово отгадано, то этот метод должен поздравить игрока с победой.

Можно приступать к реализации.

Но при реализации первого же пункта мы сталкиваемся с проблемой: как в загаданном слове открыть только отгаданные буквы, а остальные вывести в виде прочерков?

Чтобы изолировать эту проблему и оставить на потом, мы заведём для этой задачи ещё один метод `get_word_for_print` и будем считать, что он уже написан.

Очевидно, этому методу нужны только два параметра — отгаданные буквы и загаданное слово.

```ruby
puts "\nСлово: " + get_word_for_print(letters, good_letters)
```

Теперь нужно указать пользователю, сколько ошибок он допустил и какие буквы не попали в цель.

```ruby
puts "Ошибки (#{errors}): #{bad_letters.join(", ")}"
```

### Метод массива join?

Метод всех массивов в Ruby `join` — антагонист для метода split. Он делает прямо противоположное, берёт массив, берёт указанные в качестве параметра разделитель в виде строки, и склеивает элементы массива в строку, вставляя между ними этот самый разделитель.

```ruby
puts ['аптека','улица','фонарь'].join("-")
```

выведет на экран

```sh
аптека-улица-фонарь
```

Ну и наконец, нужно вывести результат игры. Если игрок ошибся семь (или каким-то образом больше) раз, то нужно ему сообщить ему, что он проиграл.

Если пользователь ошибся меньше семи раз и отгадал слово — нужно ему сообщить, что он выиграл. Проверку копируем из метода `check_result`. Если слово ещё не отгадано, мы должны написать, сколько у игрока ещё осталось попыток. В конце концов, наш метод `print_status` будет выглядеть вот так:

```ruby
def print_status(letters, good_letters, bad_letters, errors)
  puts "\nСлово: " + get_word_for_print(letters, good_letters)
  puts "Ошибки (#{errors}): #{bad_letters.join(", ")}"

  if errors >= 7
    puts "Вы проиграли :("
  else
    if letters.uniq.size == good_letters.uniq.size
      puts "Поздравляем, вы выиграли!"
    else
      puts "У вас осталось попыток: " + (7 - errors).to_s
    end
  end
end
```

### Метод get_word_for_print — вывод загаданного слова как в «Поле чудес»

Пора отдать долги — написать то, что мы считали написанным. Метод, на самом деле, очень простой. Мы уже знаем всё, что нужно, чтобы его написать.

1. Название:			`get_word_for_print`
2. Параметры:			`letters` — массив букв загаданного слова,
			        `good_letters` — массив отгаданных букв
3. Возвращаемое значение:	строка с загаданным словом, в которой неотгаданные буквы заменены на прочерки

Чтобы «собрать» слово для вывода на экран, мы заведём переменную `result` и будем добавлять в неё слово по буквам с помощью цикла `for-in`.

Но если буква не отгадана, то есть, её нет в массиве `good_letters` (проверять мы будем это с помощью полюбившейся нам команды `include?`), то мы будем выводить вместо неё прочерк.

Между буквами для красоты и удобства добавим пробелы. Получится как-то так:

```ruby
def get_word_for_print(letters, good_letters)
  result = ""

  for item in letters do
    if good_letters.include?(item)
      result += item + " "
    else
      result += "__ "
    end
  end

  return result
end
```

### Метод cls — чистка экрана после загадывания слова

Мы написали нашу самую сложную программу за весь курс, с чем я вас и поздравляю.

Однако, если мы попробуем её запустить, то выясним, что отгадывающий может увидеть слово в строчке запуска. Это нам не подходит, поэтому мы напишем ещё один метод `cls`, который будет вызываться сразу после запуска программы.

Ruby, как и многие другие языки, умеет выполнять команды в консоли. То есть вести себя так, как будто бы программа вместо нас написала что-то в консоли.

Для этого в Ruby есть метод `system`. Например, после запуска такой программы мы окажемся в папке второго урока.

```ruby
system "cd c:\rubytut\lesson2"
```

Мы пока немного знаем системных команд, поэтому не будем останавливаться на этом методе подробно. Скажем только, что вот такая строчка чистит экран в консоли Windows.

```ruby
system "cls"
```

А вот такая — во всех остальных операционных системах:

```ruby
system "clear"
```

Поэтому наш метод будет выглядеть вот так.

```ruby
def cls
  system "clear" or system "cls"
end
```

И не забудьте вызвать этот метод сразу после запуска.

![Виселица!](http://goodprogrammer.ru/system/rich_texts/000/000/18320bd36e702d3a45aeabd1bdd29687083ae276846/6.png?1429780033 "Виселица!")

### Запуск программы

Осталось перейти в нашу папку в консоли и запустить её:

```ruby
cd c:\rubytut\lesson10
ruby viselitsa.rb страус
```

Обратите внимание, что после запуска программа аккуратно стирает всё из консоли, кроме основной информации — слова, количества ошибок и названных букв.

Поиграйтесь с этой замечательной программой, попросите кого-нибудь загадать вам слово и загадайте слово ему.

Обратите внимание, что наша программа пока отличает БОЛЬШИЕ буквы от маленьких. Строго говоря буква, например, «А» и «а» это две разные буквы для Ruby. Также наша первая версия виселицы различает буквы «е» и «ё».

Все эти проблемы мы исправляем в домашних заданиях к этому и следующим урокам.

Итак, дорогие друзья, мы написали сложнейшую для новичка программу.

Нам пришлось использовать много новых инструментов (методы `include?`, `join` и `split` массивов Ruby). Мы научились проектировать сложную программу, разбивать её на методы, а методы выделять в отдельный файл и подключать его с помощью команды `require`. Написанную в этом уроке программу мы будем использовать в дальнейшем.