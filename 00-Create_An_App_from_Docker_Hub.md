# Create an image from source and deploy it to Openshift v3

_Required:_
* install docker
* install RH's s2i. Clone and `make` [this repository](https://github.com/openshift/source-to-image), you will find an executable in `_output` 
* read [here](https://github.com/sclorg/s2i-python-container)

**Source to image from RH7 registry using s2i:**

`$ ~/bin/s2i build https://github.com/openshift/s2i-python.git --context-dir=3.5/test/standalone-test-app/ registry.access.redhat.com/rhscl/python-35-rhel7 tuned/python-35-rhel7`

**Run locally the image:**

```
$ docker run -d -p 8080:8080 --name example-app tuned/python-35-rhel7 
```

**Push to Docker Hub**
* Create an account on Docker Hub
* `docker login`
* `docker push tuned/python-35-rhel7`

**Create an Openshift app from DockerHub**

```
oc new-app registry.hub.docker.com/tuned/python-35-rhel7
```

