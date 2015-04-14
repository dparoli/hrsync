hrsync
======

hrsync is a simple script showing how to backup a directory with rsync detecting moved and renamed files.

Rsync is a great tool but lack detection of moved and renamed files, with this simple script is possible to avoid transfer of files which were only moved around or renamed.

The basic idea is to create a tree (inside source directory) of hard linked files representing the original filesystem structure of the source itself, letting rsync recostructing links in the initial phase of the transfer.
After the initial run you will find a new directory (.rsync_shadow) inside source and target directories, please don't touch the tree inside if you want that the script will continue working. 

Credits due to this brilliant article: [Detecting File Moves & Renames with Rsync](http://lincolnloop.com/blog/detecting-file-moves-renames-rsync/).

Some background info in this serverfault question: [Handling renamed files or directories in rsync](http://serverfault.com/q/489289/220035)

I provide no documentation. If you want to know more just look at the source code, it's really short!

Requirements
------------

* rsync >= 3.0 (on remote host also if you use remote target)
* filesystem with support for hard links on both sides
* source and target directory should be on different devices
* source on local filesystem and optionally target on remote (via ssh)

Usage
-------

1) Both source and target on local filesystem: run the script with source and target directories as arguments:

```sh
cd <dir>
chmod +x ./hrsync
./hrsync /home/user/Documents /media/user/external/Documents
```
2) Source on local filesystem and target on remote host (via ssh): run the script with source, target and remote host arguments:

```sh
cd <dir>
chmod +x ./hrsync
./hrsync /home/user/Documents /root/Documents root@example.com
```

Do your work on the source directory: add, delete and move files, then rerun the script. 
Target directory will be synced without transferring moved or renamed files.

Please note that this script is to be considered only an example, feel free to extend the idea for your own backup solution.
Use it at your own risk, this is alpha software provided "as is" without any warranty in any case.

License
-------

hrsync is © 2014 Daniele Paroli. It is free software, and may be redistributed under the terms specified in the LICENSE file.
