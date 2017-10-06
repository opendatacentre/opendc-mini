# Style Guide

---

This page describes design elements for the **opendc-mini** course.

---

## Asciinema

*Offical [Website](https://asciinema.org)*
*Asciinema Player GitHub [Repo](https://github.com/asciinema/asciinema-player)*

`Asciinema` is used to show command line usage.

Before recording a console session, minimise the prompt size with the following command.

```console
$ export PS1="\\\$ "
```

When recording a console session make sure that there are no pauses longer than 1.5 seconds.

```console
asciinema rec -w 1.5 ~/Sites/OpenDatacentre/opendc-mini/docs/asciinema/command_aliases.json
```

To play back a recorded console session.

```console
asciinema play ~/Sites/OpenDatacentre/opendc-mini/docs/asciinema/kubectx_kubens.json
```

## Image Sizes


## Screen Capture


## Video Compression


## YouTube



## Serving Content for Testing

To serve the Gitbook site for testing on the local network, as opposed to the localhost which is used by `gitbook serve`, use the built-in Python HTTP server.

```console
$ cd opendc-mini
$ python -mSimpleHTTPServer
```

[Site](http://192.168.1.10:8000/_book/)
