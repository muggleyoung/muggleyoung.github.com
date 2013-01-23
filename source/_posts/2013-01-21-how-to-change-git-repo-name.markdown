---
layout: post
title: "how to change git repo name"
date: 2013-01-21 19:46
comments: true
categories: git
---
If you are not satisfy with your git repo name, you can easily change it.

* Log in [github](http://github.com) -> your repo -> settings
* Typing your new repo name, and "Rename" it
* Open terminal, go to your repo folder
* You have two ways to change your remote settings:

```
	git remote set-url origin git@github.com:muggleyoung/fog_city.git
```
OR

```
	vi .git/config
```
Change the remote url to your new repo url

__DONE !__
