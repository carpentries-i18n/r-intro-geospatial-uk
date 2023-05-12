---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 06-dplyr.md in _episodes_rmd/
title: Data frame Manipulation with dplyr
teaching: 30
exercises: 10
questions:
- "How can I manipulate dataframes without repeating myself?"
objectives:
- " To be able to use the six main dataframe manipulation 'verbs' with pipes in  `dplyr`."
- " To understand how `group_by()` and `summarize()` can be combined to summarize datasets."
- " Be able to analyze a subset of data using logical filtering."
keypoints:
- "Use the `dplyr` package to manipulate dataframes."
- "Use `select()` to choose variables from a dataframe."
- "Use `filter()` to choose data based on values."
- "Use `group_by()` and `summarize()` to work with subsets of data."
- "Use `mutate()` to create new variables."
source: Rmd
---



Маніпулювання йафлами даних означає багато речей для багатьох дослідників, ми часто
вибираємо певні спостереження (рядки) або змінні (стовпці), ми часто групуємо 
дані за певними змінними, або навіть обчислюємо сумарну статистику. Ми можемо
виконати ці операції використовуючи звичайні базові R операції:  


~~~
mean(gapminder[gapminder$continent == "Africa", "gdpPercap"])
~~~
{: .language-r}



~~~
[1] 2193.755
~~~
{: .output}



~~~
mean(gapminder[gapminder$continent == "Americas", "gdpPercap"])
~~~
{: .language-r}



~~~
[1] 7136.11
~~~
{: .output}



~~~
mean(gapminder[gapminder$continent == "Asia", "gdpPercap"])
~~~
{: .language-r}



~~~
[1] 7902.15
~~~
{: .output}

Але це не дуже ефективно, і це може стати швидко виснажливо, тому що є 
справедливе повторення. Повторюючи своїх дій коштуватиме вам часу, як зараз так і 
пізніше, і потенційно призведе до деяких неприємних помилок.

## Пакет `dplyr` 

На щастя, пакет [`dplyr`](https://dplyr.tidyverse.org) надає ряд 
дуже корисних  функцій для маніпулювання файлами даних, таким чином зменшить
повторення, зменшить ймовірність помилок, і можливо навіть 
збереже вам деякий набір. Як додатковий бонус, ви можете побачити, що граматику `dplyr` 
легше читати.

Тут ми розглянемо 6 найбільш часто використовуваних функцій, а також використання
конвеєрів (`%>%`) для їхнього комбінування.

1. `select()`
2. `filter()`
3. `group_by()`
4. `summarize()`
5. `mutate()`

Якщо ви не встановили цей пакет раніше, зробіть наступне: 


~~~
install.packages('dplyr')
~~~
{: .language-r}

Зараз давайте завантажимо цей пакет: 


~~~
library("dplyr")
~~~
{: .language-r}

## Використання `select()`

Якщо, наприклад, ми хочемо рухатись далі лише з декількома змінними 
нашого файлу даних, ми можемо використовувати функцію `select()`. Це збереже тільки
вибрані змінні.


~~~
year_country_gdp <- select(gapminder, year, country, gdpPercap)
~~~
{: .language-r}

![](../fig/13-dplyr-fig1.png)

Якщо ми відкриємо `year_country_gdp` ми побачимо, що він містить тільки рік,
країну і рівень ВВП. Вище ми використовували 'нормальну' граматику, але сильні сторони
`dplyr` полягають у поєднанні декількох функцій за допомогою конвеєрів. Оскільки граматика конвеєрів
не схожа на все, що ми бачили раніше в R, давайте повторимо, те що ми зробили раніше
використовуючи конвеєри.


~~~
year_country_gdp <- gapminder %>% select(year,country,gdpPercap)
~~~
{: .language-r}

Щоб допомогти вам зрозуміти, чому ми написали це таким чином, давайте пройдемося по ньому крок
за кроком. Спочатку ми викликаємо «gapminder» файл даних і передаємо його, використовуючи
символ конвеєри `%>%`, до наступного кроку, який є функцією `select()`. У цьому
випадку ми не вказуємо, який об'єкт даних ми використовуємо в функції `select()` оскільки
він отримує дані з попереднього конвеєру. **Веселий факт**: Ви можливо стикалися з 
конвеєрами перед цим у терміналі. В R, символ конвеєра це`%>%` в той час як в терміналі це
`|`, але концепція така ж!

## Використання `filter()`

Якби ми зараз хотіли рухатися вперед з вищенаведеними, але тільки з країнами Європи
ми можемо поєднати `select` і `filter`


~~~
year_country_gdp_euro <- gapminder %>%
  filter(continent == "Europe") %>%
  select(year, country, gdpPercap)
~~~
{: .language-r}

> ## Завдання 1
>
> Напишіть одну команду (яка може охоплювати кілька рядків і включає конвеєри), що
> буде виробляти таблицю даних, яка має африканські цінності для `lifeExp`, `country`
> і`year`, але не для інших континентів.  Скільки рядків у вашому файлі даних
> і чому?
>
> > ## Розв'янна до завдання 1 > >
> >
> >~~~
> >year_country_lifeExp_Africa <- gapminder %>%
> >                            filter(continent=="Africa") %>%
> >                            select(year,country,lifeExp)
> >~~~
> >{: .language-r}
> {: .solution}
{: .challenge}

Як і минулого разу, спочатку ми передаємо дані gapminder до функції `filter()`, 
потім ми передаємо відфільтровану версію даних gapminder в 
функцію `select()`. **Примітка:** Порядок операцій дуже важливий в цьому
випадку. Якщо ми спочатку використаємо 'select', фільтер не зможе знайти змінну
материка, оскільки ми прибрали його на попередньому кроці. 

## Використання `group_by()` і `summarize()`

Тепер, ми повинні були зменшити похибку повторюваності того, що зможе 
бути зроблено з базою R, але до цих пір ми не зробили цього, так як ми повинні були б
повторювати вищевказане для кожного континенту. Замість `filter()`, який тільки пройде
спостереження, які відповідають вашим критеріям (in the above: `continent=="Europe"`), ми
можемо використовувати `group_by()`, який буде по суті використовувати всі унікальні критерії, які ви 
могли використати у фільтрі.


~~~
str(gapminder)
~~~
{: .language-r}



~~~
'data.frame':\t1704 obs. of  6 variables:
 $ country  : chr  "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
 $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
 $ pop      : num  8425333 9240934 10267083 11537966 13079460 ...
 $ continent: chr  "Asia" "Asia" "Asia" "Asia" ...
 $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
 $ gdpPercap: num  779 821 853 836 740 ...
~~~
{: .output}



~~~
gapminder %>% group_by(continent) %>% str()
~~~
{: .language-r}



~~~
tibble [1,704 × 6] (S3: grouped_df/tbl_df/tbl/data.frame)
 $ country  : chr [1:1704] "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
 $ year     : int [1:1704] 1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
 $ pop      : num [1:1704] 8425333 9240934 10267083 11537966 13079460 ...
 $ continent: chr [1:1704] "Asia" "Asia" "Asia" "Asia" ...
 $ lifeExp  : num [1:1704] 28.8 30.3 32 34 36.1 ...
 $ gdpPercap: num [1:1704] 779 821 853 836 740 ...
 - attr(*, "groups")= tibble [5 × 2] (S3: tbl_df/tbl/data.frame)
  ..$ continent: chr [1:5] "Africa" "Americas" "Asia" "Europe" ...
  ..$ .rows    : list<int> [1:5] 
  .. ..$ : int [1:624] 25 26 27 28 29 30 31 32 33 34 ...
  .. ..$ : int [1:300] 49 50 51 52 53 54 55 56 57 58 ...
  .. ..$ : int [1:396] 1 2 3 4 5 6 7 8 9 10 ...
  .. ..$ : int [1:360] 13 14 15 16 17 18 19 20 21 22 ...
  .. ..$ : int [1:24] 61 62 63 64 65 66 67 68 69 70 ...
  .. ..@ ptype: int(0) 
  ..- attr(*, ".drop")= logi TRUE
~~~
{: .output}

Ви помітите, що структура dataframe, де ми використовували `group_by()`
(`grouped_df`) не збігається з оригінальним `gapminder` (`data.frame`). 
`grouped_df` можна розглядати як `list`, де кожен елемент у `list` є
`data.frame` який містить лише рядки, що відповідають певному
значенню 'континент' (принаймні, у наведеному вище прикладі).

![](../fig/13-dplyr-fig2.png)

## Використання `summarize()`

Вище було трохи на нерівномірній стороні, але `group_by()` набагато більше
захоплююче у поєднанні з `summarize()`. Це дозволить нам створювати нові
змінні за допомогою функцій, які повторюються для кожного конкретного континенту
файлу даних. Тобто, використовуючи функцію `group_by()`, ми розбиваємо нашу
оригінальну таблицю даних на кілька частин, потім ми можемо запустити функції
(e.g. `mean()` або`sd()`) всередині `summarize()`.


~~~
gdp_bycontinents <- gapminder %>%
  group_by(continent) %>%
  summarize(mean_gdpPercap = mean(gdpPercap))
~~~
{: .language-r}



~~~
`summarise()` ungrouping output (override with `.groups` argument)
~~~
{: .output}



~~~
gdp_bycontinents
~~~
{: .language-r}



~~~
# A tibble: 5 x 2
  continent mean_gdpPercap
  <chr>              <dbl>
1 Africa             2194.
2 Americas           7136.
3 Asia               7902.
4 Europe            14469.
5 Oceania           18622.
~~~
{: .output}

![](../fig/13-dplyr-fig3.png)

Це дозволило нам розрахувати середній показник ВВП для кожного континенту, але він стає 
ще краще.

> ## Завдання 2
>
>
> Розрахуйте середню тривалість життя на країну.  Яка має найдовшу середню триваліть життя 
> і яка має найкоротшу середню триваліть життя?
>
> > ## Розв'язання до завдання 2 
> >
> >
> >~~~
> > lifeExp_bycountry <- gapminder %>%
> >    group_by(country) %>%
> >    summarize(mean_lifeExp=mean(lifeExp))
> >~~~
> >{: .language-r}
> >
> >
> >
> >~~~
> >`summarise()` ungrouping output (override with `.groups` argument)
> >~~~
> >{: .output}
> >
> >
> >
> >~~~
> > lifeExp_bycountry %>%
> >    filter(mean_lifeExp == min(mean_lifeExp) | mean_lifeExp == max(mean_lifeExp))
> >~~~
> >{: .language-r}
> >
> >
> >
> >~~~
> ># A tibble: 2 x 2
> >  country      mean_lifeExp
> >  <chr>               <dbl>
> >1 Iceland              76.5
> >2 Sierra Leone         36.8
> >~~~
> >{: .output}
> >
> > Інший спосіб зробити це - використовувати функцію `dplyr` - `arrange()`, яка
> > розташовує рядки в файлі даних відповідно до порядку одного або декількох
> > змінних з файлу даних. Вона має подібний синтаксис до інших функцій
> > з пакету `dplyr`. Ви можете використовувати `desc()` всередині`arrange()` для сортування
> > в порядку спададння.
> > 
> >
> >~~~
> >lifeExp_bycountry %>%
> >    arrange(mean_lifeExp) %>%
> >    head(1)
> >~~~
> >{: .language-r}
> >
> >
> >
> >~~~
> ># A tibble: 1 x 2
> >  country      mean_lifeExp
> >  <chr>               <dbl>
> >1 Sierra Leone         36.8
> >~~~
> >{: .output}
> >
> >
> >
> >~~~
> >lifeExp_bycountry %>%
> >    arrange(desc(mean_lifeExp)) %>%
> >    head(1)
> >~~~
> >{: .language-r}
> >
> >
> >
> >~~~
> ># A tibble: 1 x 2
> >  country mean_lifeExp
> >  <chr>          <dbl>
> >1 Iceland         76.5
> >~~~
> >{: .output}
> {: .solution}
{: .challenge}

Функція «group _ by ()» дозволяє групувати по множині змінних. Давайте згрупуємо по змінних «рік» і «континент».



~~~
gdp_bycontinents_byyear <- gapminder %>%
  group_by(continent, year) %>%
  summarize(mean_gdpPercap = mean(gdpPercap))
~~~
{: .language-r}



~~~
`summarise()` regrouping output by 'continent' (override with `.groups` argument)
~~~
{: .output}

Це вже досить потужно, але стає ще краще! Ви не обмежуєтеся визначенням 1 нової змінної в `summarize()`.


~~~
gdp_pop_bycontinents_byyear <- gapminder %>%
  group_by(continent,year) %>%
  summarize(mean_gdpPercap = mean(gdpPercap),
            sd_gdpPercap = sd(gdpPercap),
            mean_pop = mean(pop),
            sd_pop = sd(pop))
~~~
{: .language-r}



~~~
`summarise()` regrouping output by 'continent' (override with `.groups` argument)
~~~
{: .output}

## `count()` і `n()`

Дуже поширеною операцією є підрахунок кількості спостережень для кожної групи.
Пакет «dplyr» поставляється з двома пов'язаними функціями, які допомагають з цим.

Наприклад, якщо ми хочемо перевірити кількість країн, включених
до набору даних за 2002 рік, ми можемо використовувати функцію `count()`. Він приймає назву
одного або декількох стовпців, які містять групи, які нас цікавлять, і ми можемо
відсортувати результат в порядку спадання `sort=TRUE`:


~~~
gapminder %>%
    filter(year == 2002) %>%
    count(continent, sort = TRUE)
~~~
{: .language-r}



~~~
  continent  n
1    Africa 52
2      Asia 33
3    Europe 30
4  Americas 25
5   Oceania  2
~~~
{: .output}

Якщо нам потрібно використовувати кількість спостережень у розрахунках, функція `n()` 
дуже корисна. Наприклад, якщо ми хочемо отримати стандартну помилку 
тривалості життя на континенті:


~~~
gapminder %>%
    group_by(continent) %>%
    summarize(se_le = sd(lifeExp)/sqrt(n()))
~~~
{: .language-r}



~~~
`summarise()` ungrouping output (override with `.groups` argument)
~~~
{: .output}



~~~
# A tibble: 5 x 2
  continent se_le
  <chr>     <dbl>
1 Africa    0.366
2 Americas  0.540
3 Asia      0.596
4 Europe    0.286
5 Oceania   0.775
~~~
{: .output}

Ви також можете об'єднати кілька зведених операцій; в цьому випадку обчислюючи `minimum`, `maximum`, `mean` і `se` тривалості життя кожного континенту в кожній країні:


~~~
gapminder %>%
    group_by(continent) %>%
    summarize(
      mean_le = mean(lifeExp),
      min_le = min(lifeExp),
      max_le = max(lifeExp),
      se_le = sd(lifeExp)/sqrt(n()))
~~~
{: .language-r}



~~~
`summarise()` ungrouping output (override with `.groups` argument)
~~~
{: .output}



~~~
# A tibble: 5 x 5
  continent mean_le min_le max_le se_le
  <chr>       <dbl>  <dbl>  <dbl> <dbl>
1 Africa       48.9   23.6   76.4 0.366
2 Americas     64.7   37.6   80.7 0.540
3 Asia         60.1   28.8   82.6 0.596
4 Europe       71.9   43.6   81.8 0.286
5 Oceania      74.3   69.1   81.2 0.775
~~~
{: .output}

## Використання `mutate()`

Ми також можемо створювати нові змінні до (або навіть після) узагальнення інформації, використовуючи `mutate()`.


~~~
gdp_pop_bycontinents_byyear <- gapminder %>%
  mutate(gdp_billion = gdpPercap*pop/10^9) %>%
  group_by(continent, year) %>%
  summarize(mean_gdpPercap = mean(gdpPercap),
            sd_gdpPercap = sd(gdpPercap),
            mean_pop = mean(pop),
            sd_pop = sd(pop),
            mean_gdp_billion = mean(gdp_billion),
            sd_gdp_billion = sd(gdp_billion))
~~~
{: .language-r}



~~~
`summarise()` regrouping output by 'continent' (override with `.groups` argument)
~~~
{: .output}

## Інші хороші ресурси

* [R for Data Science](http://r4ds.had.co.nz/)
* [Data Wrangling Cheat sheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf)
* [Introduction to dplyr](https://cran.r-project.org/web/packages/dplyr/vignettes/dplyr.html)
* [Data wrangling with R and RStudio](https://www.rstudio.com/resources/webinars/data-wrangling-with-r-and-rstudio/)
