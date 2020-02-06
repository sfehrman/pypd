# pypd

**Python version of Print Directory (pd) command**

This program will read the current directory or the directories listed 
on the command line and display the contents showing the **files** first 
then the **directories**. The `pd` command provides an alternative the 
the unix/linux `ls` command.

The original `pd` command was written by me (a long time ago) using "c", 
you can access that that project [HERE](https://github.com/sfehrman/pd)

# Install
1. You **must** have Python 3 installed
2. Clone or Download the project
3. Copy the ``pd`` script to a folder that is in your **PATH** (``/usr/local/bin``)

# Help

```
pd -h

    -b        brief, unformatted output
    -c        count entries only
    -d <args> date/time options: [full|f|dtm|m|dta|a|dtc|s] [mdy|dmy|ymd]
    -h        help
    -i        show inode numbers
    -l        show symbolic link's status
    -m        show permissions mode [4777]
    -n <args> no output options: [dot|d|hdr|h|name|n|pwd|p|qty|q]
    -p        permissions: rwx rwx rwx   name.group
    -s <args> sorting options: (default = '-s name')
              [none|0|name|n|dtm|m|dta|a|dtc|c|inode|i|link|l|size|s,rev|r] 
    -t <args> select type: [file|f|dir|d] (default show both) 
    -u <args> select unit for file size: [b|k|m|g] (default = '-u b') implicitly uses '-S'
    -v        program version
    -A        show all entries (including '.' and '..')
    -B        show file blocks allocated
    -C        output using single column
    -D        show sub-directory information not the entries (treat it like a file)
    -L        show hard link count
    -S        show file size (default = bytes)
    -T        show file types

```

# Examples

## Default output:

```bash
pd

/Users/sfehrman/Documents/github/pypd   Entries: 8

Files: 6

README.md   bar         exe         link        notes.txt   pd          

Directories: 2

.git        .idea       

```

## Size and Permissions (like ``ls -la``):

```bash
pd -S -p

/Users/sfehrman/Documents/github/pypd   Entries: 8

Files: 6

Name            Size (Bytes)   User  Group Other           User.Group   
----------------------------------------------------------------------------------------------------
README.md               1922   rw-   r--   r--         sfehrman.staff       
bar                        4   rwx   r-x   r-x         sfehrman.staff        -> (Bad Link) /foo
exe                        0   rws   rwS   rwx         sfehrman.staff       
link                    1922   rw-   r--   r--         sfehrman.staff        -> README.md
notes.txt                985   rw-   r--   r--         sfehrman.staff       
pd                     20609   rwx   r-x   r-x         sfehrman.staff       

Directories: 2

Name            Size (Bytes)   User  Group Other           User.Group   
----------------------------------------------------------------------------------------------------
.git                     510   rwx   r-x   r-x         sfehrman.staff       
.idea                    306   rwx   r-x   r-x         sfehrman.staff       
```

## All date information:

```bash
pd -dall

/Users/sfehrman/Documents/github/pypd   Entries: 8

Files: 6

Name           Modified              Accessed              Status Changed     
----------------------------------------------------------------------------------------------------
README.md      2019-10-18 21:05:25   2019-10-18 21:05:25   2019-10-18 21:05:25
bar            2019-10-14 18:42:45   2019-10-14 18:42:45   2019-10-14 18:42:45 -> (Bad Link) /foo
exe            2019-10-16 21:53:37   2019-10-16 21:53:37   2019-10-16 21:59:57
link           2019-10-18 21:05:25   2019-10-18 21:05:25   2019-10-18 21:05:25 -> README.md
notes.txt      2019-10-16 18:02:53   2019-10-16 18:43:03   2019-10-16 18:02:53
pd             2019-10-17 20:50:12   2019-10-18 20:46:41   2019-10-17 20:50:12

Directories: 2

Name           Modified              Accessed              Status Changed     
----------------------------------------------------------------------------------------------------
.git           2019-10-18 21:05:25   2019-10-18 21:04:01   2019-10-18 21:05:25
.idea          2019-10-18 20:51:58   2019-10-18 21:04:01   2019-10-18 20:51:58
```

## Show only type "file":

```bash
pd -tf /

/   Entries: 28

Files: 4

.DS_Store                                 .dbfseventsd
.file                                     installer.failurerequests

```

## Show only type "directory":

```bash
pd -td /

/   Entries: 28

Directories: 24

.DocumentRevisions-V100                   .MobileBackups
.PKInstallSandboxManager                  .PKInstallSandboxManager-SystemSoftware
.Spotlight-V100                           .fseventsd
.vol                                      Applications
Library                                   Network
System                                    Users
Volumes                                   bin
cores                                     dev
etc                                       home
net                                       private
sbin                                      tmp
usr                                       var
```

## Show Size, Blocks Allocated, Inodes:

```bash
pd -S -i -B

/Users/Shared/VirtualBox/HardDisks   Entries: 1

Files: 1

Name                            Size (Bytes)      Blocks       Inode
----------------------------------------------------------------------------------------------------
Windows7Ultimate64bit.vdi        35769196544    69861712     1175605

Directories: 0
```

## Set size units (MBytes):

```bash
pd -S -i -B -um

/Users/Shared/VirtualBox/HardDisks   Entries: 1

Files: 1

Name                           Size (MBytes)      Blocks       Inode
----------------------------------------------------------------------------------------------------
Windows7Ultimate64bit.vdi              35769    69861712     1175605

Directories: 0
```
