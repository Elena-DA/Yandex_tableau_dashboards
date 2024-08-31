Построение дашбордов в Tableau
В ходе проекта мы создадим дашборды на основе данных о конференциях TED.

Описание проекта

TED (от англ. technology, education, design — «технологии, образование, дизайн») — некоммерческий фонд, который проводит популярные конференции. На них выступают специалисты из разных областей и читают лекции на актуальные социальные, культурные и научные темы. В разное время на TED-конференциях выступали математик Бенуа Мандельброт, теоретик искусственного интеллекта Марвин Минский, спортсменка Дана Ньяд и основатель Google Ларри Пейдж. В истории TED также были неоднозначные и даже скандальные выступления. Например, в 2010 году на конференции выступил Рэнди Пауэлл с рассказом о псевдонаучной «вихревой математике», а в 2014 году в конференции TEDMED участвовала Элизабет Холмс — основательница печально известного стартапа Theranos. В этом проекте вы исследуете историю TED-конференций с помощью Tableau.

Описание данных

Файлы tableau_project_data_1.csv, tableau_project_data_2.csv, tableau_project_data_3.csv хранят данные выступлений. У них одинаковая структура:

talk_id — идентификатор выступления;
url — ссылка на запись выступления;
title — название выступления;
description — краткое описание;
film_date — дата записи выступления;
duration — длительность в секундах;
views — количество просмотров;
main_tag — основная категория, к которой относится выступление;
speaker_id — уникальный идентификатор автора выступления;
laughter_count — количество раз, когда аудитория смеялась в ходе выступления;
applause_count — количество раз, когда аудитория аплодировала в ходе выступления;
language — язык, на котором велось выступление;
event_id — уникальный идентификатор конференции.
Файл tableau_project_event_dict.csv — справочник конференций. Описание таблицы:

conf_id — уникальный идентификатор конференции;
event — название конференции;
country — страна проведения конференции.
Файл tableau_project_speakers_dict.csv — справочник авторов выступления. Описание таблицы:

author_id — уникальный идентификатор автора выступления;

speaker_name — имя автора;

speaker_occupation — профессиональная область автора;

speaker_description — описание профессиональной деятельности автора.

Набор данных проекта мог вам напомнить известный датасет TED Talks, размещённый в библиотеке Kaggle. Он не является его копией: мы собрали данные на основе материалов сайта TED с помощью специальной программы.

Цель исследования

Исследовать предоставленный набор данных о конференциях, спикерах и аудитории TED
Создать дашборды в Tableau по изученным особенностям предоставленных материалов
Подготовить презентацию с составленными дашбордами на слайдах
Ход исследования

Шаг 1. Загрузите и изучите данные

Загрузите данные в Tableau.
С помощью Union объедините файлы tableau_project_data в единую таблицу. Объедините таблицу с данными выступлений, справочники конференций и авторов с помощью Relationship.
Изучите состав и типы данных.
С помощью визуализации изучите, как количество конференций распределено по времени. Определите год, после которого количество выступлений скачкообразно выросло.
Настройте фильтр, который исключит все выступления до найденного порогового года на уровне источника данных.
Шаг 2. Постройте дашборд «История выступлений»

Создайте лист «Выступления по странам» с визуализацией типа map, которая покажет процент выступлений в каждой из стран.

Создайте лист «Выступления по годам» с визуализацией типа area charts, у которой по оси X отложены года проведения конференций, а по оси Y — абсолютное число выступлений. Используйте измерение Main Tag для разбивки выступлений по категориям. Для этого вам понадобится создать сет, в который войдёт топ-N основных тематик выступлений.

Создайте копию предыдущего листа и теперь по оси Y отобразите процент наблюдений по категориям за каждый год. Назовите новый лист «Процент выступлений по тематикам».

Задайте фильтр по полю Film Date и примените ко всем визуализациям на основе текущего набора данных.

Создайте дашборд «История выступлений».

Настройте Action на дашборде так, чтобы при выборе страны на листе «Выступления по странам» фильтр применялся и к остальным листам.

В области выводов и наблюдений напишите ответы на вопросы:

В каких странах чаще всего проходили выступления?
Какие категории выступлений наиболее популярны?
Как изменился состав категорий выступлений в 2020 и 2021 годах?
Шаг 3. Создание дашборда «Тематики выступлений»

Создайте лист «Выступления по тематике» с круговой диаграммой. На ней каждый сектор должен отражать тематику выступлений, а размер сектора — количество выступлений. Отобразите на графике топ-10 категорий по количеству выступлений, а менее популярные объедините в категорию «Другие». Используйте для этого сет.

Создайте лист «Тематики и страны» с визуализацией типа highlight table:

В строках таблицы — 10 самых популярных тематик и категория «Другие».
В столбцах — топ-3 страны по количеству выступлений. Выделите их с помощью сета.
На пересечении укажите процент выступлений на конкретную тему в каждой стране.
Отсортируйте полученную таблицу по убыванию числа просмотров по горизонтальной и вертикальной оси.
Создайте три вычисляемых поля:

Duration, min — длительность выступления в минутах;
Applause by Duration — отношение числа аплодисментов к длительности выступления в секундах;
Laughter by Duration — отношение числа ситуаций, когда аудитория смеялась, к длительности выступления в секундах.
Создайте лист «Аплодисменты по тематикам» с диаграммой размаха:

По горизонтальной оси должны быть отложены тематики, по вертикальной — переменная Applause by Duration.
Каждая точка на графике должна показывать отдельное наблюдение.
Во всплывающую подсказку добавьте название, автора и значение Applause by Duration — они понадобятся для ответа на вопросы.
Отсортируйте категории на графике по убыванию медианного значения Applause by Duration. При необходимости ограничьте значения по вертикальной оси с помощью меню редактирования осей.
Создайте копию предыдущего листа. Назовите новый лист «Смех по тематикам». На этой визуализации замените Applause by Duration на Laughter by Duration. Не забудьте про всплывающую подсказку и сортировку.

Создайте два новых листа с гистограммами длительности выступлений и числа просмотров. Назовите листы «Гистограмма длительности» и «Гистограмма просмотров». Не забудьте, что гистограммы должны показывать проценты наблюдений, а не абсолютные значения.

На листе «Выступления по тематике» настройте всплывающую подсказку так, чтобы она показывала гистограммы длительности и просмотров.

Создайте новый лист «Связь длительности с просмотрами» с визуализацией типа scatter plot:

На графике по оси X отложите длительность выступления в минутах, по оси Y число просмотров. Каждая точка на графике должна соответствовать одному выступлению.
Настройте всплывающую подсказку так, чтобы на ней отображались название и длительность выступления и число просмотров.
Создайте дашборд «Тематики выступлений».

Настройте Action так, чтобы при выборе тематики на листе «Выступления по тематике» фильтр применялся к остальным визуализациям на дашборде, кроме таблицы «Тематики и страны».

В области выводов и наблюдений напишите ответы на вопросы:

Какие категории выступлений наиболее популярны?
Различается ли распределение популярных категорий в разных странах? Например, какие категории более популярны в Канаде, чем в США?
Какие категории чаще вызывают аплодисменты аудитории, а какие реже? Какому выступлению аплодировали больше остальных?
Какие категории чаще вызывают смех аудитории, а какие реже? Какое выступление оказалось самым смешным?
Есть ли зависимость между длительностью выступления и количеством просмотров? Какое выступление посмотрели чаще всего?
Какое выступление длилось дольше всех?
Шаг 4. Создание дашборда «Авторы выступлений»

Создайте сет, который объединит наиболее популярные области деятельности авторов (Speaker Occupation). Настройте сет так, чтобы числом областей деятельности можно было управлять с помощью целочисленного параметра Top-N Speaker Occupations. Для параметра установите элемент управления типа Slider.
Создайте лист «Области деятельности авторов» с пузырьковой диаграммой (packed bubbles). Каждый кружок должен соответствовать одной из топ-N областей деятельности. Настройте визуализацию так, что она не показывала категорию «Другие».
Создайте вычисляемое поле Talks by Author, которое покажет максимальное количество выступлений у автора. При создании поля используйте LOD для фиксации измерения Author Id.
Создайте лист «Распределение числа выступлений» со столбчатой диаграммой. По оси X должно быть отложено максимальное число выступлений (Talks by Author), а по оси Y — число авторов, которые провели столько выступлений.
Создайте лист «Авторы по числу выступлений» с таблицей из столбцов:
имя автора,
область деятельности автора,
описание деятельности автора,
число выступлений.
Отсортируйте таблицу по убыванию числа выступлений.
Создайте лист «Выступления и число просмотров» с таблицей из столбцов:
название выступления;
описание выступления;
конференция, на которой проводилось выступление;
число просмотров.
Отсортируйте таблицу по убыванию числа просмотров.
Создайте дашборд «Авторы выступлений».
Настройте Actions на дашборде так, чтобы при выборе области деятельности на визуализации «Области деятельности авторов» фильтровались таблицы «Авторы по числу выступлений» и «Выступления и число просмотров». При выборе автора в таблице «Авторы по числу выступлений» должна фильтроваться таблица «Выступления и число просмотров».
Не забудьте добавить на дашборд элемент управления параметром Top-N Speaker Occupations.
В области выводов и наблюдений напишите ответы на вопросы:
Какие области деятельности у авторов преобладают?
Сколько выступлений обычно приходится на одного автора? Кто выступал чаще всего?
Какой дизайнер (Designer) выступал чаще остальных? Какое выступление этого автора смотрели меньше всего?
Шаг 5. Создание дашборда на свободную тему

Добавьте в презентацию дашборд на свободную тему с двумя или тремя визуализациями. Варианты вопросов, на которые можно ответить дашбордом:
Как изменился состав тематик категории «Другие» в 2019–2021 годах?
Можно ли разделить конференции на категории? Как менялась популярность этих категорий со временем?
Не забудьте добавить свои выводы и наблюдения на дашборд.
Шаг 6. Создание презентации

С помощью story создайте презентацию из четырёх слайдов:

дашборд «История выступлений»,
дашборд «Тематики выступлений»,
дашборд «Авторы выступлений»,
дашборд на свободную тему.
Опубликуйте презентацию на сайте Tableau Public. Не забудьте открыть к ней доступ.

Добавьте ссылку на ваш дашборд и презентацию комментарием в ячейки Jupyter-тетрадки и отправьте её на проверку ревьюеру.