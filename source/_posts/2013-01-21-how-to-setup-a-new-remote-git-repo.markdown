---
layout: post
title: "How to setup a new remote git repo"
date: 2013-01-21 00:31
comments: true
categories: git 
---

### If you already have a repo, and want to version control it:

* Goto your repo, and initialize it to a git repo

```
	cd my_repo
	git init
```

* Goto [github](http://github.com) to create your remote repo

* Connect your local repo to the remote repo

```		
	git remote add origin [your_remote_repo]
```	

* Set your branch as the remote master

```		
		vi .git/config
```
   Add
	
```		
	[branch "master"]
		remote = origin
		merge = refs/heads/master
```

* If you want to use different user name and email with your global settings, please change it here. Add

```		
	[user]
		name = your_username
		email = your_email
``` 		     

### If you want to create a repo via git, and then start to coding:

This is much easier.

* Go to [github](http://github.com) to create a new repo. (You probably want to create a readme and gitignore at the same time)
* Go to the folder where you want the repo sitting, and clone the repo

```
	cd your_folder
	git clone your_repo
```		
__DONE !__