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

```python

#!/usr/bin/env python3
# Hash Table: Collision Handling


class HashTable:
    def __init__(self):
        self.MAX = 10
        self.arr = [list() for _ in range(self.MAX)]

    def get_hash(self, key):
        key_hash = 0
        for char in key:
            key_hash += ord(char)
        return key_hash % self.MAX

    def __getitem__(self, item):
        h = self.get_hash(item)
        for elem in self.arr[h]:
            if item == elem[0]:
                return elem[1]

    def __setitem__(self, key, value):
        h = self.get_hash(key)
        found = False

        for idx, elem in enumerate(self.arr[h]):
            if len(elem) == 2 and elem[0] == key:
                self.arr[h][idx] = (key, value)
                found = True
                break
        if not found:
            self.arr[h].append((key, value))

    def __delitem__(self, key):
        h = self.get_hash(key)
        for elem in self.arr[h]:
            if key == elem[0]:
                self.arr[h].remove(elem)

    def print(self):
        print("____")
        for idx, elem in enumerate(self.arr):
            print("{}: {}".format(idx, elem))


if __name__ == "__main__":

    ht = HashTable()
    ht['march 6'] = 120
    ht['march 6'] = 78
    ht['march 8'] = 67
    ht['march 9'] = 4
    ht['march 17'] = 459
    ht.print()
    # ____
    # 0: []
    # 1: [('march 8', 67)]
    # 2: [('march 9', 4)]
    # 3: []
    # 4: []
    # 5: []
    # 6: []
    # 7: []
    # 8: []
    # 9: [('march 6', 78), ('march 17', 459)]

    print(ht['march 17'])
    # 459

    del ht['march 9']
    del ht['march 6']
    ht.print()
    # ____
    # 0: []
    # 1: [('march 8', 67)]
    # 2: []
    # 3: []
    # 4: []
    # 5: []
    # 6: []
    # 7: []
    # 8: []
    # 9: [('march 17', 459)]
```
