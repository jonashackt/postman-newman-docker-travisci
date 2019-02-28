# postman-newman-docker-travisci
[![Build Status](https://travis-ci.org/jonashackt/postman-newman-docker-travisci.svg?branch=master)](https://travis-ci.org/jonashackt/postman-newman-docker-travisci)

Example project showing how to execute Postman collections with Docker triggered by TravisCI

## Run Postman as Newmen inside a Docker Container and execute a test

Execute the provided Postman collection https://www.getpostman.com/collections/8a0c9bc08f062d12dcda with Newman inside a Docker container:

```
docker run -t postman/newman run "https://www.getpostman.com/collections/8a0c9bc08f062d12dcda"
```

## Execute on TravisCI

Create a `.travis.yml` with the following 

```yaml
services:
- docker

script:
- docker run -t postman/newman run "https://www.getpostman.com/collections/8a0c9bc08f062d12dcda"
```

and configure TravisCI on your repository.


# Links

https://hub.docker.com/r/postman/newman

https://learning.getpostman.com/docs/postman/collection_runs/newman_with_docker/