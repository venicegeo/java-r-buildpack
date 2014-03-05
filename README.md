# Cloud Foundry R Buildpack

A 'R' buildpack for CloudFoundry that includes RServe for supporting remote callers using the rserve client libraries available in those languages.

## Example Java Usage
```bash
$ cd ~/workspace/java-r-buildpack/test/java
$ mvn install
$ cf push --no-route
```

## Caveates
Using bosh-lite you may get an error when R installs: 'libreadline.so.5: cannot open shared object file: No such file or directory'.
This happens because the R binary relies on an older version of libreadline shared library than the one that comes installed on the warden stemcell.
Rather than installing the older version onto the root partition, to get around this I created a symbolic link that maps the one R is looking for to the one on the stemcell:

```bash
root@09a0ee20-9c76-4ced-95e0-393469882968:/var/vcap/packages/rootfs_lucid64/lib# ln -n ./libreadline.so.6 libreadline.so.5
```
