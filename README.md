# How to deploy Laravel applications on a server
The simple guide to deploy Laravel and Lumen application on a server
### 1. Create a new directory to store all the code.
Create a new directory to store all the code, name it `projects` or whatever you want to.
```bash
$ mkdir projects
$ cd projects
```
### 2. Git command to grab the code
If alright, from here, just issue a git command to grab the code.
```bash
$ git clone http://[GIT_SERVER]/project-name.git
$ cd project-name
```
### 3. Make the project-name/public directory to map with www directory
Next step is to make the project-name/public directory to map with www directory, symbol link is a great help for this, but we need to backup public directory first.
```bash
$ mv public public_bak
$ ln -s ~/www public
$ cp -a public_bak/* public/
$ cp public_bak/.htaccess public/
```

### 4. Update `~/www/index.php` file

```bash
require __DIR__.'/../projects/project-name/bootstrap/autoload.php';

$app = require_once __DIR__.'/../projects/project-name/bootstrap/app.php';
```

### 5. Allow write permission to `storage` directory and `bootstrap/cache`

```bash
$ chmod -R o+w storage
$ chmod -R o+w bootstrap/cache
```

### 6. Edit your `.env`
```bash
$ cp .env.example .env
```

### 7. update the required packages for Laravel project using composer and add some necessary caches

```bash
$ php composer install
$ php composer dumpautoload -o
$ php artisan key:generate
$ php artisan migrate
$ php artisan db:seed
$ php artisan config:cache
$ php artisan route:cache
```

## FAQs

### Get composer

```bash
$ wget https://getcomposer.org/composer.phar

or

$ curl -sS https://getcomposer.org/installer | php — –filename=composer
```
