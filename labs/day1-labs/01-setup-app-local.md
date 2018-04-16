# Initial Setup and Running App on Local Machine

## Clone Lab Github Repo

Once you have accessed the VM, you must clone the workshop repo to the machine.

ssh bran@52.173.82.18

1. Start with a terminal on the VM
2. Clone the Github repo via the command line

    ```
    git clone https://github.com/branstraub/aks-workshop.git
    ```

## Get Applications up and running

### Database layer - MongoDB

The underlying data store for the app is [MongoDB](https://www.mongodb.com/ "MongoDB Homepage"). It is already running. We need to import the data for our application.

1. Create a folder: 
```
sudo mkdir -p /data/db
````

2. Set rwx mode to it: 
```
cd /data/db
sudo chmod -R 777 .
```

3. Start MongoDB:
```
sudo service mongod start
```

4. Import the data using a terminal session on the VM
```bash
cd ~/aks-workshop/app/db

mongoimport --host localhost:27017 --db webratings --collection heroes --file ./heroes.json --jsonArray && mongoimport --host localhost:27017 --db webratings --collection ratings --file ./ratings.json --jsonArray && mongoimport --host localhost:27017 --db webratings --collection sites --file ./sites.json --jsonArray
```

### API Application layer - Node.js

The API for the app is written in javascript, running on [Node.js](https://nodejs.org/en/ "Node.js Homepage") and [Express](http://expressjs.com/ "Express Homepage")

1. Update dependencies and run app via node in a terminal session on the VM

```bash
curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
sudo apt-get install -y nodejs

cd ~/aks-workshop/app/api

npm install 
npm run localmachine
```

2. Open a new terminal session on the VM and test the API


```bash
curl http://localhost:3000/api/heroes
```

### Web Application layer - Vue.js, Node.js

The web frontend for the app is written in [Vue.js](https://vuejs.org/Vue "Vue.js Homepage"), running on [Node.js](https://nodejs.org/en/ "Node.js Homepage") with [Webpack](https://webpack.js.org/ "Webpack Homepage")

1. Open a new terminal session on the VM
2. Update dependencies and run app via node

    ```bash
    cd ~/aks-workshop/app/web
    
    npm install && npm run localmachine
    ```
3. Test the web front-end

    The VM has the 8080 port open. You can browse your running app with a link such as: http://50.50.50.50:8080 

    You can also test from a new terminal session in the jumpbox
    ```bash
    curl http://localhost:8080
    ```

## Clean-up

Close the web and api apps in the terminal windows by hitting `ctrl-c` in each of the corresponding terminal windows
