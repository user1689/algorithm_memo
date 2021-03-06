## 题目
https://leetcode-cn.com/problems/lru-cache/

## 思路
hashMap + doubleLinkedList

## python3
```python3
class DLinkedList:

    def __init__(self, key=0, val=0, prev=None, next=None):
        self.val = val
        self.key = key
        self.prev = prev
        self.next = next

class LRUCache:

    def __init__(self, capacity: int):
        self.map = dict()
        self.size = 0
        self.capacity = capacity
        self.head = DLinkedList()
        self.tail = DLinkedList()
        self.head.next = self.tail
        self.tail.prev = self.head

    def get(self, key: int) -> int:
        if (key not in self.map):
            return -1
        else:
            node = self.map[key]
            self.moveToHead(node)
            return node.val
            
    def put(self, key: int, value: int) -> None:
        if (key in self.map):
            node = self.map[key]
            node.val = value
            self.moveToHead(node)
        else:
            newNode = DLinkedList(key, value)
            self.map[key] = newNode
            self.addToHead(newNode)
            self.size += 1
            if (self.size > self.capacity):
                removed = self.removeTail()
                self.map.pop(removed.key)
                self.size -= 1

    def moveToHead(self, node:DLinkedList) -> None:
        self.deleteNode(node)
        self.addToHead(node)

    def removeTail(self) -> DLinkedList:
        node = self.tail.prev
        self.deleteNode(node)
        return node

    def addToHead(self, node:DLinkedList) -> None:
        node.prev = self.head
        node.next = self.head.next
        self.head.next.prev = node
        self.head.next = node

    def deleteNode(self, node:DLinkedList) -> None:
        node.prev.next = node.next
        node.next.prev = node.prev
 


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)

class Node:
    def __init__(self, key, val, prev=None, next=None):
        self.key = key
        self.val = val
        self.prev = prev
        self.next = next
        
class LRUCache:

    def __init__(self, capacity: int):
        self.size = 0
        self.capacity = capacity
        self.head = Node(-1,-1)
        self.tail = Node(-1,-1)
        self.head.next = self.tail
        self.tail.prev = self.head
        self.map = dict()

    def get(self, key: int) -> int:
        if (key in self.map.keys()):
            node = self.map[key]
            self.moveToHead(node)
            return node.val 
        else:
            return -1
        
    def put(self, key: int, value: int) -> None:
        if (key in self.map.keys()):
            node = self.map[key]
            node.val = value
            self.moveToHead(node)
        else:
            node = Node(key, value)
            self.addToHead(node)
            self.map[key] = node
            self.size += 1
            if self.size > self.capacity:
                removed = self.removeTail()
                kk = removed.key
                del self.map[kk]
                self.size -= 1
    
    def moveToHead(self, node):
        self.removeNode(node)
        self.addToHead(node)
    
    def removeNode(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev
    
    def addToHead(self, node):
        node.prev = self.head
        node.next = self.head.next
        node.next.prev = node
        self.head.next = node
    
    def removeTail(self):
        rr = self.tail.prev
        rr.prev.next = rr.next
        rr.next.prev = rr.prev
        return rr
    

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

## 复杂度分析
* time O(1)
* space O(N)

## 相关题目
1. 待补充



