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
sudo ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" /bin/subl
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

---

##### To disable AWDL and AirDrop to fix Yosemite WiFi issues:

```
sudo ifconfig awdl0 down
```

And vice versa to restore AirDrop and AWDL (and the WiFi issues):

```
sudo ifconfig awdl0 up
```


