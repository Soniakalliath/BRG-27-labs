# Regular Expressions 101: Beginner's Guide

Regular expressions (regex) are sequences of characters used to match patterns in strings. They are widely used in programming, scripting, and command-line tools like `grep`, `sed`, `awk`, and languages like Python, JavaScript, and more.

---

## 🔹 Basic Structure

A regex is made up of **literal characters** and **metacharacters**. For example:
```
^hello.*world$
```

---

## 🔹 Common Metacharacters

| Symbol | Meaning                                 | Example        | Matches                          |
|--------|------------------------------------------|----------------|----------------------------------|
| `.`    | Any single character (except newline)    | `a.c`          | `abc`, `a1c`, `a-c`              |
| `^`    | Start of line                            | `^Hi`          | Matches line starting with "Hi" |
| `$`    | End of line                              | `bye$`         | Matches line ending in "bye"    |
| `*`    | 0 or more of the previous character      | `lo*`          | `l`, `lo`, `loo`, `looo`        |
| `+`    | 1 or more of the previous character      | `lo+`          | `lo`, `loo`, `looo`             |
| `?`    | 0 or 1 of the previous character         | `lo?`          | `l`, `lo`                        |
| `[]`   | Any one of the characters inside         | `[abc]`        | `a`, `b`, or `c`                 |
| `[^]`  | Not any of the characters inside         | `[^0-9]`       | Any non-digit                    |
| `{n}`  | Exactly n times                          | `a{3}`         | `aaa`                            |
| `{n,}` | n or more times                          | `a{2,}`        | `aa`, `aaa`, `aaaa`             |
| `{n,m}`| Between n and m times                    | `a{2,4}`       | `aa`, `aaa`, `aaaa`             |
| `|`    | OR operator                              | `cat|dog`      | `cat` or `dog`                  |
| `()`   | Grouping                                 | `(ab)+`        | `ab`, `abab`, `ababab`          |
| `\`   | Escape character                         | `\.`          | Literal dot `.`                 |

---

## 🔹 Common Character Classes

| Class      | Meaning                      | Matches             |
|------------|------------------------------|---------------------|
| `\d`      | Digit (0–9)                  | `1`, `9`, etc.      |
| `\D`      | Non-digit                    | `a`, `-`, etc.      |
| `\w`      | Word character (alphanumeric + `_`) | `a`, `Z`, `9`, `_` |
| `\W`      | Non-word character           | `@`, `#`, space     |
| `\s`      | Whitespace                   | Space, tab, newline |
| `\S`      | Non-whitespace               | `a`, `1`, `#`       |
| `.`        | Any character (except newline)| `a`, `9`, `!`, etc. |

---

## 🔹 Anchors

| Anchor | Description                   |
|--------|-------------------------------|
| `^`    | Start of a line               |
| `$`    | End of a line                 |
| `\b`  | Word boundary                 |
| `\B`  | Not a word boundary           |

---

## 🔹 Examples

| Pattern         | Description                                |
|----------------|--------------------------------------------|
| `^\d{3}-\d{2}-\d{4}$` | SSN format (e.g., 123-45-6789)         |
| `[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.com` | Basic email ending in .com |
| `\bcat\b`     | Matches the word "cat" only (not "catalog")|
| `^[^#]`         | Lines that do not start with `#`           |

---

## 🔹 Use in Tools

### `grep`
```bash
grep '^Error' logfile.txt
```

### `sed`
```bash
sed -n '/^User/p' users.txt
```

### `awk`
```bash
awk '/404/' access.log
```

---

## 🔹 Tips

- Always **escape special characters** in regex when needed (e.g., `\.` to match a dot).
- Use online testers like [regex101.com](https://regex101.com) to experiment.

---

Happy matching! 🎯
