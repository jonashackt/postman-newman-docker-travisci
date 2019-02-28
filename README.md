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


## Use our own Postman collection

You can find an example Postman collection at the root of this project in [httpbin-example.json.postman_collection](collections/httpbin-example.json.postman_collection), which will use the REST API of http://httpbin.org for testing (same as the downloaded above).

Now how could we "inject" this "custom" collection into the CI process? Therefore let's have a look into __Running local collection files__ at https://hub.docker.com/r/postman/newman:

> The docker image is designed to pick files from the /etc/newman directory within the image

So we need to mount the `collections` directory into `etc/newman` in our Docker container. Try to run it locally with:

```
docker run -v `pwd`/collections:/etc/newman -t postman/newman run httpbin-example.json.postman_collection
```

Adding this to our [.travis.yml](.travis.yml) does the same on our CI server.


# Links

https://hub.docker.com/r/postman/newman

https://learning.getpostman.com/docs/postman/collection_runs/newman_with_docker/