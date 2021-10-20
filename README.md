# Использование библиотеки ___pandas___ для работы с государственными каталогами из портала открытых данных Министерства культуры Российской Федерации  
## в рамках проекта "Использование библиотек Python для задач в области культурологии"  

![](https://github.com/VladislavaRo/pesni_project/blob/3ef0d1eabade8d1c221f4e8ac3ed1629d7181fc5/cvsplot.jpg)

#### Выполнили:  
#### **Владислава Родионова**  
#### **Тимофей Кошкин**  
#### ВШЭ, Москва, 2021 г.  


## библиотека  
___pandas___ - это библиотека с открытым исходным кодом, предоставляющая высокопроизводительные, простые в использовании структуры данных и инструменты анализа данных для языка программирования Python  

:black_square_button: Какие типы данных обрабатывает библиотека pandas?  
___pandas___ является подходящим инструментом для работы с табличными данными, такими как данные, хранящиеся в электронных таблицах или базах данных.  ___pandas___ позволяет исследовать, очищать и обрабатывать такие данные. Таблица с данными в  ___pandas___ называется ___DataFrame___.  

![](https://pandas.pydata.org/docs/_images/01_table_dataframe.svg)  

:black_square_button: Как читать и записывать табличные данные?  
___pandas___ поддерживает интеграцию со многими форматами файлов или источниками данных (csv, excel, sql, json, parquet). Импорт данных из каждого из этих источников обеспечивается функцией с префиксом read_*.  

:black_square_button: Как выбрать составляющие таблицу подмножества?  
Выбор или фильтрация определенных строк и/или столбцов? Фильтрация данных по условию? D ___pandas___ доступны методы нарезки, выбора и извлечения необходимых вам данных доступны.  
![](https://pandas.pydata.org/docs/_images/03_subset_columns_rows.svg)  

:black_square_button: Как создавать визуализации в ___pandas___?   
___pandas___ также обеспечивает вывод данных после их обработки, используя возможности ___Matplotlib___. Пользователь может выбрать тип графика (точечный, линейный, прямоугольный,...), соответствующий его данным.  

![](https://pandas.pydata.org/docs/_images/04_plot_overview.svg)  

:black_square_button: Как рассчитать сводную статистику?  
Основные статистические данные (среднее значение, медиана, минимум, максимум, количество...) легко вычисляются. Эти или пользовательские агрегации могут быть применены ко всему набору данных, к скользящему окну данных или сгруппированы по категориям. Последний также известен как подход "разделение-применение-объединение".  

![](https://pandas.pydata.org/docs/_images/06_groupby.svg)  

:black_square_button: Как объединить данные из нескольких таблиц?  
Несколько таблиц могут быть объединены как по столбцам, так и по строкам, поскольку для объединения нескольких таблиц данных предусмотрены операции соединения / слияния, подобные базам данных.  

![](https://pandas.pydata.org/docs/_images/08_concat_row.svg)  

:black_square_button: Как обрабатывать данные временных отрезков?  
___pandas___ отлично поддерживает временные отрезки, обладает обширным набором инструментов для работы с датами, временем и индексированными по времени данными.  

:black_square_button: Как работать с текстовыми данными?  
Наборы данных содержат не только числовые данные. ___pandas___ предоставляет широкий спектр функций для очистки текстовых данных и извлечения из них полезной информации.  

Официальный сайт ___pandas___ [по этой ссылке](https://pandas.pydata.org/)  
Напрямую к документации о ___pandas___ [по этой ссылке](https://pandas.pydata.org/docs/)  

## пример работы  
Библиотека импортируется обычно следующим образом:  
```
import numpy as np
import pandas as pd
```
Далее можно создать Series путем передачи списка значений, позволяя ___pandas___ записать int индекс по умолчанию:
```
s = pd.Series([1, 3, 5, np.nan, 6, 8])
s
```
```
0    1.0
1    3.0
2    5.0
3    NaN
4    6.0
5    8.0
dtype: float64
```
Далее создается DataFrame, с индексом даты и времени и озаглавленными столбцами, путем передачи массива NumPy:  
```
dates = pd.date_range("20130101", periods=6)
dates
```
```
DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
               '2013-01-05', '2013-01-06'],
              dtype='datetime64[ns]', freq='D')
```
```
df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list("ABCD"))
df
```
```
                   A         B         C         D
2013-01-01  0.469112 -0.282863 -1.509059 -1.135632
2013-01-02  1.212112 -0.173215  0.119209 -1.044236
2013-01-03 -0.861849 -2.104569 -0.494929  1.071804
2013-01-04  0.721555 -0.706771 -1.039575  0.271860
2013-01-05 -0.424972  0.567020  0.276232 -1.087401
2013-01-06 -0.673690  0.113648 -1.478427  0.524988
```
___pandas___ позволяет просматривать верхние и нижние ряды DataFrame с помощью *head* и *tail*:  
```
df.head()
```
```
                   A         B         C         D
2013-01-01  0.469112 -0.282863 -1.509059 -1.135632
2013-01-02  1.212112 -0.173215  0.119209 -1.044236
2013-01-03 -0.861849 -2.104569 -0.494929  1.071804
2013-01-04  0.721555 -0.706771 -1.039575  0.271860
2013-01-05 -0.424972  0.567020  0.276232 -1.087401
```
```
df.tail(3)
```
```
                   A         B         C         D
2013-01-04  0.721555 -0.706771 -1.039575  0.271860
2013-01-05 -0.424972  0.567020  0.276232 -1.087401
2013-01-06 -0.673690  0.113648 -1.478427  0.524988
```
Также может отобразить название колонн, индексы с помощью *index* и *colums*:
```
df.index
```
```
DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
               '2013-01-05', '2013-01-06'],
              dtype='datetime64[ns]', freq='D')
```
```
df.columns
```
```
Index(['A', 'B', 'C', 'D'], dtype='object')
```
с помощью *describe* можно узнать краткую статистическую сводку используемых данных:
```
df.describe()
```
```
              A         B         C         D
count  6.000000  6.000000  6.000000  6.000000
mean   0.073711 -0.431125 -0.687758 -0.233103
std    0.843157  0.922818  0.779887  0.973118
min   -0.861849 -2.104569 -1.509059 -1.135632
25%   -0.611510 -0.600794 -1.368714 -1.076610
50%    0.022070 -0.228039 -0.767252 -0.386188
75%    0.658444  0.041933 -0.034326  0.461706
max    1.212112  0.567020  0.276232  1.071804
```
Можно отсортировать данные по столбцу с индексами или по значениям определенного столбца:  
```
df.sort_index(axis=1, ascending=False)
```
```
                   D         C         B         A
2013-01-01 -1.135632 -1.509059 -0.282863  0.469112
2013-01-02 -1.044236  0.119209 -0.173215  1.212112
2013-01-03  1.071804 -0.494929 -2.104569 -0.861849
2013-01-04  0.271860 -1.039575 -0.706771  0.721555
2013-01-05 -1.087401  0.276232  0.567020 -0.424972
2013-01-06  0.524988 -1.478427  0.113648 -0.673690
```
```
df.sort_values(by="B")
```
```
                   A         B         C         D
2013-01-03 -0.861849 -2.104569 -0.494929  1.071804
2013-01-04  0.721555 -0.706771 -1.039575  0.271860
2013-01-01  0.469112 -0.282863 -1.509059 -1.135632
2013-01-02  1.212112 -0.173215  0.119209 -1.044236
2013-01-06 -0.673690  0.113648 -1.478427  0.524988
2013-01-05 -0.424972  0.567020  0.276232 -1.087401
```
Для работы с данными можно выбирать определенный столбец или нужные строки:  
```
df["A"]
```
```
2013-01-01    0.469112
2013-01-02    1.212112
2013-01-03   -0.861849
2013-01-04    0.721555
2013-01-05   -0.424972
2013-01-06   -0.673690
Freq: D, Name: A, dtype: float64
```
```
df[0:3]
```
```
                   A         B         C         D
2013-01-01  0.469112 -0.282863 -1.509059 -1.135632
2013-01-02  1.212112 -0.173215  0.119209 -1.044236
2013-01-03 -0.861849 -2.104569 -0.494929  1.071804
```
```
df["20130102":"20130104"]
```
```
                   A         B         C         D
2013-01-02  1.212112 -0.173215  0.119209 -1.044236
2013-01-03 -0.861849 -2.104569 -0.494929  1.071804
2013-01-04  0.721555 -0.706771 -1.039575  0.271860
```
Для получения поперечного сечения из используемых данных можно воспользоваться *label*:
```
df.loc[dates[0]]
```
```
A    0.469112
B   -0.282863
C   -1.509059
D   -1.135632
Name: 2013-01-01 00:00:00, dtype: float64
```
```
df.loc[:, ["A", "B"]]
```
```
                   A         B
2013-01-01  0.469112 -0.282863
2013-01-02  1.212112 -0.173215
2013-01-03 -0.861849 -2.104569
2013-01-04  0.721555 -0.706771
2013-01-05 -0.424972  0.567020
2013-01-06 -0.673690  0.113648
```
```
df.loc["20130102":"20130104", ["A", "B"]]
```
```
                   A         B
2013-01-02  1.212112 -0.173215
2013-01-03 -0.861849 -2.104569
2013-01-04  0.721555 -0.706771
```
Данные также можно выбирать по их позиции с помощью *iloc*:
```
df.iloc[3:5, 0:2]
```
```
                   A         B
2013-01-04  0.721555 -0.706771
2013-01-05 -0.424972  0.567020
```
```
df.iloc[[1, 2, 4], [0, 2]]
```
```
                   A         C
2013-01-02  1.212112  0.119209
2013-01-03 -0.861849 -0.494929
2013-01-05 -0.424972  0.276232
```
Наконец, данные можно выбирать с помощью логического индексирования:
```
df[df["A"] > 0]
```
```
                   A         B         C         D
2013-01-01  0.469112 -0.282863 -1.509059 -1.135632
2013-01-02  1.212112 -0.173215  0.119209 -1.044236
2013-01-04  0.721555 -0.706771 -1.039575  0.271860
```
```
df[df > 0]
```
```
                   A         B         C         D
2013-01-01  0.469112       NaN       NaN       NaN
2013-01-02  1.212112       NaN  0.119209       NaN
2013-01-03       NaN       NaN       NaN  1.071804
2013-01-04  0.721555       NaN       NaN  0.271860
2013-01-05       NaN  0.567020  0.276232       NaN
2013-01-06       NaN  0.113648       NaN  0.524988
```
Выше привиденные примеры выполнялись на основе DataFrame введенного вручную и составленного ___pandas___ автоматически. Конечно же, ___pandas___ можно и нужно использовать с загруженными табличными файлами:  
```
import pandas as pd
df = pd.read_csv('table.csv', delimiter = ',', encoding = 'utf-8')




```

## применение библиотеки для нашей задачи в области культурологии 
### с чем работали?
В рамках данной проектной работы мы решили применить библиотеку ___pandas___ для работы с государственным _"Каталогом патриотической музыки"_, находящемуся по [этой ссылке](https://opendata.mkrf.ru/opendata/7705851331-patriot_music).   
Каталог выложен среди прочих других реестров и данных, содержание которых связано со сферой культуры и культурной политики, на [портале открытых данных Министерства культуры Российской Федерации](https://opendata.mkrf.ru/).  
Этот портал является частью инициативы открытого правительства, результаты работы которого представлены на сайте [Открытые данные России](https://data.gov.ru/).  
### цель работы?
Нам жгуче хотелось погрузиться в изучение патриотической музыки и составить из нее топ-чарт для прослушивания дома и на вечеринках! Шутка.  
Мы хотели узнать, какие исторические периоды отличаются большим количеством написанных патриотических песен, исходя из их каталогизированного корпуса.  
### наше предположение?  
наше предположение было такое-то.  
### этапы работы:  
-мы определи года и ключевые слова  
-нанан  
-хаха  
### результаты и выводы  
-в результате выяснилось такое-то  
-визуализировали данные для наглядности  
-получается, что...  
-в такие-то года то-то и то-то  
-анализ результатов и выводы (что полезного дает результат?)  

## описание проекта на Github (с кодом)  
### I этап
Импортируем Пандас  
```
import pandas as pd
```
Загружаем файл в таблицу df (DataFrame)  
```
df = pd.read_csv('data-1-structure-1.csv')
```
Удаляем лишние столбцы. Когда будем удалять строки с пустыми значениями, мы не потеряем те, где есть всё кроме, например, автора, который и так не нужен  
```
df.drop(["Название", "Композитор", "Автор текста", "ID музыкального жанра", "Тема", "Музыкальный жанр"], axis = 1, inplace = True)
```
Удаляем строки с пустыми значениями  
```
df.dropna(inplace = True)
```
Удаляем строки, где в годах есть тире, нам не нужны временные отрезки  
```
df = df[df["Год создания"].str.contains("-") == False]
```
Удаляем строки, где в годах фактически пусто, но технически пробел  
```
df = df[df["Год создания"].str.contains(" ") == False]
```
Сортируем по годам  
```
df = df.sort_values(by = ["Год создания"], ascending = True)  
```
Актуализируем индексы  
```
df = df.reset_index(drop = True)  
```
Экспортируем df как csv  
Экспортируем df как xlsx  
```
df.to_csv("S-years-words.csv")
df.to_excel("S-years-words.xlsx")
```
Печатаем df  
```
df
```
### II этап  
Создаем пустой словарь  
```
a = {}
```
Перебираем года из df  
Если год встречается первый раз, добавляем его в словарь и выставляем счетчик на единицу  
Если год уже есть в словаре, увеличиваем его счетчик на единицу  
```
for i in df["Год создания"]:
  if i not in a:
    a[i] = 1
  else:
    a[i] += 1
```
Создаем из словаря таблицу years  
```
years = pd.DataFrame(list(a.items()), columns=['Год создания', 'Количество музыкальных произведений'])
```
Сортируем по годам  
```
years = years.sort_values(by = ["Год создания"], ascending = True)
```
Актуализируем индексы  
```
years = years.reset_index(drop = True)
```
Экспортируем years как csv  
Экспортируем years как xlsx  
```
years.to_csv("S-years.csv")
years.to_excel("S-years.xlsx")
```
Печатаем years  
```
years
```
### III этап  
Импортируем счетчик  
```
from collections import Counter
```
Создаем пустой словарь  
```
v = {}
```
Перебираем все года  
 Создаем таблицу для каждого отдельного года  
 Каждому году в словаре создаем значение "NaN"  
```
for i in df["Год создания"]:
  dfi = df[df["Год создания"].str.contains(i)]
  v[i] = "NaN"
```
 Обращаемся к каждому ключевому слову в таблице для каждого отдельного года  
  Если год встречается впервые, создаем пустой список bb и добавляем к нему первое слово в этом году
   Меняем значение года с "NaN" на список слов bb, который создали выше  
```
  for k in dfi["Ключевые слова"]:
    if v[i] == "NaN":
      bb = []
      bb.append(k)
      v[i] = bb
```
  Если у года уже есть связанный с ним список слов bb (хоть даже из одного слова), добавляем новое слово в этот список  
```
    else:
      bb.append(k)
      v[i] = bb
```
Перебираем каждый элемент сформированного словаря  
```
for i in v:
```
 Называем списки слов для каждого года переменной x  
 Если для года нет такого списка, оставляем все как было  
 В остальных случаях находим слово в списке, которое встречается чаще всего, и связываем его с годом, заменяя им список слов  
```
  x = v[i] 
  if x == "NaN":
    x = "NaN"
  else:
    xm = [word for word, word_count in Counter(x).most_common(1)]
    v[i] = xm
```

Создаем из словаря таблицу words  
Сортируем по годам  
Актуализируем индексы  
```
words = pd.DataFrame(list(v.items()), columns=['Год создания', 'Самый популярный тэг'])
words = words.sort_values(by = ["Год создания"], ascending = True)
words = words.reset_index(drop = True)
```
Экспортируем words как csv  
Экспортируем words как xlsx  
```
words.to_csv("S-words.csv")
words.to_excel("S-words.xlsx")
```
Печатаем words  
```
words
```
### IV этап  
Объединяем таблицы years и words в таблицу wy  
```
wy = years.merge(words)
```
Экспортируем wy как csv  
Экспортируем wy как xlsx  
```
wy.to_csv("S-wy.csv")
wy.to_excel("S-wy.xlsx")
```
Печатаем wy  
```
wy
```
### Далее
Получившиеся данные можно визуализировать как и в самом ноутбуке, например, с помощью *plot*, так и при помощи вспомогательных сайтов для визуализации.
В ноутбуке задаем параметры осям x и y
```
df.plot(x='Год создания',y='Количество музыкальных произведений',style='k--')
```
или  
```
df.plot(y='Количество музыкальных произведений', kind='bar')
```
Получаются такие графики:  
![](https://github.com/VladislavaRo/pesni_project/blob/51f17e2c79d9ede81593603cffed340ad8697c2d/matplotlib2.png)
![](https://github.com/VladislavaRo/pesni_project/blob/51f17e2c79d9ede81593603cffed340ad8697c2d/matplotlib1.png)
С помощью сайта 

--визуализация на сайтах с графиками для скачивания (запись экрана)  
--визуалищзация сама классная онлайн (запись экрана)  
