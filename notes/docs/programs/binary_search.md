# Binary Search

```python

#!/usr/bin/env python3

import time


def time_it(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(func.__name__ + " took " + str((end-start) * 1000) + " mil sec")
        return result
    return wrapper


@time_it
def linear_search(numbers_list, number_to_find):
    for index, number in enumerate(numbers_list):
        if number_to_find == number:
            return index
    return -1


@time_it
def binary_search(numbers_list, number_to_find):
    left_index = 0
    right_index = len(numbers_list) - 1

    while left_index <= right_index:
        mid_index = (left_index + right_index) // 2
        mid_number = numbers_list[mid_index]
        if mid_number == number_to_find:
            return mid_index

        if mid_number < number_to_find:
            left_index = mid_index + 1
        else:
            right_index = mid_index - 1
    return -1


@time_it
def binary_search_recursive(numbers_list, number_to_find, left_index, right_index):
    if right_index < left_index:
        return -1
    mid_index = (left_index + right_index) // 2
    if mid_index >= len(numbers_list) or mid_index < 0:
        return -1

    mid_number = numbers_list[mid_index]
    if mid_number == number_to_find:
        return mid_index

    if mid_number < number_to_find:
        left_index = mid_index + 1
    else:
        right_index = mid_index - 1

    return binary_search_recursive(numbers_list, number_to_find, left_index, right_index)


def find_occurrences(numbers_list, number_to_find):
    index = binary_search(numbers_list, number_to_find)
    indices = [index]
    i = index - 1
    while i >= 0:
        if numbers_list[i] == number_to_find:
            indices.append(i)
        else:
            break
        i -= 1

    i = index + 1
    while i <= len(numbers_list):
        if numbers_list[i] == number_to_find:
            indices.append(i)
        else:
            break
        i += 1
    return sorted(indices)


if __name__ == "__main__":
    numbers_list = [12, 15, 17, 19, 21, 24, 45, 67]
    number_to_find = 24

    # numbers_list = [i for i in range(1000001)]
    # number_to_find = 1000000

    index = linear_search(numbers_list, number_to_find)
    print(f"Number found at index {index} using linear search")

    index = binary_search(numbers_list, number_to_find)
    print(f"Number found at index {index} using binary search")

    index = binary_search_recursive(numbers_list, number_to_find, 0, len(numbers_list))
    print(f"Number found at index {index} using binary search")

    numbers = [1, 4, 6, 9, 11, 15, 15, 15, 17, 21, 34, 34, 56]
    number_to_find = 15
    occurrences = find_occurrences(numbers, number_to_find)
    print(f"Number found at indices {occurrences} using binary search")


```