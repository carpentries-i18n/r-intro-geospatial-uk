---
layout: page
title: "Примітки для інструктора"
---
{% include base_path.html %}

кореневий каталог: {{ relative_root_path }}

## Примітки для інструктора

## Мотивація заняття та навчальні цілі

Цей урок призначений для ознайомлення учнів з основними поняттями R, 
які їм знадобляться для того, щоб закінчити уроки 
у цьому семінарі. Він призначений для учнів, які не мають попереднього досвіду роботи з
R. Якщо учасники вашого семінару закінчили інший семінар з R від Software Carpentry чи Data Carpentry,
або пройшли інші курси з R, ви можете пропустити цей урок
і рухатись прямо в урок 
[Введення до геопросторових растрових та векторних даних з R](https://datacarpentry.org/r-raster-vector-geospatial/).

Цей урок є скороченою версією уроку SWC 
[R для відтворюваного наукового аналізу](http://swcarpentry.github.io/r-novice-gapminder). Він не охоплює візуалізацію в деталях, 
але подальший урок в цьому семінарі охоплює візуалізацію в контексті
геопросторових даних. 

## Дизайн уроку

#### [Вступ до R та RStudio]({{ relative_root_path }}/{% link _episodes/01-rstudio-intro.md %})

* Якщо ваш семінар включає урок [Вступ до гепросторових концепцій](https://datacarpentry.org/organization-geospatial/), учням
тільки представлять RStudio в контексті загального ландшафту геопросторового
програмного забезпечення.
* Запропонуйте учням відкрити RStudio і спостерігати за тим, як ви пояснюєте кожну панель. Переконайтеся, що середовище RStudio вибрано за замовчуванням, щоб учні могли повторювати за вами.
* Обов'язково поясніть, як виконувати код у вікні скрипта незалежно від того, чи використовуєте ви
кнопку Run або комбінації клавіш.
* Учні будуть використовувати кілька бібліотек в наступному уроці, тому не забудьте
ознайомити їх з тим, що таке бібліотека і як її встановити.

#### [Управління проєктами в RStudio]({{ relative_root_path }}/{% link _episodes/02-project-intro.md %})

* Переконайтесь, що учні завантажують файли даних в Завданні 1 і переміщують ці файли 
до свого каталогу `data/`. 

#### [Структури даних]({{ relative_root_path }}/{% link _episodes/03-data-structures-part1.md %})

* Учні будуть працювати з факторами на наступному уроці. Обов'язково
охопіть цей концепт.
* Якщо це необіхдно з причин часу, ви можете пропустити розділ про списки. Учні 
не вискористовують списки в решті семінару.

#### [Вивчення Data Frames]({{ relative_root_path }}/{% link _episodes/04-data-structures-part2.md %})

* Зверніть увагу на помилки і попередження, отримані з прикладів у цьому епізоді, та поясніть їх.

#### [Формування підмножин даних]({{ relative_root_path }}/{% link _episodes/05-data-subsetting.md %})

* Епізод після поточного охоплює пакет `dplyr`, який має
альтернативний механізм формування підмножин. Учням все ще потрібно вивчити 
базове формування підмножин в R, охоплене тут, оскільки `dplyr` буде працювати не у всіх ситуаціях. Однак,
приклади в решті семінару зосереджені на синтаксисі  `dplyr`.

#### [Маніпуляція фреймами даних з dplyr]({{ relative_root_path }}/{% link _episodes/06-dplyr.md %})

* Представте пакет `dplyr` як більш простий, інтуїтивно зрозуміліший спосіб формування
підмножин. 
* На відміну від інших уроків SWC і DC R, цей урок **не** включає в себе 
зміну даних з `tidyr`, оскільки він не використовується в решті семінару.

#### [Вступ до візуалізації]({{ relative_root_path }}/{% link _episodes/07-plot-ggplot2.md %})

* Цей епізод представляє `geom_col` і `geom_histogram`. Ці геоми використовуються 
у решті семінару поряд з геомами, специфічними для геопросторових даних.
* Підкресліть, що ми будемо йти набагато глибше у візуалізацію і створення
якісних графіків пізніше у цьому семінарі.

#### [Написання даних]({{ relative_root_path }}/{% link _episodes/08-writing-data.md %})

* Слухачі повинні будуть створити структуру каталогів, описану в
[Управлінні проектами з RStudio]({{ relative_root_path }}{% link _episodes/02-project-intro.md %}) для того, щоб код
в цьому епізоді працював.

#### Підсумкові зауваження

* Тепер, коли учні знають основи R, решту семінару
вони застосовуватимуть ці концепції до роботи з геопросторовими даними в R.
* Пакети та функції, специфічні для роботи з геопросторовими даними, будуть
в центрі уваги решти семінару.
* Вони матимуть багато змін для практики застосування і розширення
цих навичок на наступному уроці.

## Технічні поради та рекомендації

* Залиште близько 30 хвилин на початку кожного семінару і ще 15 хвилин 
на початку кожного сеансу для технічних труднощів, таких як WiFi і
встановлення речей (навіть якщо ви попросили учнів встановити 
заздалегідь, або ще більше, якщо не просили).

* Не забудьте насправді виконати приклади зі сторінки довідки R: файли довідки
можуть спочатку налякати, але розуміння того, як їх читати, надзвичайно
корисно.

* Не турбуйтеся про те, щоб бути правильним або знати матеріал ззаду наперед. Використовуйте
помилки як навчальні моменти: найважливіша навичка, яку ви можете передати - це як 
зневадити та виправити несподівані помилки.

## Поширені проблеми

Підлягає оформленню: Інструктори, будь ласка, додайте ситуації, з якими ви стикаєтеся, тут.


{% include links.md %}

