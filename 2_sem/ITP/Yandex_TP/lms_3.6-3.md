# 3.6. КР «Коллекции и работа с памятью»
## 1. Шинковка строк
```python
n = int(input())
for i in range(n):
    parts = input().split('^')
    s = parts[0]
    a = int(parts[1])
    b = int(parts[2])
    step = len(s) % 4
    print(s[a:b:step])
```
## 2. Словарная опись
```python
n = input()
answ = {}
while n != "":
    for word in n.split():
        if len(word) % 2 == 0:
            letter = word[len(word) // 2 - 1]
        else:
            letter = word[len(word) // 2]

        letter = letter.lower()
        if letter not in answ.keys():
            answ[letter] = [word.upper()]
        elif word.upper() not in answ[letter]:
            answ[letter] += [word.upper()]
    n = input()
for key in answ.keys():
    answ[key].sort()
    print(key, '"', end="")
    print(*answ[key], sep=". ", end='"\n')
```
## 3. Перераспределение по размеру
```python
[x for x in nums if x > (min(nums) + max(nums)) / 2] + [x for x in nums if x <= (min(nums) + max(nums)) / 2]

'''
nums= list(map(int, input().split()))
avg = min(nums) + max(nums)
first_part = [x for x in nums if 2 * x > avg]
second_part = [x for x in nums if 2 * x <= avg]
print(first_part + second_part)
'''

```
## 4. Словарный комбинатор
```python
from itertools import permutations


# Считываем входные данные
letters_str = input().strip()
length = int(input().strip())

# Обрабатываем первую строку: уникальные буквы, отсортированные
unique_letters = list({char for char in letters_str.split('; ')})
unique_letters.sort()

# Генерируем все перестановки заданной длины
perms = permutations(unique_letters, length)

# Преобразуем кортежи в строки и сортируем результат
result = [''.join(p) for p in perms]
result.sort()

# Выводим каждое слово
for word in result:
    print(word)
```
## 5. Алфавитная статистика
```python
import json
from collections import defaultdict


word_dict = defaultdict(set)  # Используем set для уникальных значений

while True:
    try:
        word = input().strip()
        lower_word = word.lower()
        for i in range(1, len(word), 2):  # Четные позиции (индексы 1,3,5...)
            char = lower_word[i]
            word_dict[char].add(lower_word)  # add() работает для set
    except EOFError:
        break

# Преобразуем множества в отсортированные списки
for key in word_dict:
    word_dict[key] = sorted(word_dict[key])  # Сортировка лексикографически

# Запись в файл
with open("result.json", "w", encoding="utf-8") as f:
    json.dump(word_dict, f, ensure_ascii=False, indent=4)
```
