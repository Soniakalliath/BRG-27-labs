# AWK 101: Beginner's Guide

`awk` is a powerful Unix/Linux tool for text processing, pattern scanning, and data extraction.

---

## 🔹 Basic Syntax

```bash
awk 'pattern { action }' filename
```

- `pattern`: condition to match lines (optional)
- `action`: command(s) to execute
- `filename`: file to operate on

---

## 🔹 Field References

- `$0`: entire line
- `$1`, `$2`, ..., `$NF`: individual fields
- `NF`: number of fields
- `NR`: current line number

---

## 🔹 Common Examples

| Task                            | Command                                    | Description                            |
|---------------------------------|--------------------------------------------|----------------------------------------|
| Print every line                | `awk '{ print }' file.txt`                 | Same as `cat`                          |
| Print first column              | `awk '{ print $1 }' file.txt`              |                                        |
| Print 2nd and 4th columns       | `awk '{ print $2, $4 }' file.txt`          |                                        |
| Skip empty lines                | `awk 'NF > 0' file.txt`                    |                                        |
| Match a pattern                 | `awk '/error/' file.log`                   | Lines containing "error"               |
| Print line numbers              | `awk '{ print NR, $0 }' file.txt`          |                                        |
| Sum column 3                    | `awk '{ sum += $3 } END { print sum }'`    |                                        |
| Average column 2               | `awk '{ sum += $2 } END { print sum/NR }'` |                                        |
| Count matching lines            | `awk '/404/ { count++ } END { print count }'` | Count 404 errors in a log           |

---

## 🔹 Example Data

File: `data.txt`

```
Alice 90 85
Bob 88 78
Carol 82 95
```

Command:
```bash
awk '{ print $1, ($2 + $3) / 2 }' data.txt
```

Output:
```
Alice 87.5
Bob 83
Carol 88.5
```

---

## 🔹 Special Blocks

- `BEGIN {}`: runs before processing lines
- `END {}`: runs after all lines are processed

Example:
```bash
awk 'BEGIN { print "Start" } { print $1 } END { print "End" }' file.txt
```

---

## 🔹 Field Separator

Set a custom field separator with `-F`

```bash
awk -F: '{ print $1 }' /etc/passwd
```

---

## 🔹 Pass Variable to AWK

```bash
awk -v threshold=80 '$2 > threshold { print $1 }' file.txt
```

---

## 🔹 Quick Inline Test

```bash
echo -e "a b c\nd e f" | awk '{ print $2 }'
```

---

## 🔹 Apache Log Example

```bash
awk '{ print $1, $9 }' /var/log/apache2/access.log
```
Extracts IP address and HTTP status code.

---

Happy scripting! 🎉
