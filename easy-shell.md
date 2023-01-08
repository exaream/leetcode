# Easy Level Problems

- https://leetcode.com/problemset/all/?topicSlugs=shell&page=1&difficulty=EASY&status=NOT_STARTED

## 193. Valid Phone Numbers

- https://leetcode.com/problems/valid-phone-numbers/

- Runtime 99 ms, Memory 3.2 MB
```shell
# -e Multiple regular expressions can be specified
grep -e "^[0-9]\{3\}\-[0-9]\{3\}\-[0-9]\{4\}$" -e "^([0-9]\{3\}) [0-9]\{3\}\-[0-9]\{4\}$" file.txt
```
- Runtime 82 ms, Memory 3.1 MB
```shell
# -P: Perl-compatible regular expressions
grep -P "^(\([0-9]{3}\) |[0-9]{3}\-)[0-9]{3}\-[0-9]{4}$" file.txt
```
- Runtime 79 ms, Memory 3.1 MB
```shell
# -P: Perl-compatible regular expressions
grep -P "\A(\([0-9]{3}\) |[0-9]{3}\-)[0-9]{3}\-[0-9]{4}\z" file.txt
```


## 195. Tenth Line

- https://leetcode.com/problems/tenth-line/
- Runtime 41 ms, Memory 4 MB
```shell
awk NR==10 file.txt
```
- Runtime 36 ms, Memory 3.6 MB
```shell
tail -n +10  file.txt | head -n 1
```
- Runtime 32 ms, Memory 3.7 MB
```shell
sed -n 10P file.txt
```
- Runtime 32 ms, Memory 3.5 MB
```shell
i=0
while read line
do
  let 'i = i + 1'
  if [ $i -eq 10 ]; then
    echo $line
    exit 0
  fi
done < file.txt
```
- Runtime 29 ms, Memory 3.7 MB
```shell
i=0
while read line
do
  i=$(($i+1))
  if [ $i -eq 10 ]; then
    echo $line
    exit 0
  fi
done < file.txt
```

