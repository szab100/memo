##### Terminal shortcuts:
---

Shortcut | Terminal/iTerm2 command
:--- |:---
<kbd>Ctrl</kbd> + <kbd>U</kbd> | delete from the cursor to the start of the line
<kbd>Ctrl</kbd> + <kbd>K</kbd> | delete from the cursor to the end of the line
<kbd>Ctrl</kbd> + <kbd>W</kbd> | delete from the cursor to the start of the word
<kbd>Ctrl</kbd> + <kbd>A</kbd> | go to the start of the line
<kbd>Ctrl</kbd> + <kbd>E</kbd> | go to the end of the line

---

##### locate:

- To update db of files indexed by locate:

```
sudo /usr/libexec/locate.updatedb
locate -i <file>
(-i flag for case-insensitive search)
```

- locate is faster than `sudo find / -iname "word"`

- To see statistics about the information that locate has cataloged, use the "-S" option:

```
locate -S
```

---

##### To create sym link to Sublime:

```
sudo ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl
```

---

##### Homebrew:

- `brew install <something>`

- update brew itself: 
```
brew update
```

- update tools installed with brew:

```
brew upgrade

brew upgrade <something>
```

- install the GNU version of sed called gsed (Mac's sed is BSD based):

```
brew install gnu-sed
```

---

##### tree -d

`tree` displays a tree view of the filesystem

- `brew install tree`

- `tree -d` to view just the directories and to suppress listing file names

---

##### To disable AWDL and AirDrop to fix Yosemite WiFi issues:

```
sudo ifconfig awdl0 down
```

And vice versa to restore AirDrop and AWDL (and the WiFi issues):

```
sudo ifconfig awdl0 up
```

---

##### To copy/paste from the OS X clipboard:

- pbcopy (pasteboard copy)

To pipe the output of the command to the OS X clipboard:

```
ls | pbcopy
```

- pbpaste (pasteboard paste)

```
pbpaste > file.txt
```

- To escape spaces properly in the directory path:

```
pwd | pbcopy
cd "`pbpaste`"
```
or
```
cd "$(pbpaste)"
```

---

##### Use Spotlight to search from command line:

```
mdfind <keyword>
```

To find all executables:

```
mdfind "kMDItemKind == 'Unix Executable File'"
```

---

##### To find all Java apps:

```
sudo find /Applications -type d -name *.app -prune -exec sh -c 'ls -R "$1" | grep -q \.jar\$' {} {} \; -print
```

---


