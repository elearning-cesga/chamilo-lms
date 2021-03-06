## Chamilo 2.x Installation

This installation guide is for development environments only.

### Install PHP, a web server and MySQL/MariaDB

To run Chamilo, you will need at least a web server (we recommend Apache2 for commodity reasons), 
a database server (we recommend MariaDB but will explain MySQL for commodity reasons) and a PHP interpreter (and a series of libraries for it). If you are working on a Debian-based system (Debian, Ubuntu, Mint, etc), just
type
```
sudo apt-get install libapache2-mod-php mysql-server php5-gd php5-intl php5-curl php5-json
```

### Install Git

The development version 2.x requires you to have Git installed. 
If you are working on a Debian-based system (Debian, Ubuntu, Mint, etc), just type
```
sudo apt-get install git
```

### Install Composer

To run the development version 2.x, you need Composer, a libraries dependency management system that will update all the 
libraries you need for Chamilo to the latest available version.

Make sure you have Composer installed. If you do, you should be able to launch "composer" on the command line and have the 
inline help of composer show a few subcommands. 
If you don't, please follow the installation guide at https://getcomposer.org/download/

### Download Chamilo from GitHub

Clone the repository

```
sudo mkdir chamilo2
sudo chown -R `whoami` chamilo2
git clone -b master --single-branch https://github.com/chamilo/chamilo-lms.git chamilo2
```

Checkout branch 2.x

```
cd chamilo2
git checkout --track origin/master
git config --global push.default current
```

### Create database

You should have a MariaDB/MySQL user and database created before hand.

### Update dependencies using Composer

From the Chamilo folder (in which you should be now if you followed the previous steps), launch:

```
composer update
```

Composer update will ask for the database credentials in order to create a configuration file in:

```
app/config/parameters.yml.dist
```

If you face issues related to missing CSS/JS files, you might need to ensure
that your web/assets folder is completely re-generated.
Use this set of commands to do that:
```
rm composer.lock
rm -rf vendor/
composer clear-cache
composer update
```
This will take several minutes in the best case scenario, but should definitely
generate the missing files.

### Change permissions

On a Debian-based system, launch:
```
sudo chown -R www-data:www-data app main/default_course_document/images main/lang  
```

### Start the installer

In your browser, load the "web/install.php" URL and follow the installation instructions.

