# Python Useful Modules

This tutorial presents some useful Python modules that can help you in your daily coding.

## Table of Contents

* [Path](#path)
* [shutil](#shutil)
* [Random](#random)
* [argparse](#argparse)
* [enum](#enum)
* [JSON](#json)

---

# Path

The `pathlib` module provides an object-oriented way to work with **files and directories**. Instead of manipulating file paths as plain strings, you can use `Path` objects with useful methods for navigating, creating, reading, and checking paths.

## Import

```python
from pathlib import Path
```

## Creating a Path

```python
path = Path("data/config.json")

print(path)
# data/config.json
```

A `Path` can represent a file or directory whether or not it currently exists.

## Checking Files and Directories

```python
path = Path("data/config.json")

print(path.exists())
print(path.is_file())
print(path.is_dir())
```

Useful methods:

* `exists()` — checks whether the path exists
* `is_file()` — checks whether the path is a file
* `is_dir()` — checks whether the path is a directory

## Working with Paths

```python
path = Path("data") / "config.json"

print(path)
# data/config.json
```

The `/` operator can be used to join paths.

You can also access different parts of a path:

```python
path = Path("/home/user/data/config.json")

print(path.name)
# config.json

print(path.stem)
# config

print(path.suffix)
# .json

print(path.parent)
# /home/user/data
```

* `.name` — filename
* `.stem` — filename without extension
* `.suffix` — file extension
* `.parent` — parent directory

## Reading and Writing Files

```python
path = Path("data.txt")

path.write_text("Hello Python")

content = path.read_text()

print(content)
# Hello Python
```

`read_text()` reads the file as text, while `write_text()` writes text to the file.

## Creating Directories

```python
path = Path("data/results")

path.mkdir(parents=True, exist_ok=True)
```

* `parents=True` — creates missing parent directories
* `exist_ok=True` — doesn't raise an error if the directory already exists

`pathlib` is useful whenever you need to work with **filesystem paths, files, or directories**.

---

# shutil

The `shutil` module provides high-level operations for **copying, moving, renaming, and deleting files and directories**.

## Import

```python
import shutil
```

## Copying a File

```python
shutil.copy("source.txt", "backup.txt")
```

This copies the file to the destination.

You can also use:

```python
shutil.copy2("source.txt", "backup.txt")
```

`copy2()` preserves additional file metadata such as modification times.

## Copying a Directory

```python
shutil.copytree("project", "project_backup")
```

This copies an entire directory and its contents.

## Moving Files

```python
shutil.move("old.txt", "data/new.txt")
```

This moves a file or directory.

It can also be used to rename something:

```python
shutil.move("old_name.txt", "new_name.txt")
```

## Removing a Directory

```python
shutil.rmtree("project_backup")
```

This removes the directory and everything inside it.

**Be careful:** `rmtree()` permanently removes the directory and its contents.

## Useful Functions

* `copy()` — copy a file
* `copy2()` — copy a file while preserving more metadata
* `copytree()` — copy an entire directory
* `move()` — move or rename a file/directory
* `rmtree()` — remove a directory recursively

`shutil` is useful when you need operations involving **multiple files or complete directories**.

---

# Random

The `random` module provides functions for generating **pseudo-random values**.

## Import

```python
import random
```

## Random Integer

```python
number = random.randint(1, 10)

print(number)
```

`randint(a, b)` returns a random integer between `a` and `b`, **including both endpoints**.

For example:

```python
random.randint(1, 10)
```

can return `1` or `10`.

## Random Floating-Point Number

```python
number = random.random()

print(number)
```

`random()` returns a floating-point number between `0.0` and `1.0`.

## Random Choice

```python
colors = ["red", "blue", "green"]

color = random.choice(colors)

print(color)
```

`choice()` selects one random element from a sequence.

## Shuffle

```python
numbers = [1, 2, 3, 4, 5]

random.shuffle(numbers)

print(numbers)
```

`shuffle()` randomly rearranges the elements of a mutable sequence.

The original list is modified.

## Random Sample

```python
numbers = [1, 2, 3, 4, 5]

result = random.sample(numbers, 2)

print(result)
```

`sample()` selects multiple **unique** elements without modifying the original sequence.

The `random` module is useful for simulations, games, testing, random selections, and generating non-secure random values.

> **Note:** `random` should not be used for passwords, authentication tokens, cryptographic keys, or other security-sensitive values. Use the `secrets` module for those cases.

---

# argparse

The `argparse` module allows you to create **command-line interfaces (CLI)** for Python programs.

It lets users provide arguments and options when starting a program.

## Import

```python
import argparse
```

## Basic Example

```python
parser = argparse.ArgumentParser()

parser.add_argument("name")

args = parser.parse_args()

print(f"Hello {args.name}")
```

Running:

```bash
python main.py Alice
```

produces:

```text
Hello Alice
```

The argument name `"name"` becomes an attribute:

```python
args.name
```

## Optional Arguments

Optional arguments usually start with `--`.

```python
parser.add_argument("--age", type=int)

args = parser.parse_args()

print(args.age)
```

Running:

```bash
python main.py --age 22
```

gives:

```text
22
```

## Default Values

```python
parser.add_argument("--port", type=int, default=8000)
```

If `--port` is not provided, `args.port` will be `8000`.

For example:

```bash
python main.py
```

gives:

```python
args.port == 8000
```

while:

```bash
python main.py --port 5000
```

gives:

```python
args.port == 5000
```

## Type Conversion

`argparse` receives command-line arguments as strings by default.

You can specify a type:

```python
parser.add_argument("--age", type=int)
```

Then:

```bash
python main.py --age 22
```

results in:

```python
args.age
```

being an `int` instead of a `str`.

Common types include:

```python
type=int
type=float
type=str
```

## Help Messages

```python
parser.add_argument(
    "filename",
    help="Path to the input file"
)
```

`argparse` automatically generates a help page:

```bash
python main.py --help
```

It also automatically handles invalid arguments and displays useful error messages.

## Positional vs Optional Arguments

A **positional argument** is required and is identified by its position:

```python
parser.add_argument("filename")
```

Usage:

```bash
python main.py data.txt
```

An **optional argument** is identified by its flag:

```python
parser.add_argument("--output")
```

Usage:

```bash
python main.py --output result.txt
```

`argparse` is useful when you want a Python program to behave like a proper **command-line application**.

---

# enum

The `enum` module allows you to define a set of **named constants**.

It helps avoid using unexplained "magic values" throughout your code.

## Import

```python
from enum import Enum
```

## Creating an Enum

```python
class Color(Enum):
    RED = "red"
    BLUE = "blue"
    GREEN = "green"
```

You can access its members:

```python
print(Color.RED)
# Color.RED

print(Color.RED.value)
# red
```

## Comparing Enum Members

```python
color = Color.RED

if color == Color.RED:
    print("The color is red")
```

Using enum members makes code more explicit than using raw strings:

```python
# Less explicit
color = "red"

# More explicit
color = Color.RED
```

## Iterating Over an Enum

```python
for color in Color:
    print(color)
```

Output:

```text
Color.RED
Color.BLUE
Color.GREEN
```

## `.name` and `.value`

Each enum member has:

* `.name` — the name of the member
* `.value` — the value assigned to the member

Example:

```python
print(Color.RED.name)
# RED

print(Color.RED.value)
# red
```

## Enums With Integers

Enum values don't have to be strings:

```python
from enum import Enum

class Status(Enum):
    PENDING = 1
    RUNNING = 2
    FINISHED = 3
```

You can then write:

```python
status = Status.RUNNING

if status == Status.RUNNING:
    print("Program is running")
```

Enums are useful when a variable should only represent a **fixed set of possible values**, such as states, directions, modes, statuses, or categories.

---

# JSON

The built-in `json` module provides tools for working with **JSON (JavaScript Object Notation)** data. It allows Python programs to convert JSON data into Python objects and convert Python objects back into JSON.

## Import

```python
import json
```

## JSON ↔ Python Conversion

JSON data is mapped to Python types:

| JSON        | Python          |
| ----------- | --------------- |
| Object `{}` | `dict`          |
| Array `[]`  | `list`          |
| String      | `str`           |
| Number      | `int` / `float` |
| `true`      | `True`          |
| `false`     | `False`         |
| `null`      | `None`          |

## `json.loads()`

Converts a JSON **string** into a Python object.

```python
text = '{"name": "Alice", "age": 22}'

data = json.loads(text)

print(data["name"])
# Alice
```

`loads()` is used when the JSON data is already stored in a string.

## `json.dumps()`

Converts a Python object into a JSON **string**.

```python
data = {
    "name": "Alice",
    "age": 22
}

text = json.dumps(data)
```

`indent` can be used to format the resulting JSON:

```python
text = json.dumps(data, indent=4)
```

## `json.load()`

Reads JSON directly from a **file object** and converts it into a Python object.

```python
with open("data.json", "r") as file:
    data = json.load(file)
```

## `json.dump()`

Writes a Python object directly to a **JSON file**.

```python
with open("data.json", "w") as file:
    json.dump(data, file, indent=4)
```

## `load` vs `loads`

The difference is the input source:

```text
load  → file
loads → string
```

Similarly:

```text
dump  → file
dumps → string
```

The `s` in `loads()` and `dumps()` refers to **string**.

## Error Handling

Invalid JSON raises `json.JSONDecodeError`.

```python
try:
    data = json.loads(text)
except json.JSONDecodeError as error:
    print(error.msg)
    print(error.lineno)
    print(error.colno)
```

Useful attributes include:

* `error.msg` — description of the error
* `error.lineno` — line where the error occurred
* `error.colno` — column where the error occurred
* `error.pos` — character position in the input

## Important Distinction

The `json` module validates **JSON syntax**, not application-specific rules.

For example, this is valid JSON:

```json
{
    "age": -500
}
```

The JSON syntax is correct, even though `-500` may be invalid according to an application's rules.

Therefore, JSON parsing and data validation are separate concepts:

```text
JSON text
    ↓
JSON parsing
    ↓
Python object
    ↓
Application validation
    ↓
Validated data
```

The `json` module is therefore mainly responsible for **serialization and deserialization**:

* **Deserialization:** JSON → Python
* **Serialization:** Python → JSON

# Recources

https://www.tradingcode.net/python-programming-articles/
