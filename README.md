# Rawkode's Symfony2 Distribution

A Symfony2 distribution with a Linux like directory structure, Xml configuration and Docker readyness!

## How do I use it?

### Docker

First, you'll need to have the following installed:

* docker
* docker-compose
* docker-machine or boot2docker (Mac & Windows)

#### Warning

When you're on a Mac or Windows, docker-machine and boot2docker mount your $HOME directory to the virtual machine. This isn't very performant!

To speed things up, I've setup the Docker containers in a fashion that the cache and log directories are not mounted locally - but this only helps so much.

The ideal situation is to stop this mounting (I've subbmitted a pull-request https://github.com/docker/machine/pull/1622) and handle the syncing of directories yourself through rsync or nfs.

I use something like this:

```
watch -n1 rsync --exclude '.git' --exclude 'var/cache/*' --exclude 'var/log/*' -rlptDv ./ docker@$(docker-machine ip development 2>/dev/null):`pwd`
```

You want to replicate the entire local path on the virtual machine, to make the setup as seemless as possible.

### Run It!

```docker-compose up```

It is configured to run an nginx web server on port 10000 - you'll be able to access this through http://localhost:10000 or http://(docker-machine ip | boot2docker ip):10000
