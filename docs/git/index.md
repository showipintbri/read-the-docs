# Git

## The simplest Git workflow
Init --> Add --> Commit --> Push

1. Create a local repo
2. Add all files from your current directory to Git
3. Commit those files/changes
4. Push those changes to the repo

```bash
git init .
git add .
git commit -m "New Files Added"
git push
```

## Clone Remote Repository
```bash
git clone https://github.com/ntop/nDPI.git
```

## Clone a Specific Branch from Remote Repository
**NOTE:** Still fetches all the branches but marks the one you specify as active.
```bash
git clone --branch 4.2-stable https://github.com/ntop/nDPI.git
```

## Clone a Specific Branch and Only that Branch from a Remote Repo
```bash
git clone -b 4.2-stable --single-branch https://github.com/ntop/nDPI.git
```
