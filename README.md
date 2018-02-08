# APIリクエスト例外チェック

全てのURLに片っ端から例外が起こりそうな文字列を送り、500エラーが返ってきた場合は記録する。  
いつか gem 化したい。

# 使い方

最初に下記のことを行う。

- `urls.txt` を新規作成し、正常なパラメータ付きURLをテストしたい分だけ記述する
- `errors.txt` に自動で送りつけたい例外が起こりそうな文字列を記述する

`urls.txt` の例:

```
# GETリクエスト
GET:http://example.org/hoge?param1=1&param=2

# POSTリクエスト (getと同じ方式で記述する)
POST:http://example.org/fuga?param1=1
```

`errors.txt` の例:

```
# 絵文字
🍣🍕🍺
# 4バイト文字
𠀋𡈽𡌛𡑮𡢽𠮟𡚴𡸴𣇄𣗄
```

実行するには下記コマンドを叩く。

```
ruby main.rb
```

上記の設定の場合、下記のリクエストが自動で送られる。

```
http://example.org/hoge?param1=🍣🍕🍺&param=2
http://example.org/hoge?param1=𠀋𡈽𡌛𡑮𡢽𠮟𡚴𡸴𣇄𣗄&param=2
http://example.org/hoge?param1=1&param=🍣🍕🍺
http://example.org/hoge?param1=1&param=𠀋𡈽𡌛𡑮𡢽𠮟𡚴𡸴𣇄𣗄
http://example.org/fuga?param1=🍣🍕🍺
http://example.org/fuga?param1=𠀋𡈽𡌛𡑮𡢽𠮟𡚴𡸴𣇄𣗄
```

api_token等、固定したいパラメータがある場合は下記のように叩く。
(key1 と key2 のパラメータは固定される)

```
ruby main.rb param1 param2
```

実行すると `error.log` が生成され、500エラーが発生したリクエストが記録される。

以下、Google翻訳ぶっこみ。

Below, Google translation paste result.

# API request exception check

Send a character string that is likely to cause an exception from one end to all URLs and record it if 500 error comes back.

# How to use

First do the following.

- Create a new `urls.txt` and write as many URLs with normal parameters as you want to test
- Describe a string that is likely to cause an exception to be sent automatically to `errors.txt`

An example of `urls.txt`:

```
# GET request
GET: http://example.org/hoge?param1=1&param=2

# POST request (Write in the same way as get)
POST: http://example.org/fuga?param1=1
```

An example of `errors.txt`:

```
# Emoji
🍣🍕🍺
# 4 byte character
𠀋𡈽𡌛𡑮𡢽𠮟𡚴𡸴𣇄𣗄
```

To execute, hit the following command.

```
ruby main.rb
```

In the case of the above setting, the following request is automatically sent.

```
http://example.org/hoge?param1=🍣🍕🍺&param=2
http://example.org/hoge?param1=𠀋𡈽𡌛𡑮𡢽𠮟𡚴𡸴𣇄𣗄&param=2
http://example.org/hoge?param1=1&param=🍣🍕🍺
http://example.org/hoge?param1=1&param=𠀋𡈽𡌛𡑮𡢽𠮟𡚴𡸴𣇄𣗄
http://example.org/fuga?param1=🍣🍕🍺
http://example.org/fuga?param1=𠀋𡈽𡌛𡑮𡢽𠮟𡚴𡸴𣇄𣗄
```

api_token etc. If you have parameters you want to fix, hit as shown below.
(Parameters of key 1 and key 2 are fixed)

```
ruby main.rb param1 param2
```

When it is executed, `error.log` is generated and the request with 500 error is recorded.
