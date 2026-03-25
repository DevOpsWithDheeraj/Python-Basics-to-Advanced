
# 🔹 1. List in Python

## Definition

A **List** is a collection of items stored in a single variable. It is **ordered, mutable (changeable), and allows duplicates**.

## Key Features

* Ordered (indexing supported)
* Mutable (can modify elements)
* Allows duplicate values
* Can store different data types

## Syntax

```python
list_name = [item1, item2, item3]
```

## Example

```python
my_list = [10, 20, 30, "Python"]

print(my_list[0])      # Access element
my_list[1] = 25        # Modify element
my_list.append(40)     # Add element

print(my_list)
```

## Output

```
10
[10, 25, 30, 'Python', 40]
```

## Common Operations

* `append()` → Add element
* `remove()` → Remove element
* `pop()` → Remove by index
* `len()` → Length of list

---

# 🔹 2. Tuple in Python

## Definition

A **Tuple** is a collection of items that is **ordered but immutable (cannot be changed)**.

## Key Features

* Ordered
* Immutable (no modification after creation)
* Allows duplicates
* Faster than lists (because immutable)

## Syntax

```python
tuple_name = (item1, item2, item3)
```

## Example

```python
my_tuple = (10, 20, 30, "Python")

print(my_tuple[1])   # Access element

# my_tuple[1] = 25 ❌ Error (immutable)
```

## Output

```
20
```

## When to Use Tuple

* When data should not change (e.g., coordinates, fixed values)
* Improves performance and safety

---

# 🔹 3. String in Python

## Definition

A **String** is a sequence of characters enclosed in quotes. It is **ordered and immutable**.

## Key Features

* Ordered (indexing supported)
* Immutable
* Can be iterated
* Supports many built-in methods

## Syntax

```python
string_name = "Hello"
```

## Example

```python
my_string = "Python"

print(my_string[0])        # Access character
print(my_string.lower())   # Convert to lowercase
print(my_string + " Dev")  # Concatenation
```

## Output

```
P
python
Python Dev
```

## Common Operations

* `upper()` / `lower()`
* `strip()`
* `replace()`
* `split()`

---

# 🔥 Difference Between List, Tuple, and String

| Feature    | List         | Tuple      | String        |
| ---------- | ------------ | ---------- | ------------- |
| Mutable    | ✅ Yes        | ❌ No       | ❌ No          |
| Ordered    | ✅ Yes        | ✅ Yes      | ✅ Yes         |
| Duplicates | ✅ Allowed    | ✅ Allowed  | ✅ Allowed     |
| Syntax     | `[ ]`        | `( )`      | `' '` / `" "` |
| Use Case   | Dynamic data | Fixed data | Text data     |

---

# 💡 Simple Real-Life Analogy

* **List** → Shopping list (you can add/remove items anytime)
* **Tuple** → Aadhaar number / Coordinates (fixed, cannot change)
* **String** → Sentence or word (text data)

---
