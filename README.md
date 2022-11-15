
# Docker環境の破棄
コンテナの停止、ネットワーク・名前付きボリューム・コンテナイメージ、未定義コンテナを削除
docker compose down --rmi all --volumes --remove-orphans

git clone

cd docker-laravel-handson

docker compose up -d

git cloneが終わった状態では app コンテナ内に /data/vendor ディレクトリが存在しない.
→
docker compose exec app bash
chmod -R 777 storage bootstrap/cache
composer install
(composer create-project 時は .env は作成されますが、 composer install 時は .env ファイルは作成されません。)

ログファイルを見てエラーを確認
→
cat storage/logs/laravel.log
[YYYY-MM-DD HH:II:SS] 環境.ログレベル: ログメッセージ　　トレースログ
[2022-11-15 13:29:39] production.ERROR: No application encryption key has been specified. {"exception":"[object] (Illuminate\\Encryption\\MissingAppKeyException(code: 0): No application encryption key has been specified. at /data/vendor/laravel/framework/src/Illuminate/Encryption/EncryptionServiceProvider.php:79)

.env.example はありますが、 .env ファイルが存在しない
理由は .env はGit管理対象外に設定されている。

.env ファイルがないのが問題なので、.env.example を元にコピーして作成します。
cp .env.example .env

エラーメッセージはログと同じく .env に APP_KEY= の値がないと出ています。
アプリケーションキーはこのコマンドで生成できます。

php artisan key:generate
→Application key set successfully.

php artisan storage:link
php artisan migrate

exit
docker compose down

参考サイト
https://qiita.com/ucan-lab/items/56c9dc3cf2e6762672f4





