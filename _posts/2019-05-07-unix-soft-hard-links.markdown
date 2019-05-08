---
layout: post
title: Inode, soft and hard links on UNIX/LINUX
date:   2019-05-06 21:23:50 +0300
categories: notes
tags: unix
---

## What is an inode on UNIX/LINUX systems?
---
<sup>[source][inode-definition]</sup>

An inode is a data structure on a filesystem on Linux and other Unix-like operating systems that stores all the information about a file **_except its name and its actual data._**

**_When a file is created, it is assigned both a name and an inode number, which is an integer that is unique within the filesystem._** Both the file names and their corresponding inode numbers are stored as entries in the directory that appears to the user to contain the files. That is, **_the directory associates file names with inodes_**. A directory contains an entry for itself, its parent, and each of its children.

Whenever a user or a program refers to a file by name, the operating system uses that name to look up the corresponding inode, which then enables the system to obtain the information it needs about the file to perform further operations. That is, a file name in a Unix-like operating system is merely an entry in a table with inode numbers, rather than being associated directly with a file. The inode numbers and their corresponding inodes are held in **_inode tables_**, which are stored in strategic locations in a filesystem, including near its beginning.

The following will show the name of each object in the current directory together with its inode number:

```
ls -i
```

## What is the links on UNIX/LINUX systems?
---

In a nutshell, a link in UNIX is a pointer to a file or directory.

## What are the differences between soft(symbolic) and hard links?
---
<sup>[source][soft-hard-links]</sup>

### Hard Link:

**_A hard link is merely an additional name for an existing file on Linux or other Unix-like operating systems._**

* Each hard linked file is assigned **_the same inode value as the original_**, therefore they reference the same physical file location. Hard links more flexible and remain linked even if the original or linked files are moved throughout the file system, although hard links are unable to cross different file systems.
* **_Links have actual file contents and size._**
* Removing any link, just reduces the link count, but doesn’t affect other links.
* **_We cannot create a hard link for a directory_** to avoid recursive loops.
* If original file is removed then the link will still show the content of the file.
* Hard links can also be created to other hard links.

### Soft(Symbolic) Link:

**_A symbolic link is a file that links to another file or directory using its path._**

* A soft link is similar to the file shortcut feature which is used in Windows Operating systems. Each soft linked file contains **_a separate inode value_** that points to the original file. As similar to hard links, any changes to the data in either file is reflected in the other. Soft links can be linked across different file systems, although if the original file is deleted or moved, the soft linked file will not work correctly (called hanging link).
* **_Soft Link contains the path for original file and not the contents._**
* A soft link **_can link to a directory._**
* Link across filesystems: If you want to link files across the filesystems, you can only use symlinks/soft links.

<!-- 16:9 aspect ratio -->
<div class="responsive-embed responsive-embed-16by9">
  <iframe class="responsive-embed-item" src="https://www.youtube.com/watch?v=4-vye3QFTFo"></iframe>
</div>

[inode-definition]:         http://www.linfo.org/inode.html
[soft-hard-links]:          https://www.geeksforgeeks.org/soft-hard-links-unixlinux/
