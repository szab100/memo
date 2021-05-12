##### Remove .gitignore matched files from all commits (Warning: rewrites history!)
```
git filter-branch -f --index-filter 'git ls-files -i --exclude-standard| xargs -r git rm --cached --ignore-unmatch -q' -- --all
```

##### View Code Ownership (using git-blame)
```
git ls-files | while read f; do     git blame -w -M -C -C --line-porcelain "$f" |    grep -I '^author-mail '; done | cut -f2 -d'<' | cut -f1 -d'>' | sort -f | uniq -ic | sort -nr
```

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
