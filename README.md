# Знакомство с языком Nim [ черновик ]

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
Вложенные мнострочный комментарий.
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
String - это строка, нужно писать в двойных кавычках ""
```
var login: string = "wtf"
```
Int - число.
Пробелы игнорируются.
```
var age: int = 45
var mysalary  = 1_000_000
```
Float - число с плавающей запятой
```
var price: float = 45.45
```
Bool - булев тип, куда ж без него.
```
var good: bool = true
var bad: bool = false
```

### Переменные
У Nim статическая типизация по этому нужно указывать тип переменной.

Переменные объявляются ключевым словом var. 
Затем идет имя переменной. 
А после : указывают тип. 
Потом = и значение.
```
var login: string = "valgala"
```
Компилятор больно умный и может сам определять тип. 
По этому такая записть тоже правильная. Без указания типа. 
```
var login = "valgala"
```
Const - константа вычисляется во время компиляции.
Потом изменить нельзя.
```
const myos = hostOS
```
Let - переменная с одноразовым присваиванием. 
Нельзя повторно присвоить значение будет ошибка.
```
let myint = 5
```
Блоки кода разделяются пробелами. Табы не работаю, будут ошибки.
```
var
  name = "vera"
  age = 20
```

### Циклы
Пример цикла по итератору.
```
for i in countup(20,25):
    echo i
```
countup(20,25) - это итераток от 20 к 25.
for - ключевое слово которое объявляет цикл.
i - переменная куда будет попадать элемент итератора.
in - показывает из какого итератора значения.
echo - функция вывода на стандартный поток вывода.

### Ветвления
Ветвление создается словами if и else плюс :
```
if true:
    echo 1
else:
    echo 2
```

### Процедуры
Процедуры обозначаются словом proc.
Вызов делается через добавления () к имени процедуры.
```
proc print_something =
  echo "la la la"

print_something()
```