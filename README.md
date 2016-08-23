# Ghost blog run on Docker

## Why yet another container for Ghost
As known, there are many awesome Ghost docker images.For example:
1. [Ghost image from Docker library](https://github.com/docker-library/ghost)
2. [gold/ghost](https://hub.docker.com/r/gold/ghost/)
3. [ptimof/ghost](https://hub.docker.com/r/ptimof/ghost/)

Although above images have few point to improve.

For `1` above,
>The official container for Ghost is fine for running in development mode, but it has the `wrong
permissions` for running in production. That, and the config file doesn't have any easy way to tweak
it.                   --from https://hub.docker.com/r/ptimof/ghost/

For `2` and `3`, they neither support `SSL`.

## Usage
### Quickstart
```shell
docker run -d -P adolphlwq/docker-ghost
```
or:
```shell
docker run -d -p host_port:2368 adolphlwq/docker-ghost
```

### Customed Config
- download repo:
```
git clone
```
- change `config.js` for your own config
```
vim config.js
do sth
:wq
```
- rebuild docker image
```
docker build -t repo/image_name:tag .
```
- run your image

### Backup you blog database
I suggest you map a volumn from container to host when run ghost image.
```
docker run -d --name ghost -p 2368:2368 -v host_path_to_data:/opt/ghost/content/data ghost
```

## Let's Encrypt on Ubuntu Xneil
In this section,I will set up a SSL by `[Let's Encrypt](https://letsencrypt.org/)` and `[Nginx](http://nginx.org)`.

- Step 1: install Nginx and letsencrypt on Ubuntu 16.04
```
It is easy, I skip
```
- Step 2:Obtain SSL CA from `Let's Encript CA`
```
[sudo] letsencrypt certonly --webroot -w /var/www/ghost -d example.com -s www.example.com
```

## Reference
- [Ghost docs](https://ghost.org/developer/)
- [Docker docs](http://docs.docker.com/)

## TODOs
- [X] Support port mapping between Docker container and host
- [ ] Ghost Theme hacking
- [X] Support SSL via [Let's Encrypt](https://letsencrypt.org/)
- [ ] Support data volumn
- [ ] Support Google Analytics
