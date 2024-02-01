```
Push an existing folder
cd existing_folder
git init --initial-branch=main
git remote add origin git@gitlab.das.becode:becode/my-web-app.git
git add .
git commit -m "Initial commit"
git push --set-upstream origin main
```

```
Push an existing Git repository
cd existing_repo
git remote rename origin old-origin
git remote add origin git@gitlab.das.becode:becode/my-web-app.git
git push --set-upstream origin --all
git push --set-upstream origin --tags
```
