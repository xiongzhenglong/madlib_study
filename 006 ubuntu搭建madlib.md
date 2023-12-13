sudo adduser postgres
sudo usermod -aG sudo postgres
su - postgres
sudo ls /root
sudo reboot

sudo apt-get update
sudo apt-get install -y cmake g++ m4 python3-pip python3-dev libboost-dev libboost-system-dev libboost-thread-dev git  build-essential 

sudo apt update
sudo apt install gnupg
wget -qO - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list
sudo apt-get update
sudo apt-get install postgresql-15 postgresql-contrib-15 postgresql-server-dev-15 postgresql-plpython3-15  

sudo -u postgres psql
ALTER USER postgres PASSWORD '1qazZAQ!';
\q
psql --version

nano /etc/postgresql/15/main/pg_hba.conf
    local   all             postgres                                md5
    host    all             all             0.0.0.0/0               md5

nano /etc/postgresql/15/main/postgresql.conf
    listen_addresses = '*'          # what IP address(es) to listen on;

sudo systemctl restart postgresql

psql -U postgres

sudo apt-get update
cd ~
git clone https://github.com/apache/madlib.git
cd madlib
 git checkout madlib2-master # 或选择一个特定版本  非常关键
./configure
sudo make
sudo make install
psql -U postgres
CREATE DATABASE madlib_db;
\q

export PATH=$PATH:~/madlib/build/src/bin
export PATH=$PATH:/usr/lib/postgresql/15/bin

madpack install -s madlib -p postgres -c postgres@localhost/madlib_db
psql -U postgres -d madlib_db -c "SELECT madlib.version();"

sudo apt-get update
sudo apt-get install ufw
sudo ufw enable
sudo ufw allow 5432/tcp
sudo ufw status
sudo ufw allow from 180.164.88.173 to any port 5432



