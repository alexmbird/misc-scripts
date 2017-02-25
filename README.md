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

Convert individual flac files or a directory full of them into mp3s using ffmpeg/avconv.

*  Preserves metadata
*  Preserves cover art &amp; other files 
*  ...but does not preserve `.cur` and `.log` files, since they belong in flac-land

You know when you start writing a tool to do a simple job, only three hours later it turns out not to be simple and you really wish you'd used Python?  That.

Potential improvements:

*  Lame is singlethreaded and nowadays everything is multicore.  Since albums consist of many tracks, speed things up by getting [GNU Parallel](https://www.gnu.org/software/parallel/) to transcode N files at once.