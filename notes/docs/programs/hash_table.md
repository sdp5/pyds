# Hash Table

```python

#!/usr/bin/env python3


class HashTable:

    def __init__(self):
        self.MAX = 10
        self.arr = [None for _ in range(self.MAX)]

    def get_hash(self, key):
        h = 0
        for char in key:
            h += ord(char)
        return h % self.MAX

    def __setitem__(self, key, value):
        h = self.get_hash(key)
        self.arr[h] = value

    def __getitem__(self, item):
        h = self.get_hash(item)
        return self.arr[h]

    def __delitem__(self, key):
        h = self.get_hash(key)
        self.arr[h] = None


if __name__ == '__main__':

    hT = HashTable()
    hT["Key One"] = "ABC"
    hT["Key Two"] = "PQR"
    hT["Key Three"] = "LMN"
    hT["Key Four"] = "XYZ"

    print("Value at Key Three is {}".format(hT["Key Three"]))
    print("Value at Key One is {}".format(hT["Key One"]))

    del hT["Key Two"]
    print(hT.arr)

```