# [python] SQLite3 モジュールの使い方

## SQLite3について

単一ファイルやメモリ上にデータを保持するRDBMS

## 使い方

1. インポート
2. コネクション作成
3. カーソル作成
4. SQL実行
5. 結果の利用

### インポート

Pythonの標準モジュールであるため、インストールは不要。

```python
import sqlite3
```

### コネクション作成

```python
dbpath = "sqlitesample.db"
connection = sqlite3.connect(dbpath)
```

### カーソル作成

カーソルはSQL実行結果を保持する入れ物。
SQLiteではCursorを先に作ってから、CursorのメソッドでSQLを実行する。

```python
cursor = connection.cursor()
```

### SQL実行

```python
# テーブルとレコードの作成
cursor.execute("create table dict(key text, value text)")
cursor.execute("insert into dict values ('one', 'ichi')")
cursor.execute("insert into dict values ('two', 'ni')")

# コミット
connection.commit()
```

Cursorを先に作成せずConnectionから直接SQLを実行することもできるが、非標準。

### 結果の利用

executeを実行した結果はCursorオブジェクトとして返されるほか、executeを実行したCursorオブジェクト自体にも入っている。

Cursorはイテレータをサポートしているので、forループが使える。

```python
# 先ほどinsertしたものを読み出してみる
for row in cursor.execute("select * from dict"):
    print(row)
```

結果

```txt
('one', 'ichi')
('two', 'ni')
```

### コネクションのクローズ

もうこれ以上SQLの実行はしないという場合はコネクションをクローズする。

コミットされていない変更は破棄される。

```python
connection.close()
```

with構文 + contextlib.closingを利用して自動的にクローズするようにしてもよい。

```python
from contextlib import closing
with closing(sqlite3.connect(dbpath)) as connection:
    cursor = connection.cursor()
    for row in cursor.execute("select * from dict"):
        print(row)
```
