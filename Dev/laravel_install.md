# Laravel documentation install guide (for debian)

## Clone your project
```
git clone
```

## Install PHP 8.0
Avec un accès root
```
apt update && apt install -y wget gnupg2 lsb-release
wget https://packages.sury.org/php/apt.gpg && apt-key add apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list
apt update && apt install -y php8.1
php -v
```

## Install php extensions
```
sudo apt install php8.0-mysql php8.0-xml php8.0-mbstring php8.0-zip php8.0-curl php8.0-gd php8.0-bcmath php8.0-intl php8.0-imagick php8.0-redis php8.0-soap php8.0-xmlrpc php8.0-xsl php8.0-zip
```

## Install composer
```
sudo apt install composer
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
