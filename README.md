# Install
# Debian Install

```sh
## Debian reqs
sudo apt-get update -y;
sudo apt-get upgrade -y;

## ruby build reqs
sudo apt-get install -y git autoconf patch build-essential rustc libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libgmp-dev libncurses5-dev libffi-dev libgdbm6 libgdbm-dev libdb-dev uuid-dev libpq-dev curl;

## Goto: Item R
```

### Alt, Rocky Linux Install

```sh
dnf install -y autoconf gcc patch bzip2 openssl-devel libffi-devel readline zlib-devel gdbm ncurses-devel tar perl-FindBin

dnf --enablerepo=crb install libyaml-devel
## Goto: Item R
```

## Install Rust

```sh
## Item: R
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --profile minimal --default-toolchain stable-x86_64-unknown-linux-gnu;
. "$HOME/.cargo/env";
## Goto Item: 2
```

# Rbenv Install

```sh
## Item: 2
git clone https://github.com/rbenv/rbenv.git ~/.rbenv;
~/.rbenv/bin/rbenv init;
cd $HOME;

## Add to the bottom of bashrc
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
. ./.bashrc;

git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build;

## Goto Item: Setup
```

## Installing Ruby

```sh
## Item: Setup
	RUBY_CONFIGURE_OPTS="--enable-yjit" rbenv install 3.3.5;
	rbenv global 3.3.5;
	ruby -v --yjit;
```

### Sources - Notes

- adding --with-jemalloc to RUBY_CONFIGURE_OPTS, might result in better memory usage
- https://dev.to/wizardhealth/install-ruby-320-with-yjit-3mmo

# Installing Node & Yarn
## Installing Node
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
nvm install node # install latest node
```

```sh
npm install --global yarn
```

## Project setup
```sh
yarn install;
yarn build;
bundle install;
```

## Postgres Setup
```sh
sudo apt update -y && sudo apt install -y postgresql postgresql-contrib;

sudo apt update -y && sudo apt install -y postgresql postgresql-contrib && sudo service postgresql start && 
sudo -u postgres psql -c "CREATE USER sayit_db_user WITH PASSWORD 'sayit';"
sudo -u postgres psql -c "ALTER USER sayit_db_user CREATEDB;"

## Change 'local local password' -> 'trust'
sudo nano /etc/postgresql/15/main/pg_hba.conf
## In project dir
rails db:create
rails db:migrate
rails db:seed
```
