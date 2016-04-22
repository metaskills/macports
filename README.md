
# MetaSkills MacPorts repository

You can learn about setting up your own MacPorts repos at the following links.

* http://trac.macports.org/wiki/howto/InstallingOlderPort
* http://journal.bitshaker.com/articles/2007/10/20/install-old-versions-of-ports-using-macports/

In short, I added this to my /opt/local/etc/macports/sources.conf file.

```
file:///Users/kencollins/Repositories/macports [nosync]
```

Now run the `portindex` command while in that directory to pick up on changes to your own Portfiles.


# Generating Checksum Examples

```
$ shasum -a 256 /Users/kencollins/Desktop/freetds-0.91.112.tar.gz
$ openssl sha1 /Users/kencollins/Desktop/freetds-0.91.112.tar.gz
$ openssl rmd160 /Users/kencollins/Desktop/freetds-0.91.112.tar.gz
```

# My Oracle 64-bit Notes (11.2.0.3.0)

This Portfile only focuses on x86_64 for intel. It also installs the sqlplus package. Even though it does fix pre-built libraries using `otool` and `install_name_tool`, you still have to use `DYLD_LIBRARY_PATH`. Just follow the notes in the post install message.

* sudo port install oracle-instantclient @11.2.0.3.0 +universal


# My FreeTDS Notes

* deactivate, activate, install
* freetds@0.82_0

```
$ sudo port install freetds@1.0rc1_1 +openssl
```


# My ImageMagic v6.6.2 Notes

First I did a full check out of the MacPorts trunk.

```shell
$ cd ~/Repositories
$ svn co http://svn.macports.org/repository/macports/trunk macports_trunk
$ cd macports_trunk
```

Now I found out what was the commit that had the last version v6.6.2 mentioned

```shell
$ svn log dports/graphics/ImageMagick/Portfile
... examine output ...
r69223 | ryandesign@macports.org | 2010-06-29 00:16:10 -0400 (Tue, 29 Jun 2010) | 2 lines
ImageMagick: update to 6.6.2-9; see #25457
```

Now make it in out own port index.

```shell
$ mkdir graphics
$ svn co  -r 69223 'http://svn.macports.org/repository/macports/trunk/dports/graphics/ImageMagick/' graphics/ImageMagick
$ portindex
```

Now install it.

```shell
$ sudo port install ImageMagick @6.6.2-9
$ sudo port clean ImageMagick
$ export CC="/usr/bin/gcc-4.2"
```
