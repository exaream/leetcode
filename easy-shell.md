# Easy Level Problems

- https://leetcode.com/problemset/all/?topicSlugs=shell&page=1&difficulty=EASY&status=NOT_STARTED

## 193. Valid Phone Numbers

- https://leetcode.com/problems/valid-phone-numbers/

- Runtime 99 ms, Memory 3.2 MB
```shell
# -e: Multiple regular expressions can be specified
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


## 192. Word Frequency

- https://leetcode.com/problems/word-frequency/
- Runtime 94 ms, Memory 3.9 MB
```shell
# At first, replace spaces with new lines using tr
cat words.txt | tr -s ' ' '\n' | sort | uniq -c | sort -r | awk '{print $2 " " $1}'
```
- Runtime 62 ms, Memory 3.8 MB
```shell
# NF: field number
awk '
BEGIN {
    init = 0;
}
{
    for (i = 1; i <= NF; i++) {
        if (init == 0) {
            t[$i] = 1;
            init = 1;
            continue;
        }

        if ($i in t) {
            t[$i] += 1;
            continue;
        }

        t[$i] = 1;
    }
}
END {
    PROCINFO["sorted_in"] = "@val_num_desc";
    for (word in t) {
        print (word, t[word]);
    }
}
' words.txt
```
- Runtime , Memory 
```shell

```
- Runtime , Memory 
```shell

```
- Runtime , Memory 
```shell

```
