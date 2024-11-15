# Тема 11. Итераторы и генераторы
Отчет по Теме #11 выполнил(а):
- Каткова Ксения Александровна
- ПИЭ-22-1

| Задание | Лаб_раб | Сам_раб |
| ------ | ------ | ------ |
| Задание 1 | + | + |
| Задание 2 | + | + |
| Задание 3 | + | - |
| Задание 4 | + | - |
| Задание 5 | + | - |

знак "+" - задание выполнено; знак "-" - задание не выполнено;

Работу проверили:
- к.э.н., доцент Панов М.А.

## Лабораторная работа №1
Простой итератор, но у него нет гибкой настройки, например его нельзя развернуть. Он работает просто как next(), но нет prev()

```python
numbers = [0, 1, 2, 3, 4, 5]
for item in numbers:
    print(item)
```
### Результат.
![image](https://github.com/user-attachments/assets/b7d51915-f5a7-482e-9626-3f265d6600af)

## Выводы
Создается список numbers и проходится по каждому элементу, печатая его на экране. 

## Лабораторная работа №2
Класс итератор с гибкой настройкой и удобными применением

```python
class CountDown:
    def __init__(self, start):
        self.count = start + 1
    def __iter__(self):
        return self
    def __next__(self):
        self.count -= 1
        if self.count < 0:
            raise StopIteration
        return self.count
if __name__ == '__main__':
    counter = CountDown(5)
    for i in counter:
        print(i)
```
### Результат.
![image](https://github.com/user-attachments/assets/53c328be-f9de-4a6e-9f26-f8c54f1fe34f)

## Выводы
- Реализуется класс-итератор, который отсчитывает от заданного числа вниз до нуля.
- Используются методы __iter__() и __next__() для поддержки интерфейса итератора.

## Лабораторная работа №3
Генератор списка

```python
a = [i ** 2 for i in range(1, 5)]
print('a - ', a)
for i in a:
    print(i)
print('iter(a) - ', iter(a))
for i in a:
    print(i)
```
### Результат.
![image](https://github.com/user-attachments/assets/9f56b696-1349-4dbb-90c7-4727e6509708)

## Выводы
- Здесь создается список квадратов чисел от 1 до 4. 
- Итерация по списку происходит без проблем, при этом один вызов iter(a) возвращает итератор списка.

## Лабораторная работа №4
Выражения генераторы

```python
b = (i ** 2 for i in range(1, 5))
print(b)
print('first')
for i in b:
    print(i)
print('second')
for i in b:
    print(i)
```
### Результат.
![image](https://github.com/user-attachments/assets/2b991203-ac2a-46c9-96a3-fb3e212abe13)

## Выводы
- В этом коде создается генераторное выражение для квадратов чисел.
- Вторая итерация ничего не выводит, поскольку все значения уже были сгенерированы.

## Лабораторная работа №5
Такой же счетчик, как и в первом задании, только это генератор и использует yield

```python
def countdown(count):
    while count >= 0:
        yield count
        count -= 1
if __name__ == '__main__':
    counter = countdown(5)
    for i in counter:
        print(i)
```
### Результат.
![image](https://github.com/user-attachments/assets/c158a1db-34f9-415c-b359-d2b487e6a56f)

## Выводы
- Здесь создается функция-генератор, которая отчитывает вниз от заданного числа до нуля.
- Использование yield позволяет "заморозить" состояние функции и продолжить выполнение при следующем вызове.
- Каждая последующая попытка итерироваться через генератор даст пустой результат после первой итерации.

## Самостоятельная работа №1
Вас никак не могут оставить числа Фибоначчи, очень уж они вас заинтересовали. Изучив новые возможности Python вы решили реализовать программу, которая считает числа Фибоначчи при помощи итераторов. Расчет начинается с чисел 1 и 1. Создайте функцию fib(n), генерирующую n чисел Фибоначчи с минимальными затратами ресурсов. Для реализации этой функции потребуется обратиться к инструкции yield (Она не сохраняет в оперативной памяти огромную последовательность, а дает возможность “доставать” промежуточные результаты по одному). Результатом решения задачи будет листинг кода и вывод в консоль с числом Фибоначчи от 200.

```python
def fib(n):
    a, b = 1, 1
    for _ in range(n):
        yield a
        a, b = b, a + b
fibonacci_numbers = list(fib(200))
print(fibonacci_numbers[199])
```
### Результат.
![image](https://github.com/user-attachments/assets/f01ec2e2-c2ed-4015-8678-045d5db48346)

## Выводы
Инициализируются два числа a и b, которые представляют текущее и следующее значения последовательности. Используется цикл for для генерации чисел, в каждой итерации отдается текущее число a, а затем обновляются значения.
Результат помещается в список fibonacci_numbers, после чего выводится 199-е число.

## Самостоятельная работа №2
К коду предыдущей задачи добавьте запоминание каждого числа Фибоначчи в файл “fib.txt”, при этом каждое число должно находиться на отдельной строчке. Результатом выполнения задачи будет листинг кода и скриншот получившегося файла

```python
def fib_and_save(n, filename):
    a, b = 1, 1
    with open(filename, 'w') as file:
        for _ in range(n):
            file.write(f"{a}\n")
            yield a
            a, b = b, a + b
filename = "fib.txt"
fibonacci_numbers = list(fib_and_save(200, filename))
print(fibonacci_numbers[199])
```
### Результат.
![image](https://github.com/user-attachments/assets/65d3683c-d1c4-4a91-8e55-65f33928e06f)

![image](https://github.com/user-attachments/assets/73f07e67-12c7-4d21-bfa7-f96b6f57f437)

## Выводы
Имеет ту же логику, что и первый код, но с дополнением, что каждое число записывается в файл построчно. Назначено имя файла, в который записываются все числа Фибоначчи, и результат помещается в список fibonacci_numbers. Код генерирует 200 чисел Фибоначчи, записывает их в файл и выводит 199-е число.

## Общие выводы по теме
Общие выводы по теме Итераторы и Генераторы
1. Итераторы:
   - Итераторы позволяют последовательный доступ к элементам коллекции без необходимости знать о внутренней структуре этих данных.
   - Класс, реализующий итератор, должен содержать методы __iter__() и __next__().
   - Итераторы могут быть использованы для перебора различных коллекций: списков, кортежей, множеств и словарей.
2. Генераторы:
   - Генераторы — это особые функции, которые позволяют создавать итераторы с использованием ключевого слова yield.
   - Генераторы более просты в реализации и требуют меньше кода, чем классические итераторы, так как не требуют реализации методов __iter__() и __next__().
   - Генераторы автоматически сохраняют состояние между вызовами, что позволяет экономить память, поскольку элементы создаются по мере необходимости и не хранятся в памяти целиком.
3. Преимущества генераторов:
   - Экономия памяти: генераторы создают элементы на лету и могут работать с большими последовательностями данных без необходимости загрузки их в память.
   - Упрощение кода: использование yield делает код более понятным и легким для чтения.
   - Легкость в использовании: генераторы легко интегрируются с другими итерационными инструментами и конструкциями Python, такими как циклы for.
4. Отличия итераторов от генераторов:
   - Итератор - это объект, который управляет состоянием итерации, тогда как генератор - это упрощенный способ создания итераторов в виде функции.
   - Генераторы автоматически реализуют интерфейс итератора, освобождая программиста от лишних деталей.
