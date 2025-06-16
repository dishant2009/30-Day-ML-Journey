# 🔍 Hash Tables & Two Sum – Complete Summary

This README captures everything I learned about **hash tables**, **hash functions**, and how Python's `dict` serves as a hash table — particularly in solving the **Two Sum** problem optimally.

---

## 📌 What is a Hash Table?

- A **hash table** is a real data structure that allows **fast access (O(1))** to values using **keys**.
- It uses a **hash function** to convert a key (like a number or string) into an **array index**.
- That index is used to store or retrieve the key-value pair.

### 🔑 Key Properties
- Stores **key-value pairs**
- Uses a **hash function** to compute an index
- **Automatically handles collisions**
- Supports **fast lookup**, **insertion**, and **deletion**

---

## 🧠 What is a Hash Function?

- A **hash function** takes a key and returns a **fixed-size integer**.
- In Python, it's the built-in function `hash(key)`.
- Internally:  
  `index = hash(key) % table_size` (this part is abstracted in Python)

---

## 🧱 Python's `dict` = Hash Table

In Python, the `dict` type is a fully functional **hash table**:
```python
my_dict = {}
my_dict["apple"] = 5  # 'apple' is hashed behind the scenes

