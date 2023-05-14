---
layout: post
title:  "macOS Setup Giude"
date:   2022-12-28
title_include: true
categories: blog
image_url: ""
---

<style>body {text-align: justify}</style>

## MacOs Setup Guide

This writing covers some installations and envrironments that are important to set up even if you dont use them at all because play a pivotal role some command-line tools. I have been using macbook Pro for a while since macOS Sierra up untill macOS monterey and find that it is quite stable. Personally, I would not be upgrading to any further OS installation from Apple as I feel Ventura essentially doesn't let one differentiate between an iPhone and a macbook, interface wise. But again, I would like to reiterate that it is personal perference for not upgrading any further and I am not against any OS.

After a long usage of you mac over months, especially after extensive use of Docker and working with containers, you will find that your mac is running out of space. This is because Docker stores all the images and containers in a hidden folder in your home directory, which is not visible in Finder and quite frankly it is not a good idea to delete them manually. Therefore, every 4 to 5 months, I would recommend you to format your mac and reinstall macOS. This will give you a fresh start and will also free up some space on your mac. 

<figure>
<img src="/assets/img/macOS-setup-guide/first-time.jpg" width=500 style="display: block; margin: 0 auto">
</figure>

It is a good idea to have a fresh installation of macOS on your Mac. So there are two ways of going about it. <br/>

&nbsp; &nbsp; &#8226; You can do this by booting into recovery mode and reinstalling macOS. This will remove all the files and applications from your Mac and will give you a fresh start.

&nbsp; &nbsp; &#8226; You can also do this by formatting your Mac and then installing macOS from a bootable USB. You can find the instructions for this [here](https://support.apple.com/en-us/HT201372). 

## Installing Homebrew

{% marginfigure 'mf-id-1' 'assets/img/macOS-setup-guide/homebrew.png' ''  %}

Homebrew calls itself *the missing package manager* for macOS and is an essential tool for any developer. To use Homebrew, ensure that you have installed the Command Line Tools for Xcode. These tools, which include compilers and other necessary components for building from source. You can also install them directly from the terminal using the following command.

```bash
xcode-select --install
```
And then install Homebrew using the following command.
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
After installing Homebrew, you can run the following command to check if everything is working fine.
```bash
brew doctor
```

You can use Homebrew to install a variety of software, including command-line tools like Git and languages like Node.js. To see what you can install with Homebrew, you can run the following command.
```bash
brew install <formula>
```
And to update Homebrew itself, you can run the following command.
```bash
brew update
brew upgrade <formula>
```
To get rid of older versions of formulas installed on your system, in case you want to roll back to an older version. So you can do some cleanup to get rid of those old versions by:
```bash
brew cleanup
```
To uninstall a formula, you can run the following command.
```bash
brew uninstall <formula>
```
### Homebrew Cask
Homebrew Cask extends Homebrew and brings its elegance, simplicity, and speed to the installation and management of GUI macOS applications such as Visual Studio Code and Google Chrome. This is done by providing a friendly CLI workflow for the administration of macOS applications distributed as binaries. So, you need not drag and drop those `.dmg` files to your Applications folder.
To know if an application is available on Cask, one must refer to the [Official Cask Formulae](https://formulae.brew.sh/cask/) page. 

One can also search for an application using brew. To search an application, you can run the following command.
```bash
brew search <application>
```

## iTerm2

{% marginfigure 'mf-id-2' 'assets/img/macOS-setup-guide/iTerm2.png' ''  %}

<!-- Some developers cringe at the mere thought of opening a terminal window. For the uninitiated it can be daunting, stressful, and downright annoying. But devs who understand the command line would argue it’s one of the best tools at your disposal. — Jake Rocheleau -->

iTerm2 is a replacement for Terminal and the successor to iTerm. It works on Macs with macOS 10.14 or newer. iTerm2 brings the terminal into the modern age with features you never knew you always wanted. It has some powerful features that make it the perfect choice for developers. 

You can see the features from [here](https://iterm2.com/features.html) but some of the features that I like are: `Search`,   `Autocomplete`, `24-Bit Color`, `Configurability` and many more. You can use Homebrew to install iTerm2 using the following command.
```bash
brew install --cask iterm2
```

### Customizations
Here are some of the customizations that I have done to my iTerm2, they are optional and you can skip them if you want. <br/>

&nbsp; &nbsp; &#8226; Go to iTerm preferences -> profiles -> Default -> Terminal -> Check silence bell or not, depending on how you like it. <br/>
&nbsp; &nbsp; &#8226; Download one of [iTerm2 color schemes](https://github.com/mbadolato/iTerm2-Color-Schemes/tree/master/schemes) and then set it to your default profile by navigating to profile -> colors -> color presets -> import. <br/>
&nbsp; &nbsp; &#8226; Change the cursor text and cursor color according to your theme to make it more visible. I personally use the inbuilt theme of `Tango Dark` with their default colors. <br/>
&nbsp; &nbsp; &#8226; You can also change the font of your terminal to make it more readable. I personally use `Monaco` with ligatures enabled. You can download fonts using [Homebrew](https://github.com/Homebrew/homebrew-cask-fonts) using the following command:
```bash
brew tap homebrew/cask-fonts && brew install --cask font-<font-name>
```
&nbsp; &nbsp; &#8226; You can also change the transparency of your terminal to make it more appealing. <br/>
&nbsp; &nbsp; &#8226; Tree is a recursive directory listing command that produces a depth indented listing of files, which is colorized ala dircolors if the LS_COLORS environment variable is set and output is to tty. You can install tree using Homebrew using the following command.
```bash
brew install tree
```
and then use `tree` command to see the directory structure.
```bash
(base) ➜  ~ cd Desktop/py-pg
(base) ➜  py-pg tree
.
├── Pandas Serial Execution.ipynb
├── Why python ?
│   ├── CODING PATTERNS TO IDENTIFY IN PROBLEMS .pdf
│   └── PYTHON INTERVIEW QUESTIONS👉.pdf
├── hello.py
├── twoSum.py
├── uc3_multithreading.py
├── uc4_multithreading.py
├── uc5_multithreading.py
└── uc6_multithreading.py

2 directories, 9 files
(base) ➜  py-pg
```
### Oh-my-zsh Shell
Zsh, short for the Z shell, is a Unix shell that enhances the default bash shell on macOS with extra functionalities. It is advisable to choose zsh instead of bash and consider installing a framework for a better experience in managing configuration, plugins, and themes. Install `zsh` using Homebrew using the following command.
```bash
brew install zsh
```
Now, we should install `Oh-My-Zsh` which is an open-source framework for managing zsh configuration. It comes bundled with a ton of helpful functions, helpers, plugins, and themes. The configuration file for zsh is called `.zshrc` and resides in your home folder as `(~/.zshrc)`. 

<figure>
<img src="/assets/img/macOS-setup-guide/omz.png" width=500 height=300 style="display: block; margin: 0 auto">
</figure>

You can install `Oh-My-Zsh` using the following command.
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```


