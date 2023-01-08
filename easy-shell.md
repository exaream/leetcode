# Easy Level Problems

- https://leetcode.com/problemset/all/?topicSlugs=shell&page=1&difficulty=EASY&status=NOT_STARTED

## 193. Valid Phone Numbers

- https://leetcode.com/problems/valid-phone-numbers/

- Runtime 99 ms, Memory 3.2 MB
```shell
# Read from the file file.txt and output all valid phone numbers to stdout.
# -e Multiple regular expressions can be specified
grep -e "^[0-9]\{3\}\-[0-9]\{3\}\-[0-9]\{4\}$" -e "^([0-9]\{3\}) [0-9]\{3\}\-[0-9]\{4\}$" file.txt
```
- Runtime 82 ms, Memory 3.1 MB
```shell
# Read from the file file.txt and output all valid phone numbers to stdout.
# -P: Perl-compatible regular expressions
grep -P "^(\([0-9]{3}\) |[0-9]{3}\-)[0-9]{3}\-[0-9]{4}$" file.txt
```
- Runtime 79 ms, Memory 3.1 MB
```shell
# Read from the file file.txt and output all valid phone numbers to stdout.
# -P: Perl-compatible regular expressions
grep -P "\A(\([0-9]{3}\) |[0-9]{3}\-)[0-9]{3}\-[0-9]{4}\z" file.txt
```
