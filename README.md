# Docker images

Images are available on Quay: https://quay.io/repository/vrutkovs/sti-hugo


# sti-hugo

This is an source builder image for [Hugo](https://github.com/gohugoio/hugo) - a fast and modern static web site generator.

## What is "source builder"?

This image is compatible with the [Source-to-Image](https://github.com/openshift/source-to-image) project
used by [OpenShift Origin](https://github.com/openshift/origin). This allows to build the Hugo website,
to verify there is no typo in configuration and then run the final blog using Hugo web server.

## How it works?

* Create new Github repository and push your Hugo site to this repo
* Install `s2i` tool (see the link above)
* Build: `$ s2i build https://github.com/<org>/<hugo-repo> quay.io/vrutkovs/sti-hugo hugo-blog`
* Run: `$ docker run hugo-blog`

## How to use it with OpenShift?

Run:

```
$ oc new-app quay.io/vrutkovs/sti-hugo/hugo~http://github.com/<org>/<hugo-repo>
```


This is forked from `uberamd/sti-hugo` and updated for newer versions: https://github.com/mfojtik/sti-hugo
