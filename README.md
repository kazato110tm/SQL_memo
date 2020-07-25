# set up

- install Home brew

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

```

参考: http://brew.sh/index_ja.html


- mysql install

```
brew update
brew install mysql
```



- mysql start

```
mysql.server start
```


- insert test data

```
mysql -u root
CREATE DATABASE mysql_study;
exit;
mysql -u root -h localhost --default-character-set=utf8 mysql_study < data/mysql_study.backup
```


- check test data


```
mysql -u root
SHOW DATABASES;
USE mysql_study;
SHOW TABLES;
SELECT * FROM areas;
SELECT * FROM genders;
SELECT * FROM lineitems;
SELECT * FROM orders;
SELECT * FROM prefectures;
SELECT * FROM users;
```

## SQLの基本構文
### INSERT

データをテーブルに追加する．
```
INSERT INTO [TABLE_NAME] ([column_name], ...) VALUES([VALUE1], ...);

ex)
INSERT INTO members (name, sex, birth_day) VALUES ('jon', 'male', '1992-01-31');
```

### SELECT

データを参照する．
```
SELECT [column_name], ... FROM [TABLE_NAME] WHERE [CONDITIONS];

ex)
全件検索
SELECT * FROM members;

SELECT name FROM members;

SELECT name FROM members WHERE name == 'jon';

```

### UPDATE
データを更新する．

```
UPDATE [TABLE_NAME] SET [column_name]=[VALUE1] WHERE [CONDITIONS];

ex)
UPDATE members SET name = 'mike', birth_day = '2011-11-30' WHERE id = 1;
```
### DELETE
データを削除する．

```
DELETE FROM [TABLE_NAME] WHERE [CONDITIONS];

ex)
DELETE FROM members WHERE id = 1;
```

## WHEREの書き方

### 演算子
| 記述 | 概要|
| ---- | ---- |
| = | 等価 |
| > | 右不等 |
| >= | 以上 |
| < | 左不等 |
| <= | 以下 |
| != | 不等価 |

### AND
条件を追加する．
```
SELECT * FROM users WHERE age >= 20 AND age <= 30;
```

### BETWEEN
A 以上，B 未満を条件とする．
```
SELECT * FROM users WHERE age BETWEEN 20 AND 30;
```

### LIKE
部分一致の条件
```
SELECT * FROM users WHERE mail_address LIKE "%[String]%";
```
### 日付の条件
```
SELECT * FROM orders WHERE created_at <= "2015-04-01 00:00:00";
```

### IN, NOT IN
- IN
条件に含まれているuserを取得する，
```
SELECT * FROM users WHERE id IN (1, 23, 445);
```

- NOT IN
条件に含まれないuserを取得する．
```
SELECT * FROM users WHERE id NOT IN (1, 23, 445);
```

## SORTの方法

### ORDER BY
