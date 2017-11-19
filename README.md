[![Travis](https://img.shields.io/travis/rakshans1/docker-wordpress.svg)](https://travis-ci.org/rakshans1/docker-wordpress)
[![Pulls](https://img.shields.io/docker/pulls/rakshans1/wordpress.svg)]()
[![Layers](https://img.shields.io/imagelayers/layers/rakshans1/wordpress/latest.svg)]()
[![Size](https://img.shields.io/imagelayers/image-size/rakshans1/wordpress/latest.svg)]()


![rakshans1/wordpress](/icon.png?raw=true)
# wordpress 8.9.1
### Based on the [official WordPress](https://hub.docker.com/_/wordpress/) image this image fully automates your WordPress installation with the help of [wp-cli](http://wp-cli.org/).
----
## Run the image
```bash
# Start a MySQL container first
docker run -d -e MYSQL_ROOT_PASSWORD=12345678 --name mysql mysql

# Start the WordPress container with 2 plugins and the 'responsive' theme
docker run -d -p 8080:80 \
           -e SITE_URL=http://yoursite.com \
           -e WORDPRESS_PLUGINS="jetpack;wordfence" \
           -e WORDPRESS_ACTIVE_THEME=responsive \
           -e WORDPRESS_THEMES="responsive" \
           --link mysql:mysql rakshans1/wordpress:latest
```

## Use as base image
This image is optimized to be used as a base image. You can simply override all ENVs in you own Dockerfile to make your own tailored image.
```Dockerfile
FROM rakshans1/wordpress:latest

# e.g. copy your own theme or plugins
# this is quite awesome for CI solutions with continuous deployment in mind
COPY ./ /usr/src/wordpress/wp-content/themes/my-theme/

# you can simply override all the ENVs from the configuration chapter
ENV WORDPRESS_PLUGINS "password-protected;wordfence"
ENV WORDPRESS_ACTIVE_THEME "my-theme"
```

## Configuration
- `SITE_URL` (defaults to `https://example.com`)
- `SITE_TITLE` (defaults to "DockerPress")
- `WORDPRESS_PLUGINS` (defaults to `"hello-dolly"`): Semicolon-separated list of plugins to install and activate
  + e.g. `WORDPRESS_PLUGINS="wordfence;jetpack;hello-dolly"`
- `WORDPRESS_THEMES` (defaults to `"twentysixteen;twentyfifteen"`): Semicolon-separated list of themes to install
- `WORDPRESS_ACTIVE_THEME` (defaults to `twentysixteen`): This theme gets activated on initialization
- `ADMIN_USER` (defaults to `admin`)
- `ADMIN_EMAIL` (defaults to `changeme@example.com`)
- `ADMIN_PASSWORD` (defaults to `12345678`)