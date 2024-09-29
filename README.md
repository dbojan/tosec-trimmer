
# tosec-trimmer

## Trimmer for Tosec Amiga and Atari ST floppy images of releases (games) to make 1g1r one game one rom

<code> <pre> 
v2023-09-29-1

Tool to create set of games for gaming system with 1g1r (one game one rom) collection.
Mostly for Atari ST/Amiga, but can probably be used for other game systems.

To download tosec collection, google tosec on the internet, or tosec atari st.
They might be several gigabytes big. Using torrent, you can choose which folders to download,
(if option is available), or click show all on internet archive page and download single files.
For some systems, there already created 1g1r sets, like Hearto.
Usually found on the internet archive.

This program will create new folder named 'folder with games-srt', (sorted)
in which there will be hardlinks to original 'folder with games'.
(Hardlinks are like copies of files, but take no space on disk)
Multiple version of same games will not be hardlinked ('copied') to new folder.
Versions marked with [b]-bad and [v]-virus will be created to '3_bad' folder
Versions with fr, de, jp, es, it tags will be created in 2_for(eign) folder.
Note that in foreign folder there will be no separation between good and bad versions.
This is because if script encounters foreign tag (de, es...) it replaces category (1ok, 3bad)
with foreign 2for.

Before sorting within each category, there is an added score. For example no [] tags of any kind 
has lower score, then [cr]-cracked has higher score, then [a]-alternate.
[!] verified good dumps can have another tags, like [a]-alternate, so they don't have
the lowest score. That might change in the future.
Those with the lowest score will be selected first.

Multi disk games will be created in their own folder with playlist in root folder.
Playlist (.m3u) is creted in 'folder with games-srt' folder, for retroarch.
You can edit tt.py in notepad++ to change options.

## Installing:
You need to have Python installed
(If you don't have it installed, go to https://www.python.org/, 
move mouse over 'Downloads' and click on button under 'Download for Windows'
Save pythonxx.exe somewhere, and double click it to install it. Restart pc, or windows explorer.)

Installing Tosec Trimme:
Right click on the link [here](https://github.com/dbojan/tosec-trimmer/raw/main/tosec_trimmer.zip), 
Select "Save Link As".
Unzip somewhere on disk drive.

## Using:
drag and drop folder with amiga or atari st games,  on "tt-drop-folder-here.bat"

or from command line
python tt.py "folder with games"
example:
python tt.py "d:\roms\folder with games"
or 
python tt.py "d:/roms/folder with games"

Note: This program expects zip files of games to be in dropped folder directly,
not in subfolders, or subfolders of subfolders:

for example if you drop folder 'atari-st', games are supposed to be in that folder.
ok: d:\mygames\atari-st\game1.zip,  d:\mygames\atari-st\game2.zip
not ok: d:\mygames\atari-st\another-folder\game1.zip


More info:
Sorted, cleared set will be created in 'folder name-srt' on the same partiton, or disk.
It will be created using HARDLINKS, so it won't use any disk space.
Disk numbers will be changed to disk_a, disk_b, from disk 1 of 2, disk 2 of 2, so hatari can
autoload disk 2.
(Unless there is more than 26 disks)
Too bad retroarch cannot auto mount all files in zip if with usable extension. 
(without playlist)

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

You can also set extension of playlist to .htm, so when you copy or move playlist with htm 
extension, it will also move _files folder.
This htm connection works only on windows.

In retroarch, choose to scan only m3u extension.
You can delete m3u playlist in windows explorer if you do not need it.


if you do not want to have disk_a, b for multi disks, edit tt.py and change 
'use_numbers_for_disks' to some value:

use_numbers_for_disks=2


if output folder exist, program will exit.


Tested with TOSEC_V2017-04-23


Not related to Tosec group in any way.

For multidisk games, program will try to find other disks, if they exist in folder.


if you get error like this on windows 10:

  File "C:\Users\bojan\Desktop\TEMP\ttdiskv2h5-new-.py", line 46, in fMakeHardlink
    os.link(source,dest)
FileNotFoundError: [WinError 3] The system cannot find the path specified: 
'C:\\stx/Leisure Suit Larry 2 - Leisure Suit Larry Goes Looking For Love - 
In Several Wrong Places - (1988)(Sierra)(Disk 1 of 3).zip' -> 
'C:\\stx-sortedd  ddddddddddddddddddddd/1ok/Leisure Suit Larry 2 - 
Leisure Suit Larry Goes Looking For Love - In Several Wrong Places - (1988)
(Sierra)(Disks 3)/Leisure Suit Larry 2 - Leisure Suit Larry Goes Looking For Love - 
In Several Wrong Places - (1988)(Sierra)(Disks 3)_a.zip'

it could be your path name is too long.
rename source dir to something like 
c:\stx
instead of c:\games\emu\tosec ...


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

or it could be a bug in the program ... 



Also I suggest using Link Shell Extension: 
https://schinagl.priv.at/nt/hardlinkshellext/hardlinkshellext.html 
to create 'hardlinks' (for files) and 'hardlink clones' which are folders+hardlinks 
inside the folders.
Use pick link source, drop hardlink or 'hardlink clones' for folders.
You can delete clones, another instance will exist. Do not edit their content, cause the
original file's content will also change!
Don't use symlink, cause if you delete original, symlink wont work.
If you use hardlink/hardlink clones, and delete original, copy will still work.


note:
hearto uses no-intro dats for atari st, meaning there are only handfull of games.
amiga ipf files are not patched, meaning some games still have game protection.
for amiga, I suggest using lha or whd games with retroarch or some other emulator that 
supports them. Lha and whd are games installed to amiga virtual hdd.

no warranty of any kind given.



todo:
add option to move hardlinks to first letter of the name of the file.
for now drag and drop folder on 'move folders and files to first letter folders.bat'

changes in 2023-09-29-1
-bug fixed that stopped creation of next games in folder, if one game had wrong disk name,
 thanks /u/rockstarfruitpunch for the bug report and the fix
-added r to comment string in python code, so there are no deprecation warnings
-added option to specify suffix for sorted folder instead of default '-srt'
-disabled default creation of m3u, to enable, set make_m3u_playlist=1 in tt.py, using notepad,
 or notepad++

changes in 2023-08-07-2
-bug fixes: check if disk 2 is in the list, when using full name
-do not use use_numbers_for_disks=3 in this version

changes in 2023-08-08-1
-fixed bug with 'use_numbers_for_disks=3'.

changes in 2023-08-10-1
-more bug fixes for lower case for latter disks

changes in 2023-08-12-1
-added more info in readme.txt
-added 'move folders and files to first letter folders.bat'

changes in 2023-08-21-1
-small changes in readme.txt
-renamed .bat file to 'tt-drop-folder-here.bat'