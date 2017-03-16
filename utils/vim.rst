
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

