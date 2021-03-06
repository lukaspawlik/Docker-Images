# 10up Docker Library

The Dockerfiles in this repository can be used to compile Docker images intended to be used as PHP upstreams for WordPress sites.

## Nginx

## PHP
### What's Included

PHP-FPM at:

- 5.3.29
- 5.4.45
- 5.5.34
- 5.6.20
- 7.0.5

### How to use it

First, run a container:

```sh
docker run -d -v /var/www:/var/www --net=host --name php7 10up/php:7.0-fpm
```

Then, set your PHP upstreams in Nginx to point to the container. For clarity, each container listens on a different port:

- 5.3 => 9053
- 5.4 => 9054
- 5.5 => 9055
- 5.6 => 9056
- 7.0 => 9070

The `--host=net` directive above will map all host ports into the container, so if PHP is running globally on port 9000, the containers won't conflict.

In addition, this means the PHP process in each container can communicate with Memcached (port 11211) and MySQL (port 3306) on the Docker host as well.
 
Each container will attempt to install the Pecl extensions for caching backends:
- Redis
- Memcached
- Memcache
- APCu

(Unless they are unsupported. APCu is PHP7 only. Redis and Memcached are not yet PHP7-compatible.)

### What's Next

Minify the containers
- Each container image is ~180MB. We should make sure this is as small as it can be.

## License

10up's Docker Library is free software; you can redistribute it and/or modify it under the terms of the [GNU General
Public License](http://www.gnu.org/licenses/gpl-2.0.html) as published by the Free Software Foundation; either version
2 of the License, or (at your option) any later version.