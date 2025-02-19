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
#либо через .drop(column), но будет создана копия датафрейма
```python
bikes.drop("Partner 2")
```
