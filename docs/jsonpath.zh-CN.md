![GitHub top language](https://img.shields.io/github/languages/top/thiliapr/python3-tprtools)
![GitHub License](https://img.shields.io/badge/license-GPL--3.0--or--later-blue)
![GitHub repo size](https://img.shields.io/github/repo-size/thiliapr/python3-tprtools)
![GitHub forks](https://img.shields.io/github/forks/thiliapr/python3-tprtools)
![GitHub Repo stars](https://img.shields.io/github/stars/thiliapr/python3-tprtools)

# TkJSONPath
这是一个简单的JSONPath解析器。
- 版权: 根据GPL-3.0或更高版本分发。

## 语言
- [简体中文](jsonpath.zh-CN.md)
- [English](jsonpath.md)

## 使用
- 以下示例展示了4个基本函数的使用。
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
  1. `src`被赋值为一个字典。
  2. 将`path_a`与`path_b`拼合，赋值给`path_ab`。
  3. 获取`src`中路径`path_ab`的值，赋值给`how_1`。
  4. 将`src`复制出一份副本，赋值给`dst`。
  5. 赋值给`dst`中路径`$.docs[1].id`的值，值为`4`。

## 类型
- `Key: Union[int, str]`
  指示JSON的键的类型。
- `Path: list[Key]`
  指示JSONPath的路径的类型。
- `JSONObject: Union[list, dict]`
  指示JSON对象的类型。

## 函数
- `concat_path(path: str, obj_path: str) -> str`
  将两个路径连接起来。
- `str_path(path: Path) -> str`
  将Path型的路径转化为字符串型。
- `get_safe_key(key: str) -> str`
  获取安全的键值。（用于字符串型路径）
- `parse_path(path_str: str) -> Path`
  将字符串型的路径转化为Path型。
- `get(target: JSONObject, path: str | Path, default: Any = ...) -> Any:`
  从`target`中获取指定路径的值。
- `assign(target: JSONObject, path: str | Path, value: Any) -> Any`
  给`target`的路径`path`赋值。
