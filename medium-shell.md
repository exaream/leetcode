# Medium Level Problems

- https://leetcode.com/problemset/all/?topicSlugs=shell&page=1&difficulty=MEDIUM&status=NOT_STARTED


## 192. Word Frequency

- https://leetcode.com/problems/word-frequency/
- Runtime 94 ms, Memory 3.9 MB
```shell
# At first, replace spaces with new lines using tr
cat words.txt | tr -s ' ' '\n' | sort | uniq -c | sort -r | awk '{print $2 " " $1}'
```
- Runtime 62 ms, Memory 3.8 MB
```shell
# NF: number of fields
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


## 194. Transpose File

- https://leetcode.com/problems/transpose-file/
- Runtime 433 ms, Memory 3.5 MB
```shell
head -1 file.txt | wc -w | xargs seq 1 | xargs -I{} -n 1 sh -c "cut -d ' ' -f{} file.txt | paste -sd ' ' -"
```
- Runtime 258 ms, Memory 3.6 MB
```shell
col_num=`head -n1 file.txt | wc -w`

for i in `seq 1 $col_num`
do
    echo `cut -d' ' -f$i file.txt`
done
```
- Runtime 86 ms, Memory 3.9 MB
```shell
# NF: number of fields
# NR: number of rows
awk '
{
    for (i = 1; i <= NF; i++) {
        if (NR == 1) {
            t[i] = $i;
        } else {
            t[i] = t[i] " " $i
        }
    }
}
END {
    for (i = 1; t[i] != ""; i++) {
        print t[i]
    }
}
' file.txt
```
