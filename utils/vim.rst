
===
VIM
===

Features to masterize
=====================
- Tags (tagsrch.txt)
- Syntax highlighting
- Indent
- Managing buffers, windows, and tabs
- Motion
- Mapping
- Undo
- Folding
- Auto-doc
- Auto-import
- Completion

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

Assign / display variable : ::

    let var="varcontent"
    echo var

Plugins
=======

Useful plugins : ::

    cd ~/.vim/bundle/
    # File explorer
    git clone https://github.com/scrooloose/nerdtree
    # Mini Buf Explorer
    git clone https://github.com/fholgado/minibufexpl.vim.git
    # Git integration
    git clone https://github.com/tpope/vim-fugitive.git>
    # CTRLP
    git clone https://github.com/kien/ctrlp.vim
    # Python Mode
    git clone https://github.com/klen/python-mode

    # Python doc
    git clone https://github.com/fs111/pydoc.vim.git
    # Vim config for git
    git clone https://github.com/tpope/vim-git.git
    # Tab for completion
    git clone https://github.com/ervandew/supertab
    # Comment easily
    git clone https://github.com/scrooloose/nerdcommenter.git

Other :

- `YouCompleteMe - A code-completion engine for Vim <https://github.com/Valloric/YouCompleteMe>`_
- `Gundo - Graph your Vim undo tree in style <https://github.com/sjl/gundo.vim>`_
- `Syntastic - Syntax checking hacks for vim <https://github.com/scrooloose/syntastic>`_
- `Pandoc syntax <https://github.com/vim-pandoc/vim-pandoc.git>`_
- `Align data <https://github.com/vim-scripts/Align>`_
- `XML completion <https://github.com/othree/xml.vim.git>`_
- `Manage complex undo <https://github.com/mbbill/undotree.git>`_
- `ack-grep integration <https://github.com/mileszs/ack.vim>`_

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

