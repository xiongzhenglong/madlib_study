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