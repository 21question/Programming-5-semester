# Лабораторная работа 2. Ряд Фибоначчи с помощью итераторов

Лабораторная работа состоит из двух подзаданий: 
1. Создание сопрограммы на основе кода, позволяющей по данному n сгенерировать список элементов из ряда Фибоначчи.
2. Создание программы, возвращающей список чисел Фибоначчи с помощью итератора.
 

## Задание 1
![alt text](https://github.com/21question/Programming-5-semester/blob/main/LR2/Pictures/notest.png)
![alt text](https://github.com/21question/Programming-5-semester/blob/main/LR2/Pictures/test.png)

## Задание 2

![alt text](https://github.com/21question/Programming-5-semester/blob/main/LR2/Pictures/testwithfibonachi.png)
Дополненый файл ```gen_fib.py```
``` python
import functools


def my_genn():

    result = None
    while True:
        n = yield result

        if n < 0:
            raise ValueError("n must be >= 0")

        a, b = 0, 1
        result = []
        for _ in range(n):
            result.append(a)
            a, b = b, a + b


def fib_coroutine(func):
    def wrapper(*args, **kwargs):
        gen = func(*args, **kwargs)
        next(gen)
        return gen

    return wrapper


my_genn = fib_coroutine(my_genn)


class FibonacchiLst:
    def __init__(self, instance):
        self.instance = instance
        self.idx = 0

    def __iter__(self):
        return self

    def __is_fib(self, n):
        if n < 0:
            return False


        def is_square(x):
            s = int(x ** 0.5)
            return s * s == x

        return is_square(5 * n * n + 4) or is_square(5 * n * n - 4)

    def __next__(self):
        while True:
            if self.idx >= len(self.instance):
                raise StopIteration

            value = self.instance[self.idx]
            self.idx += 1

            if self.__is_fib(value):
                return value
```
Дополненный файл ```test_fib.py```
```python

from gen_fib import my_genn
from gen_fib import FibonacchiLst

def test_fib_1():
    gen = my_genn()
    assert gen.send(3) == [0, 1, 1], "Тривиальный случай n = 3"


def test_fib_2():
    gen = my_genn()
    assert gen.send(5) == [0, 1, 1, 2, 3], "Пять первых членов ряда"


def test_fib_3():
    gen = my_genn()
    assert gen.send(8) == [0, 1, 1, 2, 3, 5, 8, 13], "Восемь элементов"


def test_fib_zero():
    gen = my_genn()
    assert gen.send(0) == [], "Ноль элементов — пустой список"


def test_fib_one():
    gen = my_genn()
    assert gen.send(1) == [0], "Один элемент"


def test_fib_negative():
    gen = my_genn()
    try:
        gen.send(-5)
        assert False, "Ожидалось исключение ValueError"
    except ValueError:
        pass


def test_multiple_calls():
    gen = my_genn()
    assert gen.send(3) == [0, 1, 1]
    assert gen.send(5) == [0, 1, 1, 2, 3]


if __name__ == "__main__":
    test_fib_1()
    test_fib_2()
    test_fib_3()
    test_fib_zero()
    test_fib_one()
    test_fib_negative()
    test_multiple_calls()
    print("Все тесты успешно пройдены ✔")

if __name__ == "__main__":
    lst = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1]
    fib_iter = FibonacchiLst(lst)
    result = list(fib_iter)
    print(f"Числа Фибоначчи из списка {lst}:\n{result}")


```
