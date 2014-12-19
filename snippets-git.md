##### To view git log as a tree:

- You will need tree installed (`brew install tree`)
- Edit `~/.gitconfig`:

```
[alias]
lg = "log --graph --all --full-history --color --pretty=format:'%x1b[31m%h%x09%x1b[32m %C(white)- %d%x1b[0m%x20%s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --date=relative"
```
- For live view update in a terminal:

```
while true; 
  do tree .git; # change this to any bash command
  sleep 1;  # sleep for one second
done;
```

---
