# VIM #

## Some links ##

[A Byte of Vim](http://www.swaroopch.com/notes/Vim_en-Programmers_Editor/)

[Vim Commands Cheat Sheet](http://bullium.com/support/vim.html)

## One-liners ##

Jump to next or previous empty line :

```
}
{
```

Delete spaces at end of line :

```
s/[[:space:]]\+$//
```

Save Vim session into a file, containing all buffers and tabs :

```
:mksession /tmp/vim_session.vim
```

Restore session :

```
vim -S /tmp/vim_session.vim
```

## Plugin development ##

### Documentation ###

~~~~~
:help vim-script-intro
~~~~~

Book : _Hacking Vim_ - Kim Schulz

### Python ###

[Official Vim documentation for Python](http://vimdoc.sourceforge.net/htmldoc/if_pyth.html)

Ultra basic example :

```
function! Hellovim()
python <<EOF
import vim
vim.command("vnew")
vim.current.buffer[0] = "Hello Vim !"
EOF
endfunction

call Hellovim()
```

Save the content into a file `example.vim`, then run :

```
:source example.vim
```

