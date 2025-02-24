#Обзор ключевых методов пандас в рамках серии создание переменных 
```python
import pandas as pd
```
#чтение файла
```python
bikes = pd.read_csv("C:\\Users\\gefte\\Downloads\\BikeData.csv")
```
# вывод башни через .head(n = 5)
```python
bikes.head()
```
#формирование новой колонки как суммы предыдущих
```python
bikes["Itog"] = bikes["Partner 1"] + bikes["Partner 2"]
bikes
```
#удаление через del
```python
del bikes["Partner 1"]
```
#либо через .drop(column,exis = 1), но будет создана копия датафрейма
```python
bikes.drop("Partner 2")
```
# .info(self) получение тех. инфы с колонок
```python
bikes.info()
```
#Преобразование в тип Дейттайм .to_datetime()
```python
pd.to_datetime(bikes["Date"], dayfirst = True).dt.year
```
# Вывод всех воскресение с помощью аксессора datatime .dt (результат имеет многократно повторязуиеся даты так как в данных инфа почасовая)
```python
bikes[bikes["Date"].dt.day_name() == "Sunday"]
```
# назначение условно булевой переменной
```python
bikes["Functioning Day"] == bikes["Functioning Day"] == "YES"
```
# .apply это map наоборот с примерно следующим синтаксисом itarable.apply(func()) ; используется для преобразования например столбца через функцию
```python
bikes["Holiday"].apply(lambda x: 2 if x == "Holiday" else 0)
```
# формирование нового столбца, где если число из столбца humidity  в дапазоне то оно normal и 1, если нет  то 0,
##аналогично можно и назначить в новый столбец новые название для температуры в зависимости от числа
```python
bikes["Normal Humidity"] = bikes["Humidity"].apply(lambda x: 1 if x in range(40,61) else 0)
```
# pd.Categorical(), присвает Int по собственному классификатору для задча широкго спектра, например ML
```python
import pandas as pd

# Обычный список значений
colors = ["Red", "Blue", "Green", "Red", "Blue", "Green"]

# Преобразуем в категориальный тип
cat_colors = pd.Categorical(colors)

print(cat_colors)
print(cat_colors.categories)  # Список уникальных категорий
print(cat_colors.codes)  # Числовые коды категорий

#OUTPUT:
['Red', 'Blue', 'Green', 'Red', 'Blue', 'Green']
Categories (3, object): ['Blue', 'Green', 'Red']
[2 0 1 2 0 1]
```
# np.where(условие, значение_если_True, значение_если_False), используется в пандас для замены столбцов также
```python
import pandas as pd
import numpy as np

# Создаем DataFrame
df = pd.DataFrame({
    "Name": ["Alice", "Bob", "Charlie", "David"],
    "Age": [23, 35, 18, 45]
})

# Добавляем столбец "Category": если Age >= 30 → "Взрослый", иначе "Молодой"
df["Category"] = np.where(df["Age"] >= 30, "Взрослый", "Молодой")

# Добавляем столбец "Group" с несколькими условиями
df["Group"] = np.where(
    df["Age"] < 20, "Подросток",
    np.where(df["Age"] < 40, "Молодой взрослый", "Пожилой")
)

print(df)
```
# to_csv(path, index = bool)
```python
bikes.to_scv('//Downloads//BikesDataVars.csv', index = False)
```
# to_pickle(path.pkl, index = bool) огурец замораживает фалй при сохранении и оставляет изменные типы данных

# Метод column.value_counts(subset = None, ascending=False, dropna = False(для подсчета NaN)) используется для подсчета количества уникальных значений в столбце pandas.Series
```python
# Создаем DataFrame
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Green", "Red", "Blue", "Red"]
})

# Подсчитываем количество каждого цвета
print(df["Color"].value_counts())
🔹 Выход:
Red      3
Blue     2
Green    1
Name: Color, dtype: int64
```
