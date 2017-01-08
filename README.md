# Joomla CMS Bootstrap

## What Is It?
Joomla-cms-package is a [Composer](https://getcomposer.org/) meta-package that loads a customizable [Joomla](https://github.com/joomla/joomla-cms) repository. Set things up in less than 5 minutes! Never start a project without version control again ;)

##### No Installed Components / Modules / Plugins
Joomla extensions often come with a post-install configuration script which leads me to stick
to manual installation routines. No bundled extension so far!


## Quick Start - How To Use It?
Bootstrapping a new Joomla install…

### 1 - Install Composer *(or skip to step 2…)*
##### Linux Debian/Raspbian
When using **Raspbian / Debian**, install Composer if it's not yet available on your system.
* First, check for an existing debian package for Composer (composer.deb ?) and use `apt-get` if you find one.
* If no debian package is available (which is the case at the time of writing these lines),
	use the shell commands provided in the following gist.

        cd /usr/src
        sudo apt-get install curl php5-cli
        curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer

  @see: http://www.bravo-kernel.com/2014/08/how-to-install-composer-on-debian/

##### OSX / Linux / WINDOWS
* Official documentation: [How to install Composer on **OSX** / **Linux** / **Unix**](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx)
* Official documentation: [How to install Composer on **Windows**](https://getcomposer.org/doc/00-intro.md#installation-windows)


### 2 - Prepare Mysql
* Create new SQL **database and db user/password**.
* Save all info for later use.
* If you're not using *PhpMyAdmin*, you can use a CLI. Run the following SQL commands (after launching the mysql prompt):


  	    CREATE DATABASE joomla;
	    CREATE USER joomuser;
	    SET PASSWORD FOR joomuser= PASSWORD(“1234”);
	    GRANT ALL PRIVILEGES ON joomla.* TO joomuser IDENTIFIED BY ‘1234’;
	    FLUSH TABLES;


### 3 - `create-project`: Install the Composer Package
* `cd` into the web server's public DocumentRoot folder
* `git clone https://github.com/LianzaG/joomla-cms-package.git`
* Change folder name to the desired project's name (e.g: www.example.dev)
* `cd www.example.dev/`
* `git checkout x.x.x-joomla-cms-package' to get to the desired package version branch.
* Run `composer create-project` to install dependencies **and** to allow the post-install scripts to run afterwards.


### 4 - Moving Joomla back to the root folder manually
* This section's instruction are pertinent if you used `composer install` instead of `composer create-project`when initializing the package.
* In such a case, the post-install scripts won't be triggered and you'll need to launch them manually, using the command below.
* Simply execute `composer run relocate_joomla`.


### 5 - Install Joomla
At this point, you're ready to use the Joomla installation script. It will load by itself when you'll browse to your
site's admin backend ('www.example.dev/administrator/').


### 6 - Check Folders/Files Permissions
If you're using **RaspberryPi Server**, you may have to make WP files/folders writable:
* `chown -R www-data:www-data exampleProjectFolder/`
* OR set-up FTP server and user account to be used by WP

> *Whatever your server setup may be, always make sure that all files are chmod:644 and folders are chmod:755.*
