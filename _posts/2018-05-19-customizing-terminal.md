---
layout: post
title:  "3 Tips and Tricks to Customize Your Terminal"
date:   2018-05-19 13:30:15
categories: programming
---

In order to customize your terminal prompt, you must edit (create if it doesn't exist),
a `.bashrc` (on linux) or `bash_profile` (on macOS) file in your home directory. 


## 1. Differentiate between macOS and linux

To reuse the same bash configuration file on macOS and Linux,
sometimes it is necessary to differentiate between the two operating systems.
For example, enabling colors in terminal differs in both operating systems.
This is how you do it.
```bash
# Changing colors in macOS and linux
if [[ "$OSTYPE" = *"linux-gnu"* ]]; then
    # Linux code here
    force_color_prompt=yes
elif [[ "$OSTYPE" = *"darwin"* ]]; then
    # MacOS code here
    export CLICOLOR=1
    export LSCOLORS=GxFxCxDxBxegedabagaced
fi
```

## 2. Remove the bell sound

When you press the backspace key at the start of a line, your computer will make an
audible beep sound. To turn it off, create a file called `.inputrc` in 
your home directory. Add the following to the file.
```bash
# Silences terminal
set bell-style none
```

## 3. Set Default text editor

Some programs (such as git) automatically open a text editor when you need to
edit something. In order to change that editor, add the following line to your bash
configuration.
```bash
# Substitute path to your editor (such as /usr/bin/vim)
export EDITOR=<PATH_TO_YOUR_EDITOR>
```
