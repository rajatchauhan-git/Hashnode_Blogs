---
title: "Basics of Python for DevOps Engineers"
datePublished: Tue Jul 16 2024 21:10:13 GMT+0000 (Coordinated Universal Time)
cuid: clyowqeqm000108l2fp15cszp
slug: basics-of-python-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721163944497/b91aabbc-a073-45ef-b6f6-8f49fd8fd5f8.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721164162658/c9a270ed-68bd-446a-9994-6b769d7de835.png
tags: python, learning, python3, devops, data-types, python-beginner, 90daysofdevops, trainwithshubham

---

## What is Python?

Python is an open-source, general-purpose, high-level, and object-oriented programming language. It was created by Guido van Rossum and first released in 1991. Python is known for its simplicity and readability, making it a popular choice for beginners and experienced developers. The language supports various programming paradigms, including procedural, object-oriented, and functional programming.

![](https://miro.medium.com/v2/resize:fit:1400/1*ycIMlwgwicqlO6PcFRA-Iw.png align="left")

Python boasts a vast collection of libraries and frameworks that extend its capabilities. Some of the most popular ones include:

* **Django**: *A high-level web framework that encourages rapid development and clean, pragmatic design*.
    
* **TensorFlow**: *An open-source library for machine learning and artificial intelligence.*
    
* **Flask**: *A micro web framework for building small to medium-sized web applications.*
    
* **Pandas**: *A powerful data manipulation and analysis library.*
    
* **Keras**: *An open-source software library that provides a Python interface for artificial neural networks.*
    

## How to Install Python

You can install Python on various operating systems, including Windows, macOS, Ubuntu, and CentOS. Below are the installation steps for different platforms:

![](https://files.realpython.com/media/Python-3-Installation--Setup-Guide_Watermarked.62f654dcab67.jpg align="left")

### Windows Installation

1. Download the Python installer from the [official Python website](https://www.python.org/downloads/).
    
2. Run the installer and follow the prompts. Check the box that says "Add Python to PATH" during installation.
    
3. After installation, open Command Prompt and type `python --version` to verify the installation.
    

### Ubuntu Installation

To install Python on Ubuntu, open the terminal and run the following command:

```bash
sudo apt-get install python3
```

Verify the installation by typing:

```bash
python3 --version
```

### macOS Installation

1. Download the latest version of Python from the [official Python website](https://www.python.org/downloads/macos/).
    
2. Run the downloaded package and follow the installation instructions.
    
3. Open the terminal and type `python3 --version` to verify the installation.
    

### CentOS Installation

To install Python on CentOS, open the terminal and run the following command:

```bash
sudo yum install python3
```

Verify the installation by typing:

```bash
python3 --version
```

## Read About Data Types in Python

Python provides a variety of built-in data types. Understanding these data types is crucial for writing efficient and effective Python code. Below is a detailed overview of the most commonly used data types in Python:

![](https://realpython.com/cdn-cgi/image/width=960,format=auto/https://files.realpython.com/media/Basic-Data-Types-in-Python_Watermarked.e3dd34457952.jpg align="left")

### 1\. Numbers

Python supports different types of numerical data:

* **int**: Integer numbers, e.g., `1`, `42`, `-7`
    
* **float**: Floating-point numbers (decimal numbers), e.g., `3.14`, `2.718`, `-0.001`
    
* **complex**: Complex numbers, e.g., `3+4j`, `5-2j`
    

### 2\. Strings

* **str**: Strings are sequences of characters enclosed in single quotes (`'`), double quotes (`"`), or triple quotes (`'''` or `"""`). For example, `'hello'`, `"world"`, and `"""This is a string"""`.
    

### 3\. Lists

* **list**: Lists are ordered collections of items (which can be of different data types) enclosed in square brackets (`[]`). Lists are mutable, meaning their contents can be changed. For example, `[1, 2, 3]`, `['apple', 'banana', 'cherry']`.
    

### 4\. Tuples

* **tuple**: Tuples are ordered collections of items, similar to lists, but they are immutable, meaning their contents cannot be changed after creation. Tuples are enclosed in parentheses (`()`). For example, `(1, 2, 3)`, `('a', 'b', 'c')`.
    

### 5\. Dictionaries

* **dict**: Dictionaries are unordered collections of key-value pairs enclosed in curly braces (`{}`). Keys must be unique and immutable (e.g., strings, numbers, or tuples), while values can be of any data type. For example, `{'name': 'Alice', 'age': 25}`.
    

### 6\. Sets

* **set**: Sets are unordered collections of unique items enclosed in curly braces (`{}`). Sets are mutable, but their items must be immutable. For example, `{1, 2, 3}`, `{'a', 'b', 'c'}`.
    
* **frozen set**: Frozen sets are immutable versions of sets. They are created using the `frozenset()` function. For example, `frozenset([1, 2, 3])`.
    

### 7\. Boolean

* **bool**: Boolean data types represent one of two values: `True` or `False`. They are used in conditional statements and logical operations. For example, `True`, `False`.
    

### 8\. NoneType

* **NoneType**: The `NoneType` data type represents the absence of a value. It has only one value, `None`. It is often used to signify the absence of a value or a null value. For example, `None`.
    

```python
# Numbers
int_num = 42
float_num = 3.14
complex_num = 3 + 4j

print("Numbers:")
print("Integer:", int_num)
print("Float:", float_num)
print("Complex:", complex_num)
print()

# Strings
single_quote_str = 'hello'
double_quote_str = "world"
triple_quote_str = """This is a string"""

print("Strings:")
print("Single quote:", single_quote_str)
print("Double quote:", double_quote_str)
print("Triple quote:", triple_quote_str)
print()

# Lists
num_list = [1, 2, 3]
mixed_list = ['apple', 'banana', 'cherry']

print("Lists:")
print("Number list:", num_list)
print("Mixed list:", mixed_list)
print()

# Tuples
num_tuple = (1, 2, 3)
mixed_tuple = ('a', 'b', 'c')

print("Tuples:")
print("Number tuple:", num_tuple)
print("Mixed tuple:", mixed_tuple)
print()

# Dictionaries
person = {'name': 'Alice', 'age': 25}

print("Dictionaries:")
print("Person dictionary:", person)
print()

# Sets
num_set = {1, 2, 3}
char_set = {'a', 'b', 'c'}
frozen_set_example = frozenset([1, 2, 3])

print("Sets:")
print("Number set:", num_set)
print("Character set:", char_set)
print("Frozen set:", frozen_set_example)
print()

# Boolean
true_bool = True
false_bool = False

print("Boolean:")
print("True:", true_bool)
print("False:", false_bool)
print()

# NoneType
none_type = None

print("NoneType:")
print("None:", none_type)
```