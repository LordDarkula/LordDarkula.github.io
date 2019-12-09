---
layout:     post
title:      "3 More Tips and Tricks to Customize Your Terminal"
date:       2019-12-08 19:04:34
categories: programming
---

I'm back with a couple more terminal tips and tricks. Pull up your bash configuration file (`.bashrc` or `.bash_profile`) and lets get started.

## 1. Highlight tabs and trailing whitespace

One thing that plagued me when I started using vim regularly to write code was trailing whitespace. Due to misstypes, My code would always end up with some whitespace at the end of a line. This would inevitably drive both me and the style checker crazy as it kept complaining about whitespace I couldn't even see. This is how you highlight it for easy removal.
```bash
" Highlights spaces in grey. The autocmd BufEnter is needed so it works on every file at the same time when multiple files are open in the same pane.
highlight ExtraWhitespace ctermbg=white guibg=white
autocmd BufEnter * silent! match ExtraWhitespace /\s\+$/

" tabs highlighted in grey
highlight Tabs ctermbg=grey guibg=grey
autocmd BufEnter * silent! 2match Tabs /\t/
 ```
## 2. Multiple pane splitting
When I started using multiple vim panes with `sp:` and `vsp:`, There were two major annoyances I had. They were the location new vim panes would open, and having to press Control+W+W every time I wanted to switch between panes.
```bash
" remaps pane navigation to Control + (h,j,k,l)
nnoremap <C-J> <C-W><C-J>
nnoremap <C-K> <C-W><C-K>
nnoremap <C-L> <C-W><C-L>
nnoremap <C-H> <C-W><C-H>

" opens new panes below and to the right of currently open panes
set splitbelow
set splitright
```

