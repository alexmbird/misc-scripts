Miscellaneous Scripts
=====================

A variety of scripts I find useful everywhere.


## Setup

To install...
```bash
$ git clone git@github.com:alexmbird/misc-scripts.git /opt/mockyscripts
```

To add to system-wide path:
```bash
$ sudo vi /etc/environment
    # Append '/opt/mockyscripts' to PATH
$ source /etc/environment && export PATH
```

To make them work seamlessly under sudo:
```bash
$ sudo visudo -f /etc/sudoers.d/path
    # Add something like:
    Defaults        secure_path="/opt/mockyscripts:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
```


## What's in the toolbox?

### hevconv

Use ffmpeg to transcode a video to hevc, saving much disk space.


### img2jpeg

Use ImageMagick to batch-convert images to jpeg with options for scaling & noise reduction.


### on-all-lxc

Run a command on every LXC container within a host.

Example:

```bash
$ on-all-lxc apt-get -y -qq update
container1 output...
container2 output...
```


### borgmeup

A wrapper script around the [borg](http://borgbackup.readthedocs.io/) backup tool to automate daily/weekly/monthly backups with automatic pruning of outdated archives.


### flac2mp3

Convert individual flac files or a directory full of them into <strike>mp3s</strike> mp3 or [opus](http://opus-codec.org/) using ffmpeg/avconv.

*  Preserves tags &amp; filesystem metadata
*  Preserves cover art &amp; other files 
*  ...but does not preserve `.cur` and `.log` files, since they belong in flac-land
*  Encoders are mostly singlethreaded, so uses a Python ThreadPool to run as many in parallel as you have cores for a huge speedup.
*  Supports the new [opus](http://opus-codec.org/) codec, giving better compression &amp; higher quality than mp3.

Requires Python 3.4+.


### flashtest

Test flash media by writing & validating random files.

Counterfeit flash media typically fakes its size by overwriting existing blocks.  This means writes succeed, and you only discover something is wrong when you later try to read your data.  Flashtest fills your device with random files then uses checksums to validate the data can be re-read. 

Also useful for detecting genuine-but-worn-out media.

NB: O_DIRECT is unavailable on OSX.  Thus there's no way (without a `sudo purge`) to fully disable the OS's block cache.  It is assumed that your flash media is sufficiently larger than ram for this not to matter :)

No warranty but it works for me.  Be aware that repeatedly writing to your flash wears it out.

Requires Python 3+
