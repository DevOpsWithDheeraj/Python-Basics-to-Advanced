
# 🔹 1. Sets in Python

## ✅ Definition

A **Set** is an **unordered collection of unique elements**.

👉 Key Points:

* No duplicate values allowed
* Unordered (no indexing)
* Mutable (can add/remove elements)
* Defined using `{}`



## 🔸 Example of Set

```python
my_set = {1, 2, 3, 4, 5}
print(my_set)
```

👉 Output:

```
{1, 2, 3, 4, 5}
```



## 🔸 Duplicate Handling

```python
s = {1, 2, 2, 3, 4}
print(s)
```

👉 Output:

```
{1, 2, 3, 4}
```

✔️ Duplicate `2` is automatically removed.



## 🔸 Set Operations

### 1. Add Element

```python
s = {1, 2, 3}
s.add(4)
print(s)
```



### 2. Remove Element

```python
s.remove(2)
print(s)
```



### 3. Union

```python
a = {1, 2, 3}
b = {3, 4, 5}
print(a | b)
```

👉 Output:

```
{1, 2, 3, 4, 5}
```



### 4. Intersection

```python
print(a & b)
```

👉 Output:

```
{3}
```



## 🔸 Real-Life Example

👉 Think of a set like a **collection of unique students in a class** — no student appears twice.



# 🔹 2. Dictionary in Python

## ✅ Definition

A **Dictionary** is a collection of **key-value pairs**.

👉 Key Points:

* Keys must be unique
* Values can be duplicated
* Ordered (Python 3.7+)
* Mutable
* Defined using `{key: value}`



## 🔸 Example of Dictionary

```python
student = {
    "name": "Dheeraj",
    "age": 22,
    "course": "Python"
}
print(student)
```

👉 Output:

```
{'name': 'Dheeraj', 'age': 22, 'course': 'Python'}
```



## 🔸 Accessing Values

```python
print(student["name"])
```

👉 Output:

```
Dheeraj
```



## 🔸 Adding / Updating

```python
student["age"] = 23      # update
student["city"] = "Kolkata"  # add
print(student)
```



## 🔸 Removing Elements

```python
student.pop("course")
print(student)
```



## 🔸 Looping Through Dictionary

```python
for key, value in student.items():
    print(key, ":", value)
```



## 🔸 Real-Life Example

👉 Think of a dictionary like a **contact list**:

* Name → Phone Number
* Roll No → Student Name



# Difference Between Set and Dictionary

| Feature   | Set         | Dictionary                 |
| --------- | ----------- | -------------------------- |
| Structure | Only values | Key-value pairs            |
| Duplicate | Not allowed | Keys not allowed duplicate |
| Access    | No indexing | Access via key             |
| Example   | `{1, 2, 3}` | `{"a": 1, "b": 2}`         |



# ✅ Final Summary

* **Set** → Unique elements, no duplicates
* **Dictionary** → Key-value mapping
* Both are **mutable and powerful** data structures

---
