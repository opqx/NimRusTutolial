# Знакомство с синтаксисом языка Nim [ черновик ]

- [сайт проекта](https://nim-lang.org/ "Язык программирования Nim.")
- [репозиторий проекта](https://github.com/nim-lang/Nim "Git Nim.")
>Текущая версия Nim 0.17.2

### Комментарии

Однострочный комментарий.
```
# какой-то комментарий
```
Многострочный комментарий.
```
#[
комментарий
на несколько
строк
]#
```
Вложенные мнострочные комментарии.
```
#[
вложенный
 #[комментарий]#
 #[на #[несколько]# ]#
строк
]#

```

### Типы данных

В одинарных кавычках помещают символы.
```
var ch: char = 'a'
var tab: char = '\t'
```
**String** - это строка, нужно писать в двойных кавычках ""
```
var login: string = "wtf"
```
**Int** - число.
Пробелы игнорируются.
```
var age: int = 45
var mysalary  = 1_000_000
```
**Float** - число с плавающей запятой
```
var price: float = 45.45
```
**Bool** - булев тип, куда ж без него.
```
var good: bool = true
var bad: bool = false
```

### Переменные
У Nim статическая типизация по этому нужно указывать тип переменной.

Переменные объявляются ключевым словом **var**. 
Затем идет имя переменной. 
А после **:** указывают тип. 
Потом **=** и значение.
```
var login: string = "valgala"
```
Компилятор больно умный и может сам определять тип. 
По этому такая записть тоже правильная. Без указания типа. 
```
var login = "valgala"
```
**Const** - константа вычисляется во время компиляции.
Потом изменить нельзя.
```
const myos = hostOS
```
**Let** - переменная с одноразовым присваиванием. 
Нельзя повторно присвоить значение будет ошибка.
```
let myint = 5
```
Блоки кода разделяются пробелами. Табы не работают, будут ошибки.
```
var
  name = "vera"
  age = 20
```
### Дополнительные типы
В Nim можно определить новые типы. Делается это с помощью **type**.

**range** - позволяет определить диапазон значений, среди которых могут быть челочисленные
значения, *char* или перечисления.
```
type
  subrange = range[1..12]

var t: subrange = 1 # входит в диапазон
t = 12 # входит в диапазон
t = 15 # не входит в диапазон будет ошибка
```
**enum** - позволяет создавать новый тип *перечисления*.
Значения у этого типа могут быть только из числа перечисленных.
```
type
  enumType = enum # создаем тип enum
    one, two, three # указываем возможные значения

var a: enumType = three
var b = two
echo a
echo b
```
Значения упорядочены. Их номер можнопосмотреть через **ord**.
```
type
  enumType = enum
    one, two, three

var a: enumType = three
var b = two
echo ord(a) # 2
echo ord(b) # 1
```
Можно задать свои номера, но они должны идти по возрастанию.
Возможны промежутки *5 - 8* и это не будет ошибкой.
```
type
  enumType = enum
    one = 5, two = 8

var a = one
echo ord(a) # 5
```
Так же можно присвоить строковое значение.
```
type
  enumType = enum
    one = "Какая-то строка", two = 8

var a = one
echo ord(a) # индекс
echo a # строка
```
Или задать сразу индекс и строку.
```
type
  enumType = enum
    one = (2,"Какая-то строка"), two = 8

var a = one
echo ord(a) # индекс
echo a # строка
```
**array** - это массив фиксированного размера и одного типа.
```
type
  arrStr = array[1..3, string] # тип arrStr будет массивом из трех строк
  arrStr2 = array[3, string] # получим тот же результат
  
var myArr: arrStr = [ "asd", "sdf", "sdfg" ]
var myArr2: arrStr = [ "asd", "sdf", "sdfg", "123" ] # будет ошибка
var myArr3: arrStr = [ "asd", "sdf", ] # тоже ошибка
```
Так же массив можно создать с помощью скобок **[ ]**.
```
var arr = [1,2,3]
```
Получить доступ к элементу можно можно через все теже скобки.
```
var arr = [1,2,3]

echo arr[1]
arr[1] = 5
echo arr[1]
```
**seq** - это последовательность. Она похожа на массив, только переменной длины.
Обьявить последовательность можно с помошью **seq** и указания типа. Создается последовательность
с помощю конструкции **@[ ]**.
```
type
  myStrSeq = seq[string] # последовательность из строк
  myIntSeq = seq[int] # последовательность из чисел

var mySeq: myIntSeq # указали тип (будет числовая последоватьельность seq[int]) 
mySeq = @[] # присвоили пустую последовательность
mySeq = @[1,2,3] # присвоили последовательность из 1,2,3
```
**tuple** - кортеж, это упорядоченные значения вида ключ: значение.
Доступ к элементам возможен через `.` или `[ ]`.
```
type
  people = tuple[name: string, age: int]
  
var
  me: people = ("Dima", 30)
  friend: people
  girl: people

friend[0] = "Vova"
friend[1] = 35

girl.name = "Ira"
girl.age = 25

echo me, friend, girl 
```


### Ветвления
Ветвление создается ключевыми словами **if**, **elif**, **else** плюс **:**

Если условие между `if` и `:` верно `true` то выполниться следующий блок кода. 
```
if 2 == 2:
  echo "распечатает эту строку"
```
Если условие не верно, то выполеняется альтернативный блок кода.
```
if false:
  echo "эта процедура не отработает потому что false"
else:
  echo "а эта строка будет напечатана"
```
Если нужно дополнительное условие используется `elif`.
```
if false:
  echo "эта процедура не отработает потому что false"
elif true:
  echo "а эта строка будет напечатана"
else:
  echo "этот блок кода не отработает"
```
Еще один способ сделать ветвление через конструкцию `case`.
Между **case** и **:** пишем значение, между **of** и **:** с чем будем сравнивать,
через запятую можно перечислить несколько значений.
Где происходит совпадение тот блок кода и будет выполняться. Если все разное, то выполняется
блок **else** - он обязательный.
```
case 2
of 1:
  echo "1"
of 2,3,4:
  echo "2,3,4"
else:
  echo "ни один случай не подошел"
```


### Циклы
Пример **for** цикла по итератору.
```
for i in countup(20,25):
  echo i
```
- **countup(20,25)** - это итераток от 20 к 25.
- **for** - ключевое слово которое объявляет цикл.
- **i** - переменная куда будет попадать элемент итератора.
- **in** - показывает из какого итератора значения.
- **echo** - функция вывода на стандартный поток вывода.

Ключево слово **break** прерывает цикл.
```
for i in countup(20,30):
  if i == 25:
    break
  echo i
```

Ключевое слово **continue** завершает текущую итерацию.
```
for i in countup(20,30):
    if i > 25:
        continue
    echo i
```

Пример **while** цикла.
```
var
  counter = 1
  n = 5
while n != counter :
    echo counter
    inc(counter)
```
- **while** проверяет условие и если оно возвращает true делает итерацию цикла.
- **inc** - добавляет 1 к переменной counter.
- **echo** - функция вывода на стандартный поток вывода.

### Процедуры
Процедуры обозначаются словом **proc**.
Вызов делается через добавления **()** к имени процедуры.
```
proc print_something =
  echo "la la la"

print_something()
```
Передать *параметры* в процедуру можно добавив их в скобки после названия с указанием типа.
Не указал тип будет ошибка, не передал параметр в процедуру - ошибка.
```
proc print_something(my_string: string) =
  echo my_string

print_something("Nim классный язык программирования!")
```
Параметры *по умолчанию* добавляются после знака **=**. 
Теперь можно не передавать параметры в процедуру.
```
proc print_something(my_string: string = "Математика супер наука !") =
  echo my_string

print_something()
```
*Несколько параметров* указываются через **`,`** .
Если мы присваиваем значения по умолчанию, то можно пропустить тип.
Мы же помним что компилятор умный.
```
proc print_something(
    my_string: string = "Математика супер наука !",
    need_math = " Все знают что она нужна программисту !"
  ) =

  echo my_string, need_math

print_something()
```
Пример без значений по умолчанию.
```
proc print_something(name: string, year: int) =
  echo "Меня зовут " & name & "."
  echo "Я живу в " & $year & " году."

print_something("Фрай", 3000)
```
- **&** - конкатенация (объединение) строк.
- **$** - оператор преобразования в строку.

Можно указать тип сразу для нескольких параметров.
```
proc point(x,y,z: int) =
  echo "координаты в пространстве"
  echo "x=" & $x
  echo "y=" & $y
  echo "z=" & $z

point(10, 11, 12)
```
Переменная **return** позволяет вернуть значение из функции. 
Но мы обязательно должны указать тип возвращаемого значения.
После имени процедуры и параметров если они есть нужно поставить знак `:`
и до знака `=` указать тип.
```
proc get_string: string =
  return "Свободу попугаям !"

echo get_string()
```
Возможно делать перегрузку в процедурах.
```
proc overloadMe(x: int, y: int)=
  echo x,y

proc overloadMe(x: int)=
  echo x

overloadMe(1) 
overloadMe(1, 2)
```
Если у процедуры неуказать имя она будет анонимной.
```
var anonymous = proc(x: string)=
  echo x

anonymous("я анонимная процедура :)")
```

Пример *передачи* процедуры в качестве аргумента.
```
proc f(): int =
  return 5
  
proc wrap(function: proc)=
  echo function()
  
wrap(f)
```
Пример *возврата* процедуры в качестве аргумента.
```
proc get(): proc =
  proc res(): int =
    return 5
  return res
  
echo get()()
```

### Итераторы
Если в процедуре заменить **proc** на **iterator** а **return** на **yield** то получиться итератор.
```
iterator printItem(): int =
  for i in [1,2,3,4,5]:
    yield i
    
for i in printItem():
  echo i
```

### Преобразование типов
### Исключения
### Шаблоны
### Макросы
### Модули
### Прагмы
### Ооп
### Дженерики
Дженерики это процедуры которые могут принимать указанные типы в качестве параметров.
Между `[]` мы указываем нужные типы. `[T]` - любой тип. `[T: int|float ]` - только **int** или **float**.
```
proc dj[T](x: T)=
  echo x
  
dj(45)
dj(45.45)
dj("строка будет принята")
```
```
proc dj[T: int|float](x: T)=
  echo x
  
dj(45)
dj(45.45)
dj("будет ошибка") # ошибка не соотвествия типа
```
```
proc dj[T: int|float, D: char|string](x: T, y: D)=
  echo x
  echo y
  
dj(45,'a')
dj(45.45, "sdf")

dj("sdf", 45) # ошибка не соотвествия типа
```

### Потоки и параллелизм
### Компиляция
Для компиляции файла с исходниками нужно выполнить такую команду в консоле.
`nim c -r --verbosity:0 helloworld.nim`
* nim - вызываем компилятор и передаем ему параметры
* c - синоним *compile* говорит о том что мы хотим скомпилировать файл
* -r - сообщает что мы хотим сразу запустить скомпилированный файл
* --verbosity:0 - какую информацию выводить на поток вывода, на сколько она подробная
* helloworld.nim - файл с исходным кодом который мы хотим скомпилировать


### Ссылки
- (https://nim-lang.org/docs/manual.html)
- (https://nim-lang.org/docs/tut1.html)
- (https://nim-lang.org/docs/tut2.html)
- (https://nim-lang.org/docs/lib.html)
- (https://nim-by-example.github.io)
- (http://rosettacode.org/wiki/Category:Nim)
- (http://devdocs.io/nim/)
- (https://play.nim-lang.org/)