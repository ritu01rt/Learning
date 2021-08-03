https://docs.microsoft.com/en-gb/windows/dev-environment/javascript/nodejs-on-wsl 

nvm use --lts to switch to the LTS version (recommended since more stable) by going into your project directory


https://stackoverflow.com/questions/62495999/installing-mongodb-in-wsl workaround for installing mogodb on wsl2
For installing mongodb community edition, I have added the commands below:

wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
sudo apt-get install gnupg
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list

sudo apt-get update
sudo apt-get install -y mongodb-org
Now, to get mongoDB running,

sudo nano /etc/init.d/mongod
and paste the contents in this link into the file and save it.

#give permissions
sudo chmod +x /etc/init.d/mongod

#start the service
sudo service mongod start
Now, you can run mongo to reach the database.
