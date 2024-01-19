+++
title = 'Minimal doubly linked list'
date = 2022-10-22T13:56:52-08:00
lastmod = 2022-11-20T05:52:35-08:00
+++

Below are relatively simple ways to create [doubly linked lists](https://en.wikipedia.org/wiki/Doubly_linked_list) in Python and C++.

## Python

```python
class Node:
    def __init__(self, data, *, previous=None, next=None):
        self.data = data
        self.previous = previous
        self.next = next

class DoublyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def append(self, data):
        if self.head is None:
            self.head = Node(data)
            self.tail = self.head
        else:
            self.tail.next = Node(data, previous=self.tail)
            self.tail = self.tail.next

    def prepend(self, data):
        if self.head is None:
            self.head = Node(data)
            self.tail = self.head
        else:
            self.head.previous = Node(data, next=self.head)
            self.head = self.head.previous

    def clear(self):
        self.head = None
        self.tail = None

    def print_list(self):
        node = self.head
        while node is not None:
            print(end=f"{node.data} ")
            node = node.next
        print()

def main():
    dll = DoublyLinkedList()
    dll.append(5)
    dll.append(3)
    dll.append(8)
    dll.append(2)
    dll.append(7)

    dll.prepend(1)

    dll.print_list()  # 1 5 3 8 2 7

if __name__ == "__main__":
    main()
```

## C++

```cpp
#include <iostream>
using namespace std;

class Node
{
public:
    int data;
    Node* previous = NULL;
    Node* next = NULL;
    Node(int data)
    {
        this->data = data;
    }
};

class DoublyLinkedList
{
public:
    void append(int data)
    {
        if (head == NULL)
        {
            head = new Node(data);
            tail = head;
        }
        else
        {
            Node* new_node_ptr = new Node(data);
            new_node_ptr->previous = tail;
            tail->next = new_node_ptr;
            tail = new_node_ptr;
        }
    }

    void prepend(int data)
    {
        if (head == NULL)
        {
            head = new Node(data);
            tail = head;
        }
        else
        {
            Node* new_node_ptr = new Node(data);
            new_node_ptr->next = head;
            head->previous = new_node_ptr;
            head = new_node_ptr;
        }
    }

    void print_list()
    {
        for (Node* ptr = head; ptr != NULL; ptr = ptr->next)
            cout << ptr->data << " ";
    }

    void clear()
    {
        Node* temp = NULL;
        while (head != NULL)
        {
            temp = head->next;
            delete head;
            head = temp;
        }
        tail = NULL;
    }

    ~DoublyLinkedList()
    {
        clear();
    }

private:
    Node* head = NULL;
    Node* tail = NULL;
};

int main()
{
    DoublyLinkedList dll;
    dll.append(5);
    dll.append(3);
    dll.append(8);
    dll.append(2);
    dll.append(7);

    dll.prepend(1);

    dll.print_list();  // 1 5 3 8 2 7 

    cout << endl;
    return 0;
}
```
