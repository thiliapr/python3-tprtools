![GitHub top language](https://img.shields.io/github/languages/top/thiliapr/python3-tprtools)
![GitHub License](https://img.shields.io/badge/license-GPL--3.0--or--later-blue)
![GitHub repo size](https://img.shields.io/github/repo-size/thiliapr/python3-tprtools)
![GitHub forks](https://img.shields.io/github/forks/thiliapr/python3-tprtools)
![GitHub Repo stars](https://img.shields.io/github/stars/thiliapr/python3-tprtools)

# TkJSONPath
This is a simple JSONPath parser.
- License: Distributed under GPL-3.0 or later.

## Languages
- [简体中文](jsonpath.zh-CN.md)
- [English](jsonpath.md)

## Usage
- Below are examples demonstrating the usage of four basic functions:
  ```python
  from tprtools import jsonpath
  
  src = {"docs": [{"how": "how?", "id": 1}, {"how": "emm", "id": 2}]}
  
  path_a = "$.docs"
  path_b = "$[0].how"
  
  # path_ab -> "$.docs[0].how"
  path_ab = jsonpath.concat_path(path_a, path_b)
  
  # how_1 -> "how?"
  how_1 = jsonpath.get(src, path_ab)
  
  # dst -> src
  dst = src.copy()
  # dst["docs"][1]["id"] -> 4
  jsonpath.assign(dst, "$.docs[1].id", 4)
  ```
  1. `src` is assigned a dictionary.
  2. Concatenate `path_a` and `path_b`, assigning the result to `path_ab`.
  3. Retrieve the value at the `path_ab` location in `src`, assigning it to `how_1`.
  4. Create a copy of `src` and assign it to `dst`.
  5. Assign the value `4` to the path `$.docs[1].id` in `dst`.

## Types
- `Key: Union[int, str]`
  Indicates the type of JSON key.
- `Path: list[Key]`
  Indicates the type of JSONPath path.
- `JSONObject: Union[list, dict]`
  Indicates the type of JSON object.

## Functions
- `concat_path(path: str, obj_path: str) -> str`
  Concatenate two paths.
- `str_path(path: Path) -> str`
  Convert a Path type path to a string type.
- `get_safe_key(key: str) -> str`
  Get a safe key value. (For string type paths)
- `parse_path(path_str: str) -> Path`
  Convert a string type path to a Path type.
- `get(target: JSONObject, path: str | Path, default: Any = ...) -> Any:`
  Get the value of the specified path from `target`.
- `assign(target: JSONObject, path: str | Path, value: Any) -> Any`
  Assigns a value to the path `path` of `target`.