# VIM #

## Some links ##

[A Byte of Vim](http://www.swaroopch.com/notes/Vim_en-Programmers_Editor/)

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

### Python ###

[Official Vim documentation for Python](http://vimdoc.sourceforge.net/htmldoc/if_pyth.html)

