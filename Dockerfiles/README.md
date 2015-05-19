# Shared docker images for Hoist
these folders and files represent some shared docker files we use between applications at hoist

#Running via Docker

You're most likely running on OSX so there are a couple of requirements:

* install (https://docs.docker.com/installation/mac/)[boot2docker]
* install (https://docs.docker.com/compose/install/)[docker compose]

```
curl -L https://github.com/docker/compose/releases/download/1.2.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

in order to keep data around between boots we create a mapped volume, usually this would mean mapped to the host but if you're using boot2docker the docker images run inside a VM so the volume is actually on that VM


#Create the data folder in boot2docker
```
boot2docker up (or init then up)
boot2docker ssh
sudo mkdir -p /mnt/sda1/dev/data/db
exit
```

we can actually map this folder back to OS X if needed using sshfs (a user space remote file system)


* install sshfs
```
brew install Caskroom/cask/osxfuse
brew install sshfs

```
* create a mapped directory on the boot2docker vm
from (https://gist.github.com/sevastos/2fa4c86f01541351efe8)
```
mkdir -p ~/.hoist
mkdir -p ~/.hoist/test-data
sshfs docker@localhost:/mnt/sda1/dev ~/.hoist/test-data/ -p 2022
tcuser (is the password)
```

ok that should be all.

Now bring up the docker images by running

```
docker-compose --project-name Hoist up (or run ./start.sh)
```






