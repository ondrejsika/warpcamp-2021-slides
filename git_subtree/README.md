# Git Subtree

## Setup Monorepo

Clone & setup remotes

```
git clone git@gitlab.sikalabs.com:examples/subtree/mono.git
cd mono

git remote add proj-a git@gitlab.sikalabs.com:examples/subtree/proj-a.git
git remote add proj-b git@gitlab.sikalabs.com:examples/subtree/proj-b.git
git remote add proj-c git@gitlab.sikalabs.com:examples/subtree/proj-c.git
```

Create some commits

```
echo "Monorepo" > README.md
git add README.md
git commit -m "docs: Create README"

mkdir proj-a
echo "Proj A" > proj-a/README.md
git add proj-a
git commit -m "docs(proj-a): Create README"

mkdir proj-b
echo "Proj B" > proj-b/README.md
git add proj-b
git commit -m "docs(proj-b): Create README"

git push
```

See:

- https://gitlab.sikalabs.com/examples/subtree/mono

## Push Subtrees

```
git subtree push --prefix proj-a  --annotate "[generated] " proj-a master
git subtree push --prefix proj-b  --annotate "[generated] " proj-b master
```

- https://gitlab.sikalabs.com/examples/subtree/proj-a
- https://gitlab.sikalabs.com/examples/subtree/proj-b

## Pull Subtrees

Create `proj-c` repo

```
git clone git@gitlab.sikalabs.com:examples/subtree/proj-c.git
cd proj-c
echo "Proj C" > README.md
git add README.md
git commit -m "docs: Create README"
git push origin master
cd ..
rm -rf proj-c
```

Allow non fast-forward merges

```
git config --local merge.ff false
```

Add repo

```
git subtree add --prefix proj-c proj-c master
```

Pull

```
git subtree pull --prefix proj-c proj-c master
```

Push

```
git subtree push --prefix proj-c --annotate "[generated] " proj-c master
```

Pull

```
git subtree pull --prefix proj-c proj-c master
```
