# Binary Tree

```python

#!/usr/bin/env python3

from functools import reduce


class BinarySearchTreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

    def add_child(self, data):
        if data == self.data:
            return
        if data < self.data:
            if self.left:
                self.left.add_child(data)
            else:
                self.left = BinarySearchTreeNode(data)
        else:
            if self.right:
                self.right.add_child(data)
            else:
                self.right = BinarySearchTreeNode(data)

    def in_order_traversal(self):
        elements = []
        if self.left:
            elements += self.left.in_order_traversal()
        elements += [self.data]
        if self.right:
            elements += self.right.in_order_traversal()
        return elements

    def search(self, val):
        if self.data == val:
            return True
        if val < self.data:
            if self.left:
                return self.left.search(val)
            else:
                return False
        if val > self.data:
            if self.right:
                return self.right.search(val)
            else:
                return False

    def find_min(self):
        if not self.left:
            return self.data
        return self.left.find_min()

    def find_max(self):
        if not self.right:
            return self.data
        return self.right.find_max()

    def calculate_sum(self):
        return reduce(
            lambda x, y: x+y, self.in_order_traversal()
        )

    def post_order_traversal(self):
        elements = []
        if self.left:
            elements += self.left.in_order_traversal()
        if self.right:
            elements += self.right.in_order_traversal()
        elements += [self.data]
        return elements

    def pre_order_traversal(self):
        elements = []
        elements += [self.data]
        if self.left:
            elements += self.left.in_order_traversal()
        if self.right:
            elements += self.right.in_order_traversal()
        return elements

    def breadth_first_traversal(self):
        elements = []
        elements += [self.data]
        if self.left:
            elements += [self.left.data]
        if self.right:
            elements += [self.right.data]
        left, right = self.left, self.right
        while left and right:
            if left.left:
                elements += [left.left.data]
            if left.right:
                elements += [left.right.data]
            if right.left:
                elements += [right.left.data]
            if right.right:
                elements += [right.right.data]
            left, right = left.left, right.right
        return elements

    def delete(self, val):
        if val < self.data:
            if self.left:
                self.left = self.left.delete(val)
        elif val > self.data:
            if self.right:
                self.right = self.right.delete(val)
        else:
            if not self.left and not self.right:
                return
            if not self.left:
                return self.right
            if not self.right:
                return self.left

            # min_val = self.right.find_min()
            # self.data = min_val
            # self.right = self.right.delete(min_val)

            # or, take max from left subtree
            max_val = self.left.find_max()
            self.data = max_val
            self.left = self.left.delete(max_val)
        return self


def build_tree(elements):
    root = BinarySearchTreeNode(elements[0])
    for i in elements:
        root.add_child(i)
    return root


if __name__ == "__main__":
    numbers = [17, 4, 1, 20, 9, 23, 18, 34]
    countries = [
        "India",
        "Pakistan",
        "Germany",
        "USA",
        "China",
        "India",
        "UK",
        "USA"
    ]

    numbers_tree = build_tree(numbers)
    print(numbers_tree.in_order_traversal())
    print(numbers_tree.search(210))
    print(numbers_tree.find_min())
    print(numbers_tree.find_max())
    print(numbers_tree.calculate_sum())
    print(numbers_tree.post_order_traversal())
    print(numbers_tree.pre_order_traversal())
    print(numbers_tree.breadth_first_traversal())
    numbers_tree.delete(9)
    print("After deleting 9", numbers_tree.breadth_first_traversal())
    numbers_tree.delete(23)
    print("After deleting 23", numbers_tree.breadth_first_traversal())
    numbers_tree.delete(17)
    print("After deleting 17", numbers_tree.breadth_first_traversal())

    countries_tree = build_tree(countries)
    print(countries_tree.in_order_traversal())
    print("UK is in the list? ", countries_tree.search("UK"))
    print("Sweden is in the list? ", countries_tree.search("Sweden"))


```