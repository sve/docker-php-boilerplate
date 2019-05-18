## PHP Application Boilerplate

### Features
- Used docker [multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/)
- Based on alpine images
- Pulls images from Docker Hub
- [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) used as [zsh](https://www.zsh.org/) configurator

### Installation
##### Pull images from GitHub Docker Registry
```
docker-compose pull
```
##### Start services
```
docker-compose up -d
```

### Usage
##### SSH into container
```
docker-compose exec php zsh
```

##### Start a Laravel Application
```
laravel new
```
##### ...or start a Symfony Application
```
composer create-project symfony/skeleton tmp/ && cp -r tmp/** . && rm -rf tmp/
```

[![CircleCI](https://circleci.com/gh/sve/docker-php-boilerplate/tree/master.svg?style=svg&circle-token=c057f8fcf375f25aa2340430957f0c420451be83)](https://circleci.com/gh/sve/docker-php-boilerplate/tree/master)
