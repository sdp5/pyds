## Singly linked list
#### Reverse and Pair-swap

```python

#!/usr/bin/env python3

class Node:
    def __init__(self, val, next=None):
        self.val = val
        self.next = next


class LinkedList:
    head = None

    def last_node(self):
        itr = self.head
        while itr.next:
            itr = itr.next
        return itr

    def add_node(self, val):
        new_node = Node(val)
        if not self.head:
            self.head = new_node
        else:
            self.last_node().next = new_node

    def print_list(self):
        itr = self.head
        while itr:
            print(f"{itr.val}", end="")
            if itr.next:
                print(" -> ", end="")
            itr = itr.next
        print("")

    def reverse(self):
        prev = None
        curr = self.head
        next = None

        while curr:
            next = curr.next
            curr.next = prev
            prev, curr = curr, next
        self.head = prev

    def is_empty(self):
        return self.head is None

    def swap(self):
        if self.is_empty():
            return
        curr = self.head
        next = curr.next
        new_head = None

        while next:
            if not next.next:
                curr.next = None
                next.next = curr
                if not new_head:
                    new_head = next
                break
            p1 = curr.next.next
            p2 = next.next.next
            curr.next = next.next \
                if not next.next.next \
                else next.next.next
            next.next = curr
            if not new_head:
                new_head = next
            curr, next = p1, p2

        if new_head:
            self.head = new_head


if __name__ == "__main__":
    ll = LinkedList()
    ll.add_node(88)
    ll.add_node(34)
    ll.add_node(12)
    ll.add_node(90)
    ll.add_node(10)
    ll.add_node(90)
    ll.add_node(75)
    ll.add_node(64)

    ll.print_list()
    ll.reverse()
    ll.print_list()
    ll.swap()
    ll.print_list()


```


## Doubly linked list

```python

#!/usr/bin/env python3


class Node:
    def __init__(self, data=None, next=None, prev=None):
        self.data = data
        self.next = next
        self.prev = prev


class LinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def print_forward(self):
        # This method prints list in forward direction. Use node.next
        if self.head is None:
            print("Linked list is empty")
            return
        itr = self.head
        llstr = ''
        while itr:
            llstr += str(itr.data)+' --> ' if itr.next else str(itr.data)
            itr = itr.next
        print(llstr)

    def print_backward(self):
        # Print linked list in reverse direction. Use node.prev for this.

        if self.tail is None:
            print("Linked list is empty")
            return
        itr = self.tail
        llstr = ''
        while itr:
            llstr += str(itr.data)+' --> ' if itr.prev else str(itr.data)
            itr = itr.prev
        print(llstr)

    def get_length(self):
        count = 0
        itr = self.head
        while itr:
            count += 1
            itr = itr.next

        return count

    def insert_at_beginning(self, data):
        if self.head is None and self.tail is None:
            # list is empty
            node = Node(data)
            self.head = node
            self.tail = node
        else:
            node = Node(data, self.head)
            self.head = node
            self.head.next.prev = node

    def insert_at_end(self, data):
        if self.head is None and self.tail is None:
            # list is empty
            node = Node(data)
            self.head = node
            self.tail = node
        else:
            node = Node(data, None, self.tail)
            self.tail = node
            self.tail.prev.next = node

    def insert_at(self, index, data):
        if index < 0 or index > self.get_length():
            raise Exception("Invalid Index")

        if index == 0:
            self.insert_at_beginning(data)
            return

        if index == self.get_length():
            self.insert_at_end(data)
            return

        count = 0
        itr = self.head
        while itr:
            if count == index - 1:
                node = Node(data, itr.next, itr)
                itr.next = node
                itr.next.next.prev = node
                break

            itr = itr.next
            count += 1

    def remove_at(self, index):
        if index < 0 or index >= self.get_length():
            raise Exception("Invalid Index")

        if index == 0:
            if self.head.next is None:
                self.head = None
                self.tail = None
                return
            self.head = self.head.next
            self.head.prev = None
            return

        if index == self.get_length() - 1:
            if self.tail.prev is None:
                self.head = None
                self.tail = None
                return
            self.tail = self.tail.prev
            self.tail.next = None
            return

        count = 0
        itr = self.head
        while itr:
            if count == index - 1:
                itr.next.next.prev = itr
                itr.next = itr.next.next
                break

            itr = itr.next
            count += 1

    def insert_values(self, data_list):
        self.head = None
        self.tail = None
        for data in data_list:
            self.insert_at_end(data)

    def insert_after_value(self, data_after, data_to_insert):
        # Search for first occurrence of data_after value in linked list
        # Now insert data_to_insert after data_after node

        count = 0
        itr = self.head

        while itr:
            if itr.data == data_after:
                temp = Node(data_to_insert, itr.next, itr)
                itr.next = temp
                itr.next.next.prev = temp
                break

            itr = itr.next
            count += 1

    def remove_by_value(self, data):

        count = 0
        itr = self.head
        found = False

        if self.head.data == data:
            self.remove_at(0)
            return

        if self.tail.data == data:
            self.remove_at(self.get_length() - 1)
            return

        while itr:
            if itr.data == data:
                found = True
                itr.prev.next = itr.next
                itr.next.prev = itr.prev
                break

            itr = itr.next
            count += 1
        if not found:
            print("{} not found in the list".format(data))


if __name__ == '__main__':
    ll = LinkedList()
    ll.insert_values(["banana", "mango", "grapes", "orange"])
    ll.print_forward()
    ll.print_backward()
    ll.insert_after_value("mango", "apple")  # insert apple after mango
    ll.print_forward()
    ll.print_backward()
    ll.remove_by_value("orange")  # remove orange from linked list
    ll.print_forward()
    ll.print_backward()
    ll.remove_by_value("figs")
    ll.remove_by_value("banana")
    ll.remove_by_value("mango")
    ll.remove_by_value("apple")
    ll.print_forward()
    ll.print_backward()
    ll.remove_by_value("grapes")
    ll.print_forward()
    ll.print_backward()

```
