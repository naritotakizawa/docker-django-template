# docker-django-template

Django を使ったアプリケーションの、Docker での開発用テンプレートです。このリポジトリをクローンやフォークし、設定を書き換えたり、機能やアプリケーションを加えたりして開発を進めていくと捗るかもしれません。

```
git clone https://github.com/naritotakizawa/docker-django-template
cd docker-django-template
```

データベースは PostgreSQL、Web サーバーとして Nginx、Nginx の背後に Django+Gunicorn が動作しています。
backend 以下に Django プロジェクトがあります。

## 入っている Django アプリケーションについて

必要がなければ消したり、新しく追加してください。

### register

自作のアプリケーション。カスタムユーザーモデルを定義しています。今のところ追加のフィールド等は何もありませんが、ユーザーモデルを拡張したい場合に備え、あらかじめ定義しています。

## 動かしてみる

### 開発環境

Django は`manage.py runserver`で動作させているので、エラーなどを確認できますし、ホットリロードも反映されます。

次のコマンドで起動できます。

```
docker-compose -f docker-compose.yml -f dev.yml build
docker-compose -f docker-compose.yml -f dev.yml up
```

標準の動作では、admin admin123 でスーパーユーザーが作成されます。書き換えたい場合は、dev.yml や prod.yml の`SUPERUSER_NAME`、`SUPERUSER_PASSWORD`を書き換えてください。

ページの表示は`http://127.0.0.1`で行えます(:8000 などは不要)。

### 本番環境

Django は`gunicorn ...`で動作させています。

prod.yml を編集します。

```
nano prod.yml
```

ALLOWED_HOSTS の部分を書き換えます。

```
ALLOWED_HOSTS=127.0.0.1
↓
ALLOWED_HOSTS=サーバーのIP、又はドメイン
```

あとは単純に起動できます。

```
docker-compose -f docker-compose.yml -f prod.yml build
docker-compose -f docker-compose.yml -f prod.yml up
```

ページの表示は`http://IPかドメイン`で行えます(:8000 などは不要)。
