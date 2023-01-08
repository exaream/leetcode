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
