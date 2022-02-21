```
find /HDD1/Media/Downloads -size +50M -links 1 -type f -print
```
Will show all files that have no hard link and that are bigger than 50M. 
Replace `-print` by `-delete` to delete them