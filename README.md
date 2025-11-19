# 1. Intro

## 1.1 Node Class

```python
class Node:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

## 1.2 Binary Search (Array)

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

---

# 2. Construction

## 2.1 Height, Count Nodes, and Combined Solution

```python
def height(root):
    if root is None:
        return -1
    left_h = height(root.left)
    right_h = height(root.right)
    return 1 + max(left_h, right_h)
```

```python
def count_nodes(root):
    if root is None:
        return 0
    return 1 + count_nodes(root.left) + count_nodes(root.right)
```

```python
def soln(root):
    return height(root) - count_nodes(root)
```

---

# 3. Traversal

## 3.1 Decreasing Order (Reverse Inorder)

```python
def decreasing_order(root):
    if not root:
        return []
    else:
        return decreasing_order(root.right) + [root.val] + decreasing_order(root.left)
```

---

# 4. Operations

## 4.1 Insert

```python
def insert(root, val):
    if not root:
        return Node(val)
    if val <= root.val:
        root.left = insert(root.left, val)
    elif val > root.val:
        root.right = insert(root.right, val)
    return root
```

## 4.2 Find Maximum

```python
def find_max(root):
    if root.right is None:
        return root
    return find_max(root.right)
```

## 4.3 Remove Maximum

```python
def remove_max(root):
    if not root.right:
        return root.left
    root.right = remove_max(root.right)
    return root
```

---

# Final Problem: Implement `remove`

```python
def remove(root, target):
    if not root:
        return None

    if root.val > target:
        root.left = remove(root.left, target)
    elif root.val < target:
        root.right = remove(root.right, target)
    else:
        if not root.left:
            return root.right
        if not root.right:
            return root.left

        pred = find_max(root.left)  # Given
        root.val = pred.val
        root.left = remove_max(root.left)  # Given

    return root
```
