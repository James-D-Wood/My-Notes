# Removing Sensitive Info Using BFG

## Whoops
So you committed sensitive information to your repo. The same repo that's connected to the interwebs and possibly visible to the world. You're better than this. You know not to commit anything even remotely sensitive to GitHub. And yet, you're human and copying and pasting from your terminal has gotten you in trouble again. What to do?

## Scrubba-Dub
Thankfully the BFG utility can be used to wipe your repo's history clean in these easy steps.
1) Clone a mirror of the repo
```
git clone --mirror https://github.com/user/repo
```

2) Create a .txt file with the info you'd like redacted special ops style line by line 
```
touch whoops.txt
```

3) Run the BFG utility
```
bfg --replace-text whoops.txt repo.git
```

4) Run git cleanup and push changes
```
cd repo.git
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git push
```

Easy peasy lemon squeezy.

## A footnote on cleaning
I actually had no idea what `git reflog` or `git gc` referenced. So I did some reading. Reflogs is short for reference logs (I now feel a bit silly for worrying about why someone would want to flog their repo). Git uses these reflogs to track updates to the tips of branches. The expire command removes old or unreachable entries created by the BFG util.

`git gc` is also necessary but a bit less exciting. It prunes unnecessary files to optimize your repo.

#### References
https://git-scm.com/docs/git-gc
https://rtyley.github.io/bfg-repo-cleaner/
https://anchor.host/removing-sensitive-data-from-git-repos/
https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog