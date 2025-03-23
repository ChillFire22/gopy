# gopy
A mark-then-move CLI tool built in Go that alleviates remembering paths and renders moving or copying typo-proof

# Functionality
+ Mark files to move and they get stored in a 'targets' file
+ Mark destination(s) to move targets into and they get stored in a 'destinations' file
+ List, with indexes, the content of the targets files, destinations file, or current working directory
+ Select entires to move and those to move-into of the targets and destinations files, respectively (default: all marked files, last marked destination)
+ Clear entries from the targets or destinations file (default: all)
+ Move, by copying or cutting, the selected files to the selected destination(s)
+ All commands (except for List) are index-based, and any provided indexes take priority over any default indexes (Clear "1 3" removes entries 1, and 3 regardless of the internal cursor set by Select)
+ Paths used internally will be absolute paths to ensure consistency

# Extra
Any extra functionality, such as editing the value of an entry, is open for discussion and future implementation
The first version, v-0.0.1, will be the first prototype version of the tool and will strictly be command-based with no interactivity
Copying directories will not be supported in v-0.0.1

# Examples
Assuming the placeholder command name of 'gopy'
Marking:
```
$gopy --list cwd
 Index)  Path
 1)  foo.txt
 2)  bar.txt
 4)  supersecretburgerrecipe
 3)  readme.md
$gopy --mark "1 2 4"
$gopy --list targets
 Index, selected(yes:y/no:n)  Path
 1, y)  /path/to/foo.txt
 2, y) /path/to/bar.txt
 3, y) /path/to/readme.md
$cd /path/to/dirA
$cd dirB/dirC
$cd dir1
$gopy --move 3 --copy
$ls
 readme.md
$cd ..
$gopy --move
$ls
 foo.txt  bar.txt  readme.md
$gopy --select "3 2"
cd ..
$gopy --move --cut
$ls
 readme.md  bar.txt
```
and in the original directory, the two files are deleting

# Warning
This tool is provided as-is with no guarantees.
