# Install MongoDB on WSL

The normal instructions for linux do not work for WSL so here is what I did to get the installation to work.

1) Install Mongo
```
sudo apt-get install mongodb
```

2) Start Mongo Server
```
sudo service mongodb start
```

3) Connect to Mongo Shell
```
mongo
```
