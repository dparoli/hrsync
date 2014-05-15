hrsync
======

hrsync is a simple script showing how to backup a directory with rsync detecting moved and renamed files.

Rsync is a great tool but lack detection of moved and renamed files, with this simple script is possible to avoid transfer of files which were only moved around or renamed.

Basic idea is to create a shadow directory (inside source directory) of hard linked files representing the original filesystem structure, letting rsync recostructing links before transfer.

You will find a new directory (.rsync_shadow) created inside source and target directories, please don't touch the tree inside if you want that the script will continue working. 

Original idea of a shadow directory here: [Detecting File Moves & Renames with Rsync](http://lincolnloop.com/blog/detecting-file-moves-renames-rsync/).

I provide no documentation if you want to know more just look at the source code, it's really short!

Requirements
------------

* rsync >= 3.0
* filesystem with support for hard links
* source and target directory should be on different devices

Usage
-------
Edit hrsync file changing configuration section, source and target directory are a MUST, then
run the script:

```sh
cd <dir>
chmod +x ./hrsync
./hrsync
```
Do your work on the source directory, add and delete files or move them then rerun the script. 
You will find that renamed or moved files won't be transferred again.

Please note that this script is to be considered only an example, feel free to extend the idea for your own backup solution.

Use it at your own risk, this is alpha software provided "as is" without any warranty in any case.

License
-------

hrsync is © 2014 Daniele Paroli. It is free software, and may be redistributed under the terms specified in the LICENSE file.