---
layout: reference
---
{% include base_path.html %}

## Посилання

## [Введення в R та RStudio]({{ relative_root_path }}/{% link _episodes/01-rstudio-intro.md %})

 - Використовуйте клавішу <kbd>Esc</kbd> для скасування незавершених команд або запущеного коду
(Ctrl+C), якщо ви використовуєте R з терміналу.
- Базові арифметичні операції виконуються в стандартному порядку пріоритетів:
- Дужки: `(`, `)`
- Експоненти: `^` або `**`
- Ділення: `/`
- Множення: `*`
- Додавання: `+`
- Віднімання: `-`.
- Можна використовувати наукове позначення, наприклад: `2e-3`.
- Все, що знаходиться праворуч від `#` є коментарем, R ігнорує його!
- Функції позначаються через `ім'я_функції()`. Вирази всередині дужок
обчислюються перед передачею у функцію, а
функції можуть бути вкладеними.
- Оператори порівняння: `<`, `<=`, `>`, `>=`, `==`, `!=`
- Використовуйте `all.equal` для порівняння чисел!
- `<-` - оператор присвоювання. Все, що знаходиться праворуч, обчислюється, а потім
зберігається у змінній, названій ліворуч.
- `ls` виводить список усіх створених вами змінних і функцій
- `rm` можна використовувати для їх видалення
- При присвоюванні значень аргументам функції ви _обов'язково_ повинні використовувати `=`.

## [Управління проєктами в RStudio]({{ relative_root_path }}/{% link _episodes/02-project-intro.md %})

- Для створення нового проєкту виберіть File -> New Project (Файл -> Новий проєкт)
- Деякі найкращі практики:
* Розглядайте дані як доступні лише для читання
* Зберігайте очищені дані окремо від необроблених брудних даних
* Розглядайте згенероване виведення як одноразове
* Зберігайте пов'язані дані разом
* Використовуйте послідовну схему іменування

## [Структури даних]({{ relative_root_path }}/{% link _episodes/03-data-structures-part1.md %})

- Використовуйте `read.csv()` для імпорту даних в пам'ять
- ` class()` надає вам клас даних вашого об'єкту
- R автоматично перетворює типи даних
- Функції `length()`, `nrow()`, `head()`, `tail()` та `str()` можуть бути
  корисними для перегляду даних.
- Фактори - це спеціальний клас для роботи з категоріальними даними.
- Списки забезпечують гнучкий тип даних.
- Фрейми даних є окремим випадком списків.

## [Вивчення фреймів даних]({{ relative_root_path }}/{% link _episodes/04-data-structures-part2.md %})

* R дозволяє легко імпортувати набори даних, що зберігаються віддалено
* **[Фрейми даних]({{ relative_root_path }}/05-data-structures-part2/)**
 - `?data.frame` is a key data structure. It is a `list` of `vectors`.
 - `cbind()` will add a column (vector) to a data.frame.
 - `rbind()` will add a row (list) to a data.frame.

**Корисні функції для запиту структур даних
- структура `?str`, виводить короткий опис всієї структури даних
- `?class` що це за структура даних?
- `?head` вивести перші `n` елементів (рядки для двовимірних об'єктів)
- `?tail` вивести останні `n` елементів (рядки для двовимірних об'єктів)
- `?rownames`, `?colnames`, `?dimnames` отримують або змінюють назви рядків
та імена стовпців об'єкта.
- `?length` отримують кількість елементів в атомарному векторі
- `?nrow`, `?ncol`, `?dim` отримують розмірність n-вимірного об'єкта
(Не працює для атомарних векторів та списків).
* Якщо ваш фрейм даних містить фактори, вам потрібно виконати додаткові кроки, щоб додати рядки, які містять нові значення рівнів.

- `read.csv` зчитати дані у звичайній структурі
   - `sep` аргумент для вказівки розділювача
     - "," for comma separated
     - "\t" for tab separated
   - Other arguments:
     - `header=TRUE` if there is a header row


## [Subsetting data]({{ relative_root_path }}/{% link _episodes/05-data-subsetting.md %})

 - Elements can be accessed by:
   - Index
   - Name
   - Logical vectors

- `[` single square brackets:
   - *extract* single elements or *subset* vectors
    - e.g.`x[1]` extracts the first item from vector x.
   - *extract* single elements of a list. The returned value will be another `list()`.
   - *extract* columns from a data.frame
 - `[` with two arguments to:
   - *extract* rows and/or columns of
     - matrices
     - data.frames
     - e.g. `x[1,2]` will extract the value in row 1, column 2.
     - e.g. `x[2,:]` will extract the entire second column of values.

 - `[[` double square brackets to extract items from lists.
 - `$` to access columns or list elements by name
 - negative indices skip elements


## [Data frame manipulation with dplyr]({{ relative_root_path }}/{% link _episodes/06-dplyr.md %})


 - `?select` to extract variables by name.
 - `?filter` return rows with matching conditions.
 - `?group_by` group data by one of more variables.
 - `?summarize` summarize multiple values to a single value.
 - `?mutate` add new variables to a data.frame.
 - `?count` and `?n` to tally values in the data frame.
 - Combine operations using the `?"%>%"` pipe operator.


## [Control flow]({{ relative_root_path }}/{% link _episodes/07-plot-ggplot2.md %})


 - figures can be created with the grammar of graphics:
   - `library(ggplot2)`
   - `ggplot` to create the base figure
   - `aes`thetics specify the data axes, shape, color, and data size
   - `geom`etry functions specify the type of plot, e.g. `point`, `line`, `density`, `box`
   - `geom`etry functions also add statistical transforms, e.g. `geom_smooth`
   - `scale` functions change the mapping from data to aesthetics
   - `facet` functions stratify the figure into panels
   - `aes`thetics apply to individual layers, or can be set for the whole plot
     inside `ggplot`.
   - `theme` functions change the overall look of the plot
   - order of layers matters!
   - `ggsave` to save a figure.


## [Writing data]({{ relative_root_path }}/{% link _episodes/08-writing-data.md %})

 - `write.table` to write out objects in regular format


## Glossary

{:auto_ids}
argument
:   A value given to a function or program when it runs.
    The term is often used interchangeably (and inconsistently) with [parameter](#parameter).

assign
:   To give a value a name by associating a variable with it.

body
:   (of a function): the statements that are executed when a function runs.

comment
:   A remark in a program that is intended to help human readers understand what is going on,
    but is ignored by the computer.
    Comments in Python, R, and the Unix shell start with a `#` character and run to the end of the line;
    comments in SQL start with `--`,
    and other languages have other conventions.

comma-separated values
:   (CSV) A common textual representation for tables
    in which the values in each row are separated by commas.

delimiter
:   A character or characters used to separate individual values,
    such as the commas between columns in a [CSV](#comma-separated-values) file.

documentation
:   Human-language text written to explain what software does,
    how it works, or how to use it.

floating-point number
:   A number containing a fractional part and an exponent.
    See also: [integer](#integer).

for loop
:   A loop that is executed once for each value in some kind of set, list, or range.
    See also: [while loop](#while-loop).

index
:   A subscript that specifies the location of a single value in a collection,
    such as a single pixel in an image.

integer
:   A whole number, such as -12343. See also: [floating-point number](#floating-point-number).

library
:   In R, the directory(ies) where [packages](#package) are stored.

package
:   A collection of R functions, data and compiled code in a well-defined format. Packages are stored in a [library](#library) and loaded using the library() function.

parameter
:   A variable named in the function's declaration that is used to hold a value passed into the call.
    The term is often used interchangeably (and inconsistently) with [argument](#argument).

return statement
:   A statement that causes a function to stop executing and return a value to its caller immediately.

sequence
:   A collection of information that is presented in a specific order.

shape
:   An array's dimensions, represented as a vector.
    For example, a 5×3 array's shape is `(5,3)`.

string
:   Short for "character string",
    a [sequence](#sequence) of zero or more characters.

syntax error
:   A programming error that occurs when statements are in an order or contain characters
    not expected by the programming language.

type
:   The classification of something in a program (for example, the contents of a variable)
    as a kind of number (e.g. [floating-point](#float), [integer](#integer)), [string](#string),
    or something else. In R the command typeof() is used to query a variables type.

while loop
:   A loop that keeps executing as long as some condition is true.
    See also: [for loop](#for-loop).

