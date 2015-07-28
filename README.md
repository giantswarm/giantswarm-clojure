# Clojure Apps on Giant Swarm

This is a simple example of deploying Clojure applications with Docker on [Giant Swarm](https://giantswarm.io/).

Check out the full guide here:

https://blog.giantswarm.io/deploy-clojure-application-in-1-minute/

## Prerequisites 

* A [Giant Swarm account](https://giantswarm.io/request-invite/)
* [Docker](http://docs.docker.com/) installed.
* Make sure you have a [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) installed.
* Make sure you have [Leiningen](https://github.com/technomancy/leiningen) installed.

## Building your Docker Image for Local Testing

If you don't have an own Clojure project, yet, clone this [helloworld repo](https://github.com/denderello/clojure-helloworld).

Put `[com.palletops/uberimage "0.4.1"]` into the `:plugins` vector of your `:user` profile.
A minimal `~/.lein/profiles.clj` should look like:

```
{:user {:plugins [[com.palletops/uberimage "0.4.1"]]}}
```

For more information check out the [`lein-uberimage` GitHub repo](https://github.com/palletops/lein-uberimage).

Open the project root and run `lein uberimage`. You will get back an image uuid. You can test the image locally with

```nohighlight
$ docker run -d -p 3000:8080 <image-uuid>
```

where 8080 is the port that your application listens on. Open your browser at `http://<docker-host>:3000` to see if it worked.

## Building and Pushing your Docker Image to the Registry

1. Add `:uberimage {:tag "registry.giantswarm.io/<username>/<repo>:<tag>"}` to your project's `project.clj`.
2. Run `lein uberimage`.
3. Run `docker push registry.giantswarm.io/<username>/<repo>:<tag>`.

## Running your Application on the Swarm

1. Create a simple [`swarm.json`](giantswarm-clojure/swarm.json) using the image you pushed above. 
2. Run `swarm up`.
