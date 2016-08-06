# git x (git times)

A simple bash script to run git commands into multiple nested git repositories.

It is great for projects that are split into multiple repositories.

The tool detects nested git repositories (one level deep by default) and run any command you pass to it on each nested repository:

```bash
git x status
git x checkout master
git x pull
git x <any valid git command and arguments>
```

## Motivation

It has become a common practice these days to break bigger projects into smaller ones. Take the example below:

```
.
├── README.md
├── frontend-app/
├── library-1/
├── library-2/
├── service-1/
└── service-2/
```

And while this approach makes it easier to maintain and deploy each project individually, it adds complexity to manage them all as "one". There are solutions like [foreman](http://ddollar.github.io/foreman/) and [docker-compose](https://github.com/docker/compose) that helps running them, but you still need to manage each Git repository individually.

This project's goal is to make it easy to run a git command on all these nested git repositories at once. So you can change branches, pull changes and check statuses; literally do everything you could if you would be running these commands on each nested folders.

So instead of doing:

```bash
git status

cd frontend-app
git status
cd ..

cd library-1
git status
cd ..

cd library-2
git status
cd ..

cd service-1
git status
cd ..

cd service-2
git status
cd ..
```

You can simply do:

```bash
git x status
```

It is [Git Submodules](http://www.git-scm.com/book/en/v2/Git-Tools-Submodules) without all the hassle.

## Cloning

Another motivation is on-boarding new developers to a project. We wanted to make it easy to clone a parent repository, and from it clone, all the nested repositories.

If run the tool on a git repository, it automatically creates a `.gitrepositories` file containing the URLs for all nested repositories, such as:

```
git@github.com:fancy-project/frontend-app.git
git@github.com:fancy-project/library-1.git
git@github.com:fancy-project/library-2.git
git@github.com:fancy-project/service-1.git
git@github.com:fancy-project/service-2.git
```

This file then can be checked into source control and latter be used to clone all nested repositories by a new developer:

```bash
git x clone
```

## Deeply nested repositories

To detect deeper repositories just run:
```bash
GITX_DEPTH=n git x status # adjust the value accordingly
```
or
```bash
export GITX_DEPTH=n
git x status
```
or to make it permanent, set the environment variable in the shell initialization file (it could be `~/.bashrc`).

## Instalation

For simplicity, it is available as a NPM package:

```bash
npm install -g git-x
```

But since it is a simple bash script, you can simply download [the latest release](https://raw.githubusercontent.com/pirelenito/git-x/master/git-x.sh) and add it to your path.

```bash
curl -O https://raw.githubusercontent.com/pirelenito/git-x/master/git-x.sh
chmod +x git-x.sh
```
