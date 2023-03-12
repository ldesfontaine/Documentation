# Laravel documentation install guide (for debian)

## Clone your project
```
git clone
```

## Install php
```
sudo apt install php7.2 php7.2-fpm php7.2-mysql php7.2-xml php7.2-mbstring php7.2-curl php7.2-zip php7.2-gd php7.2-bcmath
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