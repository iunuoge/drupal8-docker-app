drupal8-docker-app
=============

This repo contains a recipe for making a [Docker](http://docker.io) container for Drupal8, using Linux, Apache, MySQL and Memcache. 
To build, make sure you have Docker [installed](http://www.docker.io/gettingstarted/).

#Instructions:

```
## 1 - Install docker and create the image:
```
curl get.docker.io | sudo sh -x
sudo docker build -t ricardo/drupal8 https://github.com/ricardoamaro/drupal8-docker-app.git
```
this can take a while but should eventually return a command prompt. It's done when it says "Successfully built {hash}"

## 2 - Run the container, connecting port 80:
```
sudo docker run -i -t -p 80:80 <yourname>/drupal8
```
That's it!
## 3 - Visit http://localhost/ in your webrowser. 

### Credentials:
* Drupal account-name=admin & account-pass=admin *
* ROOT   MYSQL_PASSWORD will be on /mysql-root-pw.txt
* DRUPAL MYSQL_PASSWORD will be on /drupal-db-pw.txt


## You can also clone this repo somewhere, 
```
git clone https://github.com/ricardoamaro/drupal8-docker-app.git
cd drupal8-docker-app
```
and then build it with:
```
sudo docker build -t <yourname>/drupal8 .
```

Note1: you cannot have port 80 already used or the container will not start.
In that case you can start by setting: `-p 8080:80`

Note2: To run the container in the background
```
sudo docker run -d -t -p 80:80 <yourname>/drupal8
```

build directly from github is broken at the moment:
```
sudo docker build -t <yourname>/drupal8 git://github.com/ricardoamaro/docker-drupal.git
```

## More docker awesomeness

This will create an ID that you can start/stop/commit changes:
```
# sudo docker ps
ID                  IMAGE                   COMMAND               CREATED             STATUS              PORTS
538114c20d36        <yourname>/drupal8:latest   /bin/bash /start.sh   3 minutes ago       Up 6 seconds        80->80  
```

Start/Stop
```
sudo docker stop 538114c20d36
sudo docker start 538114c20d36
```

Commit the actual state to the image
```
sudo docker commit 538114c20d36 <yourname>/drupal8
```

Starting again with the commited changes
```
sudo docker run -d -t -p 80:80 <yourname>/drupal8 /start.sh
```

Shipping the container image elsewhere 
```
sudo docker push  <yourname>/drupal8
```

You can find more images using the [Docker Index][docker_index].

ricardoamaro/drupal-lamp

### Clean up
While i am developing i use this to rm all old instances
```
sudo docker ps -a | awk '{print $1}' | grep -v CONTAINER | xargs -n1 -I {} docker rm {}
``` 

### Known Issues
* Warning: This is still in development and ports shouldn't be open to the outside world.


## Contributing
Feel free to fork and contribute to this code. :)

1. Fork the repo
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## Authors

Created and maintained by [Ricardo Amaro][author] 
https://blog.ricardoamaro.com

## License
GPL v3

[author]:                 https://github.com/ricardoamaro
[docker_upstart_issue]:   https://github.com/dotcloud/docker/issues/223
[docker_index]:           https://index.docker.io/

