# [Python] 基本の備忘録

## for range

rangeの使い方に注意。

第2引数は「未満」の条件を表す。「以下」ではない

```python
t = 5
for i in range(0,t):
    print("hoge")
```

これはC/C++ならば、

```c
int t = 5;
for(int i = 0; i < t; i++) {    // i <= t ではない！
    printf("hoge");
}
```

VisualBasicなら、

```vb
Dim t As Integer
t = 5
For i = 0 To t-1    ' tではなくt-1 ！
    Console.WriteLine("hoge")
Next i
```
