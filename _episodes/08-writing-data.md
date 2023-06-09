---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 08-writing-data.md in _episodes_rmd/
title: Writing Data
teaching: 10
exercises: 10
questions:
- "How can I save plots and data created in R?"
objectives:
- "To be able to write out plots and data from R."
keypoints:
- "Save plots using `ggsave()` or `pdf()` combined with `dev.off()`."
- "Use `write.csv` to save tabular data."
source: Rmd
---




## Збереження рисунків

Ви можете зберегти рисунок/діаграму/схему за допомогою кнопки 'Export' 
у вікні 'Plot'. Це дасть вам можливість зберегти як
.pdf або як .png, .jpg або в інших форматах зображень.

Іноді ви захочете зберегти рисунок, не створюючи їх спочатку в 
вікні 'Plot'. Можливо ви захочете зробити pdf документ з
декількома сторінками: на кожній з яких буде інший рисунок. Або можливо
ви циклічно переглядаєте кілька підмножин файлу,  будуючи структури даних з 
кожної підмножини, і ви хочете зберегти кожен малюнок. 
У ц ьому випадку ви можете використовувати більш гнучкий підхід. Функція
`pdf()`  створює новий pdf пристрій. Ви можете контролювати розмір і роздільну здатність
використовуючи аргументи функції.


~~~
pdf("Distribution-of-gdpPercap.pdf", width=12, height=4)
ggplot(data = gapminder, aes(x = gdpPercap)) +   
  geom_histogram()

# Потім ви повинні переконатися що вимкнули pdf пристрій!

dev.off()
~~~
{: .language-r}

Відкрийте цей документ і подивіться.

> ## Завдання 1
>
> Перепишіть команду 'pdf'  для друку другої
> сторінки в, показуючи поруч панель
> графік ВВП на душу населення в країнах Америки 
> у 1952-2007 роках, які ви створили в 
> попередньому епізоді. 
> 
> > ## Розв'язок до завдання  1
> >
> > 
> > ~~~
> > pdf("Distribution-of-gdpPercap.pdf", width = 12, height = 4)
> > ggplot(data = gapminder, aes(x = gdpPercap)) + 
> > geom_histogram()
> > 
> > ggplot(data = gapminder_small_2, aes(x = country, y = gdpPercap, fill = as.factor(year))) +
> > geom_col(position = "dodge") + coord_flip()
> > 
> > dev.off()
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}


Команди `jpeg`, `png` тощо. використовуються аналогічно для створення
документів у різних форматах.

## Написання даних

У якийсь момент, ви захочете виписати дані з R.

Для цього ми можемо використовувати функцію `write.csv`, яка
дуже схожа до `read.csv` з попереднього.

Давайте створимо скрипт очищення даних, для цього аналізу, ми
хочемо зосередитись тільки на даних gapminder для Австралії:


~~~
aust_subset <- filter(gapminder, country == "Australia")

write.csv(aust_subset,
  file="cleaned-data/gapminder-aus.csv"
)
~~~
{: .language-r}

Давайте відкриємо файл, щоб переконатись, що він містить дані, які ми очікуємо. Перейдіть до вашого
`cleaned-data` каталог і двічі клікніть на назву файлу. Він відкриється за допомогою
комп'ютера із розширенням `.csv` за замовчуванням. Щоб відкрити у певному
додатку, клацніть правою кнопкою миші і оберіть програму. Використання програми електронної таблиці
(наприклад Excel), щоб відкрити цей файл показує нам що у нас є правильно відформатовані дані
включаючи тільки точки даних з  Австралії. Однак, є номери рядків 
пов'язані з даними, які безкорисні для нас (вони відносяться до номерів рядків 
з gapminder data frame).

Давайте подивимось на файл довідки, щоб з'ясувати, як змінити цю поведінку.


~~~
?write.csv
~~~
{: .language-r}

За замовчування, R випише назви рядків і
стовпців при записі даних у файл.
Щоб записати цю поведінку, ми можемо зробити наступне:


~~~
write.csv(
  aust_subset,
  file="cleaned-data/gapminder-aus.csv",
  row.names=FALSE
)
~~~
{: .language-r}

> ## Завдання 2
>
> Підмножин gapminder
> дані, які включають тільки точки даних, зібраних з 1990. Запишіть нову підмножину до файла
> у каталозі `cleaned-data/`.
> 
> > ## Розв'язок до завдання 2
> >
> > 
> > ~~~
> > gapminder_after_1990 <- filter(gapminder, year > 1990)
> > 
> > write.csv(gapminder_after_1990,
> >   file = "cleaned-data/gapminder-after-1990.csv",
> >   row.names = FALSE)
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

