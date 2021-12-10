# Tree

```python

#!/usr/bin/env python3

class TreeNode:

    def __init__(self, data):
        self.data = data
        self.children = []
        self.parent = None

    def add_child(self, child):
        child.parent = self
        self.children.append(child)

    def get_level(self):
        level = 0
        p = self.parent
        while p:
            level += 1
            p = p.parent
        return level

    def print_tree(self, p_format=None, level=0):
        if self.get_level() > level:
            return
        spaces = "  " * self.get_level()
        prefix = spaces + "|__" if self.parent else ""
        print_format = ""
        if isinstance(self.data, str):
            print_format = prefix + self.data
        if isinstance(self.data, (list, tuple, set)):
            print_format = prefix + self.data[0] + " (" + self.data[1] + ")"
            if p_format and p_format == "name":
                print_format = prefix + self.data[0]
            if p_format and p_format == "designation":
                print_format = prefix + self.data[1]
        print(print_format)
        for child in self.children:
            child.print_tree(p_format=p_format, level=level)


def build_product_tree():
    root = TreeNode("Electronics")

    laptop = TreeNode("Laptop")
    laptop.add_child(TreeNode("Mac"))
    laptop.add_child(TreeNode("Surface"))
    laptop.add_child(TreeNode("Thinkpad"))

    cellphone = TreeNode("Cell Phone")
    cellphone.add_child(TreeNode("iPhone"))
    cellphone.add_child(TreeNode("Google Pixel"))
    cellphone.add_child(TreeNode("Vivo"))

    tv = TreeNode("TV")
    tv.add_child(TreeNode("Samsung"))
    tv.add_child(TreeNode("LG"))

    root.add_child(laptop)
    root.add_child(cellphone)
    root.add_child(tv)

    return root


def build_mgmt_hierarchy():
    root = TreeNode(("Nilupul", "CEO"))

    eng = TreeNode(("Chinmay", "CTO"))
    infra = TreeNode(("Vishwa", "Infrastructure Head"))
    infra.add_child(TreeNode(("Dhaval", "Cloud Manager")))
    infra.add_child(TreeNode(("Abhijit", "App Manager")))
    eng.add_child(infra)
    eng.add_child(TreeNode(("Aamir", "Application Head")))

    hr = TreeNode(("Gels", "HR Head"))
    hr.add_child(TreeNode(("Peter", "Recruitment Manager")))
    hr.add_child(TreeNode(("Waqas", "Policy Manager")))

    root.add_child(eng)
    root.add_child(hr)
    return root


def build_location_tree():
    root = TreeNode("Global")

    india = TreeNode("India")

    gujarat = TreeNode("Gujarat")
    gujarat.add_child(TreeNode("Ahmedabad"))
    gujarat.add_child(TreeNode("Baroda"))
    india.add_child(gujarat)

    karnataka = TreeNode("Karnataka")
    karnataka.add_child(TreeNode("Bengluru"))
    karnataka.add_child(TreeNode("Mysore"))
    india.add_child(karnataka)

    usa = TreeNode("USA")

    new_jersey = TreeNode("New Jersey")
    new_jersey.add_child(TreeNode("Princeton"))
    new_jersey.add_child(TreeNode("Trenton"))
    usa.add_child(new_jersey)

    california = TreeNode("California")
    california.add_child(TreeNode("San Francisco"))
    california.add_child(TreeNode("Mountain View"))
    california.add_child(TreeNode("Palo Alto"))
    usa.add_child(california)

    root.add_child(india)
    root.add_child(usa)
    return root


if __name__ == "__main__":
    # root = build_product_tree()
    root = build_mgmt_hierarchy()
    # root = build_location_tree()
    root.print_tree(level=1)
    

```