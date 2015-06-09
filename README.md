# Clojure Apps on Giant Swarm

## Prerequisites 

1. Make sure you have a [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) installed.
2. Make sure you have [Leiningen](https://github.com/technomancy/leiningen) installed. If not:
`
$ brew install leiningen
`
3. Put `[com.palletops/uberimage "0.4.1"]` into the `:plugins` vector of your `:user` profile.
A minimal `~/.lein/profiles.clj` should look like:
`
{:user {:plugins [[com.palletops/uberimage "0.4.1"]]}}
`

## Building your Docker Image for Local Testing

Open the project root and run `lein uberimage`. You will get back an image uuid. You can test the image locally with

```no highlight
$ docker run -d -p 8080:3000 <image-uuid>
```

where 3000 is the port that your application listens on. Open your browser at `http://<docker-host>:8080` to see if it worked.

## Building and Pushing your Docker Image to a Registry

