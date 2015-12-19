```
git clone https://github.com/hhru/frontik.git tests
cd tests
for branch in `git branch -a | grep remotes | grep -v HEAD | grep -v master`; do git branch --track ${branch#remotes/origin/} $branch; done;
git filter-branch --tag-name-filter cat --prune-empty --subdirectory-filter tests -- --all
git remote rm origin
git remote add origin https://github.com/kurtov/frontik_tests.git
git push -u origin --all

cd ..

git clone https://github.com/hhru/frontik.git frontik
cd frontik
for branch in `git branch -a | grep remotes | grep -v HEAD | grep -v master`; do git branch --track ${branch#remotes/origin/} $branch; done;
git filter-branch --force --index-filter 'git rm -fr --cached --ignore-unmatch -- tests' --prune-empty --tag-name-filter cat -- --all
git remote rm origin
git remote add origin https://github.com/kurtov/frontik.git
git push -u origin --all
```

Ссылки:
- https://help.github.com/articles/splitting-a-subfolder-out-into-a-new-repository
- https://help.github.com/articles/remove-sensitive-data
- https://coderwall.com/p/0ypmka/git-clone-all-remote-branches-locally
