# tosec-trimmer
Trimmer for Tosec Amiga and Atari ST floppy images of releases (games) to make 1g1r one game one rom

```
#2023-08-08-1
#beta

Installing:
click on tosec_trimmer.zip
click on download on the right. (click on the arrow pointing down)
unzip somewhere on disk drive.

Using:
python tt.py "folder with games"
example:
python tt.py "d:\roms\folder with games"
or 
python tt.py "d:/roms/folder with games"

or drag and drop folder to tt.bat.

Note: This program expects your zip files to be in "folder with games", not in subfolders of "folder with games".

Sorted, cleared set will be created in 'folder name-srt' on the same partiton, or disk.
It will be created using HARDLINKS, so it won't use any disk space.
Disk numbers will be changed to disk_a, disk_b, from disk 1 of 2, disk 2 of 2, so hatari can autoload
disk 2.
(Unless there is more than 26 disks)
Too bad retroarch cannot auto mount all files in zip if with usable extension. (without playlist)

To disable creation of m3u playlist, edit tt.py in notepad++, and change line
make_m3u_playlist = 1
to 
make_m3u_playlist = 0

If you want to change folders extension you can change it to '' to not create it at all.
Or bellow the line:
files_connect = '_files'
Add:
files_connect = ''
which will make variable files_connect = to empty.

You can also set extension of playlist to .htm, so when you copy or move playlist with htm extension,
it will also move _files folder.
This htm connection works only on windows.

In retroarch, choose to scan only m3u extension.
You can delete m3u playlist in windows explorer if you do not need it.


if you do not want to have disk_a, b for multi disks, edit tt.py and change 'use_numbers_for_disks'
to some value:

#use_numbers_for_disks=0# use game name disk_a, disk_b, (hatari emulator auto inserts disk_b), default
#use_numbers_for_disks=1# use game name disk_1,game name_disk 2
#use_numbers_for_disks=2# use game name(disk 1 of 2)
#use_numbers_for_disks=3# use game name(disk 1 of 2)[more tags here], sometimes might show error if the file path is longer than 260


if output folder exist, program will exit.


Tested with TOSEC_V2017-04-23


Not related to Tosec group in any way.

For multidisk games, program will try to find other disks, if they exist in folder.


if you get error like this on windows 10:

  File "C:\Users\bojan\Desktop\TEMP\ttdiskv2h5-new-.py", line 46, in fMakeHardlink
    os.link(source,dest)
FileNotFoundError: [WinError 3] The system cannot find the path specified: 'C:\\stx/Leisure Suit Larry 2 - Leisure Suit Larry Goes Looking For Love - In Several Wrong Places - (1988)(Sierra)(Disk 1 of 3).zip' -> 'C:\\stx-sortedd  ddddddddddddddddddddd/1ok/Leisure Suit Larry 2 - Leisure Suit Larry Goes Looking For Love - In Several Wrong Places - (1988)(Sierra)(Disks 3)/Leisure Suit Larry 2 - Leisure Suit Larry Goes Looking For Love - In Several Wrong Places - (1988)(Sierra)(Disks 3)_a.zip'

it could be your path name is too long.
rename source dir to something like 
c:\stx
instead of c:\games\emu\tosec ...

#b added priority to notags regex
#elvira notags is in german language ?



you could also change suffix of changed folder from -srt to -s in code.

or rename specific game disk(s):

from:
Leisure Suit Larry 2 - Leisure Suit Larry Goes Looking For Love - In Several Wrong Places - (1988)(Sierra)(Disk 1 of 3).zip
to:
Leisure Suit Larry 2 - Leisure Suit Larry Goes Looking For Love  - (1988)(Sierra)(Disk 1 of 3).zip
or:
Leisure Suit Larry 2 - (1988)(Sierra)(Disk 1 of 3).zip

remember to rename all disk of a specific game, not just the first one!



or try updating your windows 10

error is because max length of file name path in windows 10.

or it could be a bug in the programme ... 



Also I suggest using Link Shell Extension: https://schinagl.priv.at/nt/hardlinkshellext/hardlinkshellext.html to create
'hardlinks' (for files) and 'hardlink clones' which are folders+hardlinks inside for folders.
Use pick link source, drop hardlink or 'hardlink clones' for folders.
You can delete clones, another instance will exist. Do not edit their content, cause the original file's content
will also change!
Don't use symlink, cause if you delete original, symlink wont work.
If you use hardlink/hardlink clones, and delete original, copy will still work.


note:
hearto uses no-intro dats for atari st, meaning there are only handfull of games.
amiga ipf files are not patched, meaning some games still have game protection.
for amiga, I suggest using lha or whd games with retroarch or some other emulator that supports them
lha and whd are games installed to amiga virtual hdd.

no warranty of any kind given.


changes in 2023-08-07-2
-bug fixes: check if disk 2 is in the list, when using full name
-do not use use_numbers_for_disks=3 in this version

changes in 2023-08-08-1
-fixed bug with 'use_numbers_for_disks=3'.

