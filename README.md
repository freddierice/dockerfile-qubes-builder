# dockerfile-qubes-builder
A docker image for building qubes.

## run
```
[user@host ~]$ ./run
Cloning into 'qubes-builder'...
remote: Counting objects: 4299, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 4299 (delta 2), reused 8 (delta 2), pack-reused 4287
Receiving objects: 100% (4299/4299), 3.12 MiB | 4.29 MiB/s, done.
Resolving deltas: 100% (2405/2405), done.
[user@81371a48c3a0 build]$ ls
qubes-builder
```

## copy files to host
```
[user@81371a48c3a0 build]$ cp build.iso /shared
```
