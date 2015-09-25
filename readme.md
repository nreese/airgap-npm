==airgap-npm
Some of us are forced to work on airgapped systems (no internet connection).
This makes working with package management systems a real pain. This project contains everything needed to setup an NPM repo on a airgapped system. 

==Setup
Follow all setup instructions on machine with internet connection.

===Install Sinopia
Sinopia, https://github.com/rlidwka/sinopia, is an excellent NPM repo and the basis for this solution. 

Sinopia install instructions suggest a global install. This project requires something more self contained. As such, follow the instructions below to install sinopia into a folder that can easily be compressed and tranfered with physical media.

```
//airgap-npm/sinpoia directory
npm install
```

===Load dependencies
* Start sinopia

```
//airgap-npm/sinpoia directory
./start.sh
```

* Configure NPM to use sinopia

```
npm set registry http://localhost:4873
```

* Load required global packages into sinopia. Below is an example for Gulp

```
sudo npm install gulp --global
```

* Load required local packages into sinopia. Update dependencyProject/package.json with all dependencies needed on air gapped system.

```
//airgap-npm/dependencyProject directory or any directory containing package.json
npm install
```


==Test it
There is nothing worse than bringing in a new repo only find that a dependency is missing. Test your repo to insure you can do a clean build without internet access. 
* turn off wifi
* delete local npm cache
```
cd ~
rm -rf .npm/*
```

* delete global npm cache. Below is an example for Gulp

```
sudo npm uninstall gulp --global
```

* Configure sinpoia to only serve packages from storage. Update `sinopia/config.yaml`, commenting out the lines and restart sinopia

```
uplinks:
  npmjs:
    url: https://registry.npmjs.org/
```

* Load global and local npm packages.


==SneakerNet
* Compress the sinopia directory and export to physical media. Transfer physical media to airgapped network.
* Uncompress and start sinopia
* Configure NPM to use sinopia

```
npm set registry http://npmhost:4873
```

* Run npm installs on airgapped network just like you would on a network with internet connectivity.
