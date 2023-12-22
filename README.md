![Obsidian](https://img.shields.io/badge/Obsidian-%23483699.svg?style=for-the-badge&logo=obsidian&logoColor=white)
![https://vii33.medium.com/](https://img.shields.io/badge/Medium-12100E?style=for-the-badge&logo=medium&logoColor=white)
![https://twitter.com/vii33_official](https://img.shields.io/badge/Ask%20me-anything-1abc9c.svg)



![Header Image](readme-images/Header.jpg)

# Obsidian .vimrc Jumpstart File

## Background
Vim is a [brilliant language](https://www.youtube.com/watch?v=XfJBvgnCeBk) to efficently manage and navigate in structured pieces of text. With the Obsidian editor this build a nice synergy, because  Obsidian notes consists out of larger markdown chunks. Therefore,obsidian has [native Vim support](https://publish.obsidian.md/hub/04+-+Guides%2C+Workflows%2C+%26+Courses/for+Vim+users).

To further enhance Vim capabilities in Obsidian, esm7 has build the [vimrc plugin](https://github.com/esm7/obsidian-vimrc-support), based on CodeMirror, to store Vim configurations in `.obsidian.vimrc` files.

## `.obsidian.vimrc`
The following code is my `.obsidian.vimrc` base file, which you can use to get a jumpstart.

If you need to use internal Obsidian command bindings, check out the [Obsidian commands](Obsidian_commands.md) file.


```vim
" See here for available codemirror operators/motions: (until about line 200) - https://github.com/replit/codemirror-vim/blob/master/src/vim.js
" To see available internal Obsidian commands, go to developer console, click in the editor, type :obcommand and check log output 

" Have j and k navigate visual lines rather than logical ones
nmap j gj
nmap k gk

" Big J/K jumps multiple lines (compared to their smaller siblings j/k)
" To be able to remap keys, they need to be unmapped first
nunmap J
nmap J 15j 
nunmap K
nmap K 15k 

" Join Lines with space+j (Space is my leader key)
" unmap space for leader key usage first
" commands like :join can be found on above given link
unmap <Space>
map <Space>j :join

" Escape insert mode more easily (quickly press jj )
imap jj <Esc> 

" H and L for beginning/end of line (big variants of h & l)
nmap H ^
nmap L $

" Quickly remove search highlights
nmap <F9> :nohl

" Yank to system clipboard
set clipboard=unnamed

" go to last change - https://vimhelp.org/motion.txt.html#g%3B
nmap g, u<C-r>

" [g]oto [f]ile (= Follow Link under cursor)
exmap followLinkUnderCursor obcommand editor:follow-link
nmap gf :followLinkUnderCursor

" Emulate Folding https://vimhelp.org/fold.txt.html#fold-commands
exmap togglefold obcommand editor:toggle-fold
nmap zo :togglefold
exmap unfoldall obcommand editor:unfold-all

nmap zR :unfoldall
exmap foldreduce obcommand editor:fold-less
nmap zr :foldreduce

exmap foldall obcommand editor:fold-all
nmap zM :foldall
exmap foldmore obcommand editor:fold-more
nmap zm :foldmore


"--- PLUGINS ---"

" Surround plugin keymaps (other plugins don't work)
" usage: either mark word in visual mode or go over word in normal mode
" these lines create new commands which are then used in the bottom
exmap surround_wiki surround [[ ]]         
exmap surround_double_quotes surround " "
exmap surround_single_quotes surround ' '
exmap surround_backticks surround ` `
exmap surround_brackets surround ( )
exmap surround_square_brackets surround [ ]
exmap surround_curly_brackets surround { }

" NOTE: must use 'map' and not 'nmap'
map [[ :surround_wiki
nunmap s
vunmap s
map s" :surround_double_quotes
map s' :surround_single_quotes
map s` :surround_backticks
map sb :surround_brackets
map s( :surround_brackets
map s) :surround_brackets
map s[ :surround_square_brackets
map s[ :surround_square_brackets
map s{ :surround_curly_brackets
map s} :surround_curly_brackets

" Go to daily note (needs daily note plugin)
exmap godailynote obcommand daily-notes
nmap <Space>gd :godailynote

```