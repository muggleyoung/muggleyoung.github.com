---
layout: post
title: "Version Control .vim File With Git"
date: 2013-03-27 22:45
comments: true
categories: git
---

_We usually have lots of vim plugins installed, and custermized configrations. It is better to version control .vim, .vimrc, even .gvimrc. So that we can easily set the configration on different laptop, also as a backup :)_

**如何使用github管理vim配置文件？**

如果仅使用git管理.vim目录，你会发现提交之后的版本库中，每个插件都是不可用的，也无法完全pull下来。那是因为插件目录本身也是一个git的版本库。对于这样的情况，需要使用git submodel来进行配置。

I will introduce solutions for my case first.

* I have [Pathogen.vim](https://github.com/tpope/vim-pathogen) installed, so in my .vim directory, there should be a "/bundle" dir.
* I've already have several plugins installed
* I inited my .vim as a git repo 

##### Add plugins as git submodule

1. Remove git index for your plugins

	Because the .vim is a git repo now, so all the installed plugins is already staged in git. So we need to remove them first.

	You can try this first:

	```
	git ls-files --stage plugin_folder
	```
	
	If you can see something like this
	
	```
	160000 d00cf29f23627fc54eb992dde6a79112677cd86c 0 plugin_folder
	```
	
	That means the repo in plugin_folder has been added as "gitlink" already. So run following command to remove them from index:
	
	```
	git rm --cached plugin_folder
	```
	
2. Add plugins as a git module

	e.g. I have a [nerdTree](https://github.com/scrooloose/nerdtree) installed, and about to add its folder as submodule.
	
	```
	git submodule add https://github.com/scrooloose/nerdtree.git bundle/nerdTree
	```
	
	Make a commit
	
	```
	git add .
	git ci -m "add nerdTree as git submodule"
	```
	
3. Do step1, step2 for your other plugin dirs


##### Script to do things as above, for lazy guys and who already has lots of plugins installed

** 在[邱大师](http://icodeit.org/)的帮助下，我们还有对于懒人和装了N多插件的同学的脚本！**

###### 1.Goto your .vim directory

```
cd ~/.vim
```

###### 2. Create a script file, and copy the following commands:

```
#!/bin/bash
git rm -r --cached bundle
find ./bundle/ -name config | xargs grep 'url' | awk -F= '{print $2}' | awk -F/ '{printf("git submodule add %s bundle/%s\n", $0, $NF)}' | sed 's/\(.*\).git/\1/g' >script
chmod +x script
./script
rm script
```

I've updated the script in my [.vim repo](https://github.com/muggleyoung/vimrc). You can download the script from here: <https://github.com/muggleyoung/vimrc/blob/master/sync_git.sh>

** Note: **

 In this script, we first remove the staged plugins from git, then run the "git submodule add …" command for all the existing plugin folders.

**So it is important to make sure the script is created under ./vim folder. **

###### 3. Then you can make your own commit and push


##### We can also add .vimrc and .gvimrc into our repo, by make them as symbolic link

1. Move .vimrc and .gvimrc files to .vim directory
	
	```
	mv .vimrc ~/.vim/vimrc
	mv .gvimrc ~/.vim/gvimrc
	```
	
2. Create symbolic links for them

	```
	ln -s ~/.vim/vimrc ~/.vimrc
	ln -s ~/.vim/gvimrc ~/.gvimrc
	```

	So that the ~/.vimrc points to ~/.vim/vimrc

3. Of course we need to add another commit as well


**Check your repo now, it should all work!**

-----------------------------------------------------------------------------
##### If you just start to install plugins, you can do as following:

1. Init .vim as a git repo;
2. Install [Pathogen.vim](https://github.com/tpope/vim-pathogen);
3. Install plugins as submodule:

	```
	cd ~/.vim
	mkdir ~/.vim/bundle
	git submodule add plugin-repo-url
	```

4. Add .vimrc and .gvimrc into your repo, and make a commit.
