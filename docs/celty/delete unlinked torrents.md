```
find /HDD1/Media/Downloads -size +50M -links 1 -type f -print
```
Will show all files that have no hard link and that are bigger than 50M. 
Replace `-print` by `-delete` to delete them

Now you may want to delete all snapshots of `HDD1/Media` with this command:
```
zfs list -H -o name -t snapshot HDD1/Media | xargs -n1 zfs destroy
```