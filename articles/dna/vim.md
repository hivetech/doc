---
sidebar_current: "dna-vim"
---

Vim
===

General
-------

**Experimental** Giving a shot at [Vundle](https://github.com/gmarik/vundle).
Installation of Vundle itself and plugin is automatic thanks to [Erik
Zaadi](http://www.erikzaadi.com/2012/03/19/auto-installing-vundle-from-your-vimrc/).
Check `.vim/plugin/bundles.vim` to review the process and the plugin lists.

If present, `before.vimrc` and `after.vimrc` will be loaded.

Features
--------

* Automatic Vundle and plugins installation
* Autojump to last position when opening a file
* Template loading
* Tabs with MinibufExpl
* Persistent undo
* Leader key : ","
* Famous Solarized or Base16 color themes
* Airline status line
* Useful tlib and webapi libs installed
* Git diff show
* Powerfull semantic for search, substitution and abbrev
* Ruby on rails and bundle shortcuts
* Salstack files support


Keymaps
-------

* General

    * Help window            : \<F2\>
    * Back to normal mode    : ii
    * Save file              : ,w
    * (backward) search      : (\<ctrl\>+)\<space\>
    * Remove highlight       : //
    * New file               : ,N
    * Toggler spell checking : ,ss
    * Move to current dir    : ,cd
    * Copy to clipborad      : \<C-c\>
    * Paste to clipboard     : \<C-v\>
    * Ctrlp files list       : ,v
    * Ctrlp tags             : \<CR\>
    * Window split           : {ss,vv}
    * Source .vimrc          : ,vr
    * Undo tree              : ,u
    * Nerdtree window        : \<F4\>
    * Buffers window         : ,yr
    * Save as sudo           : :w!!
    * Better iabbrev         : :Abolish {despa,sepe}rat{e,es,ed,ing,ely,ion,ions,or}  {despe,sepa}rat{}
    * Better search          : :Subvert/di{e,ce}/spinner{,s}/g

* Dev

    * Trigger make                       : \<F5\>
    * Trigger make run                   : \<F12\>
    * Manage debug window                : ,{o,n,p,c}
    * Toggle between header/source files : ,h
    * Surround the word with {character} : ,{character}
    * adds ; at the end of the line      : ;;
    * puts the cursor after last "       : \<C-a\>
    * opens a gitgrep line               : ,gg
    * Align on {character}               : \<C-A\>{character}
    * {sexy,normal} toogle comments      : ,c{s,\<space\>}
    * opens tagbar                       : \<F3\>
    * align lines on {character}         : \<Ctrl-a\>{character}
    * opens tasks list                   : ,t
    * opens git dirty files              : ,ocf
    * Open a window with {ipython,bash,zsh,mysql,node,irb,R} prompt : ,t{y,b,z,s,n,i,r}
    * Go to {next,previous} git change   : g{h,H}
    * <C-x><C-o>                         : Completion menu for go code

* Move

    * 4 lines {forward,backward} : \<C-{e,y}\>
    * Navigate buffers           : {right,left} arrow
    * Navigate windows           : {up,down} arrow

* LaTex

    * Compile the current file   : ,ll
    * Omnicompletion             : <C-x><C-o>



Plugins
-------

* Vundle - [the plug-in manager for Vim](https://github.com/gmarik/vundle)
* Fugitive - [a Git wrapper so awesome, it should be illegal ](https://github.com/tpope/vim-fugitive)
* Syntastic - [Syntax checking hacks for vim](https://github.com/scrooloose/syntastic)
* Solarized - [Precision colorscheme for the vim text editor](https://github.com/altercation/vim-colors-solarized)
* Delimitmate - [Vim plugin, provides insert mode auto-completion for quotes, parens, brackets, etc](https://github.com/Raimondi/delimitMate)
* Base 16 - [Color schemes for hackers](https://github.com/chriskempson/base16-vim)
* Ctrlp - [Fuzzy file, buffer, mru, tag, etc finder](https://github.com/kien/ctrlp.vim)
* Gundo - [Graph your vim undo tree in style](http://sjl.bitbucket.org/gundo.vim/)
* Conque-Shell - [Run interactive commands inside a Vim buffer](https://github.com/vim-scripts/Conque-Shell)
* Minibufexpl - [Elegant buffer explorer - takes very little screen space](http://fholgado.com/minibufexpl)
* NerdCommenter - [Vim plugin for intensely orgasmic commenting](https://github.com/scrooloose/nerdcommenter)
* NerdTree - [A tree explorer plugin for vim](https://github.com/scrooloose/nerdtree)
* NerdTree-tabs - [NERDTree and tabs together in Vim, painlessly](https://github.com/jistr/vim-nerdtree-tabs)
* Vim-snipmate - [default snippets](https://github.com/honza/vim-snippets)
* Tabular - [Vim script for text filtering and alignment](https://github.com/godlygeek/tabular)
* Tagbar - [Vim plugin that displays tags in a window, ordered by class etc](http://majutsushi.github.io/tagbar/)
* TaskList - [Eclipse like task list](https://github.com/vim-scripts/TaskList.vim)
* Template - [Simple templates plugin for Vim](https://github.com/aperezdc/vim-template)
* Tlib - [Some utility functions for VIM](https://github.com/tomtom/tlib_vim)
* WebAPI - [vim interface to Web API ](https://github.com/mattn/webapi-vim)
* YankRing - [Maintains a history of previous yanks, changes and deletes ](https://github.com/vim-scripts/YankRing.vim)
* Airline - [lean & mean status/tabline for vim that's light as air](https://github.com/bling/vim-airline)
* Gitgutter - [A Vim plugin which shows a git diff in the gutter (sign column)](https://github.com/airblade/vim-gitgutter)
* Abolish - [easily search for, substitute, and abbreviate multiple variants of a word](https://github.com/tpope/vim-abolish)
* Rails - [Ruby on Rails power tools](https://github.com/tpope/vim-rails)
* Bundler - [Lightweight support for Ruby's Bundler](https://github.com/tpope/vim-bundler)
* Vim-gocode - [A Go bundle for Vundle or Pathogen](https://github.com/Blackrush/vim-gocode)
* LaTex-Box - [Lightweight Toolbox for LaTeX](https://github.com/LaTeX-Box-Team/LaTeX-Box)
* YouCompleteMe - [A code-completion engine for Vim](https://github.com/Valloric/YouCompleteMe)
* Salt-vim - [Vim files for editing Salt files](https://github.com/saltstack/salt-vim)

---
##### last modified on: April 29, 2014
---
