
===
VIM
===

Web ressources
==============

`A Byte of Vim <http://www.swaroopch.com/notes/Vim_en-Programmers_Editor/>`_

`Vim Commands Cheat Sheet <http://bullium.com/support/vim.html>`_

One-liners
==========

Jump to next or previous empty line : ::

    }
    {

Delete spaces at end of line : ::

    s/[[:space:]]\+$//

Save Vim session into a file, containing all buffers and tabs : ::

    :mksession /tmp/vim_session.vim

Restore session : ::

    vim -S /tmp/vim_session.vim

Convert Textile links into RST links : ::

    s/\v\[(.*)\]\((.*)\)/`\1 <\2>`_/

Edit field value enclosed by double quotes : ::

    ci"

Plugins
=======

Useful plugins :

- `File explorer <https://github.com/scrooloose/nerdtree>`_
- `Git integration <https://github.com/tpope/vim-fugitive.git>`_
- `Pandoc syntax <https://github.com/vim-pandoc/vim-pandoc.git>`_
- `Align data <https://github.com/vim-scripts/Align>`_
- `XML completion <https://github.com/othree/xml.vim.git>`_
- `Manage complex undo <https://github.com/mbbill/undotree.git>`_
- `Python doc <https://github.com/fs111/pydoc.vim.git>`_
- `Run syntax checks <https://github.com/klen/python-mode>`_
- `Vim config for git <https://github.com/tpope/vim-git.git>`_
- `ack-grep integration <https://github.com/mileszs/ack.vim>`_
- `Tab for completion <https://github.com/ervandew/supertab>`_
- `Comment easily <https://github.com/scrooloose/nerdcommenter.git>`_

Probably useful but not personally tested :

- `CTRLP - Fuzzy file, buffer, mru, tag, etc finder <https://github.com/kien/ctrlp.vim>`_
- `YouCompleteMe - A code-completion engine for Vim <https://github.com/Valloric/YouCompleteMe>`_
- `Gundo - Graph your Vim undo tree in style <https://github.com/sjl/gundo.vim>`_
- `Syntastic - Syntax checking hacks for vim <https://github.com/scrooloose/syntastic>`_
- `Python-mode - Vim python-mode. PyLint, Rope, Pydoc, breakpoints from box <https://github.com/klen/python-mode>`_

Useful links for development :

- `Turning Vim into a modern Python IDE <http://sontek.net/blog/detail/turning-vim-into-a-modern-python-ide>`_
- `My Development Environment For Python <http://www.jeffknupp.com/blog/2013/12/04/my-development-environment-for-python/>`_

pydoc
-----
https://github.com/fs111/pydoc.vim/blob/master/ftplugin/python_pydoc.vim

View the documentation of the ``os.path`` module : ::

    :Pydoc os.path

Search the documentation for the word ``import`` : ::

    :PydocSearch import

View the documentation for the word under the cursor : ::

    <Leader>pw

View the documentation for the WORD under the cursor : ::

    <Leader>pW

Plugin development
==================

Documentation
-------------

Tutorial : ::

    :help vim-script-intro

Book : *Hacking Vim* - Kim Schulz

Python
------

`Official Vim documentation for Python <http://vimdoc.sourceforge.net/htmldoc/if_pyth.html>`_

Ultra basic example : ::

    function! Hellovim()
    python <<EOF
    import vim
    vim.command("vnew")
    vim.current.buffer[0] = "Hello Vim !"
    EOF
    endfunction

    call Hellovim()

Save the content into a file ``example.vim``, then run : ::

    :source example.vim

