# Cloud Foundry R Buildpack

A '[R](http://www.r-project.org/)' buildpack for [CloudFoundry](http://cloudfoundry.org/) that includes [Rserve](https://rforge.net/Rserve/) for supporting remote callers using the rserve client libraries available in those languages.

## Example Java Usage
```bash
$ cd ~/workspace/java-r-buildpack/test/java
$ mvn install
$ cf push --no-route
```

## Caveats
When pushing an app using the buildpack to CF using [bosh-lite](https://github.com/cloudfoundry/bosh-lite) you may get an error when R installs: 
```
libreadline.so.5: cannot open shared object file: No such file or directory
```

This happens because the R binary relies on an older version of libreadline shared library than the one that comes installed on the warden stemcell.
Rather than installing the older version onto the root partition, to get around this I created a symbolic link that maps the one R is looking for to the one on the stemcell:

```bash
root:/var/vcap/packages/rootfs_lucid64/lib# ln -n ./libreadline.so.6 libreadline.so.5
```
