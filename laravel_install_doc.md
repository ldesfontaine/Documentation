# Laravel documentation install guide (for debian)

## Clone your project
```
git clone
```

## Install php
```
sudo apt install php7.2 
```

## Install composer
```
composer install --no-dev
```

## Install npm
```
npm install
```

## Set up your .env file
```
cp .env.example .env
```

## Generate your app key
```
php artisan key:generate
```

## Set up your database
```
php artisan migrate
```
Do for each DatabaseSeeder.php file in your database/seeds folder
```
php artisan db:seed --class=DatabaseSeeder
```
