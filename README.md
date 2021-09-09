# Install Wordpress Requirements

When using the Sage way for developing Wordpress projects, there's a few requirements when setting up your local development environment. 

*   **[PHP](https://www.php.net/)**
*   **[Mysql](https://www.mysql.com/)**
*   **Webserver** (apache / nginx)
*   **[Node](https://nodejs.org/en/)** version >= 12.18
    (when using nvm check with nvm list to show current version, execute nvm use stable to switch to stable version, currently v15)
*   **Yarn**
*   **[Composer](https://getcomposer.org/)**
*   **[Wp cli](https://make.wordpress.org/cli/handbook/guides/installing/)**
*   **[Git](https://git-scm.com/)**

Here's an example of how to install all requirements on Mac OS. It uses **[homebrew](https://brew.sh/)** to install most of the required software, **[nvm](https://github.com/nvm-sh/nvm)** to manage node versions, and laravel **[valet](https://laravel.com/docs/8.x/valet)** as webserver.

```sh
# install command line tools (including git)
xcode-select --install

# configure git global user
git config --global user.name <your-git-username>
git config --global user.email <your-git-email>

# install homebrew
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# php + mysql
brew install php
brew install mysql
brew services start mysql
mysql --user='root' --execute='FLUSH PRIVILEGES;'
$(brew --prefix mysql)/bin/mysqladmin -u <your-mysql-username> password <your-mysql-password>

# composer
brew install composer
if ! grep -q 'PATH="~/.composer/vendor/bin:$PATH"' ~/.bash_profile ; then
  echo 'export PATH="~/.composer/vendor/bin:$PATH"' >> ~/.bash_profile
  source ~/.bash_profile
fi

# wp-cli
brew install wp-cli

# laravel valet
composer global require laravel/valet
valet install
valet start
valet domain localhost # optional, default domain extension is 'test'

# node version manager
brew install nvm
mkdir ~/.nvm
if ! grep -q 'NVM_DIR=~/.nvm' ~/.bash_profile ; then
  echo 'export NVM_DIR=~/.nvm' >> ~/.bash_profile
  source ~/.bash_profile
fi
if ! grep -q 'source $(brew --prefix nvm)/nvm.sh' ~/.bash_profile ; then
echo 'source $(brew --prefix nvm)/nvm.sh' >> ~/.bash_profile
  source ~/.bash_profile
fi
nvm install # install latest node
nvm install --lts # install and load latest stable node

# yarn
brew install yarn
```
