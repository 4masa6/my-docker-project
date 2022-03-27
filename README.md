## 概要

Docker環境構築
PHP8・Laravel8・Nginx・MySQL・PhpMyAdmin


## 手順
### 準備

```bash
# プロジェクトをダウンロード
git clone

cd my-docker-project

# .envをコピー
cp .env.example .env
```

### ./.env修正
```bash:./.env
DB_NAME=db_name # 適宜修正
DB_USER=db_user # 適宜修正
DB_PASSWORD=db_password # 適宜修正
DB_ROOT_PASSWORD=password # 適宜修正
```

### プロジェクトの立ち上げ

```bash
# ビルド
docker-compose build

# コンテナ起動
docker-compose up -d

# コンテナに入る
docker-compose exec app bash

# Laravelプロジェクト作成
composer create-project --prefer-dist laravel/laravel . "8.*"
```

### ./src/.env修正
```bash:./src/.env
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=db_name # ./.envに合わせる
DB_USERNAME=root # ./.envに合わせる
DB_PASSWORD=password # ./.envに合わせる

/public/css/app.css # 追記
/public/js/app.js # 追記
```

### appコンテナに入り、マイグレーションを実行
```bash
docker-compose exec app bash
php artisan migrate
```

### LaravelBreezeのインストール

```bash
docker-compose exec php /bin/bash
cd src
composer require laravel/breeze "1.*" --dev
php artisan breeze:install
npm install && npm run dev
```

- URL
`http://127.0.0.1:80`

- ## phpMyAdminに接続
`http://127.0.0.1:8086`