# Recursion

```python

#!/usr/bin/env python3

def find_sum(n):
    sum = 0
    for i in range(1, n+1):
        sum += i
    return sum


def find_sum_recursion(n):
    if n == 1:
        return 1
    return n + find_sum(n - 1)


# 0,1,1,2,3,5,8
# -------------
# 0,1,2,3,4,5,6
def fib(n):
    if n == 0 or n == 1:
        return n
    return fib(n-1) + fib(n-2)


def sum_list_of_numbers(numbers_list):
    if len(numbers_list) == 1:
        return numbers_list[0]
    return numbers_list[0] + sum_list_of_numbers(numbers_list[1:])


def recursive_list_sum(data_list):
    total = 0
    for element in data_list:
        if isinstance(element, list):
            total = total + recursive_list_sum(element)
        else:
            total = total + element
    return total


def sum_series(number):
    if number == 2:
        return 2
    return number + sum_series(number - 2)


def find_exp(number, power):
    if power == 1:
        return number
    return number * find_exp(number, power - 1)


if __name__ == "__main__":
    print(fib(10))
    print(recursive_list_sum([1, 2, [3, 4], [5, 6]]))
    print(sum_series(10))
    print(find_exp(3, 4))

```