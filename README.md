These are files that can be used to check your PHP code using PHP CodeSniffer. Code will be checked for coding standards, formatting, PHPDoc blocks, silly mistakes and more.

Developed under phpcs version 1.4.2.
Seems fine so far also under 1.4.2.

Installation
------------

1. Install phpcs:

        pear install PHP_CodeSniffer

2. Find your PEAR directory:

        pear config-show | grep php_dir

3. Copy, symlink or check out this repo to a folder called Snap inside the
   phpcs `Standards` directory:

        cd /path/to/pear/PHP/CodeSniffer/Standards
        git clone git@github.com:SnapInteractive/phpcs-standard.git Snap

4. Set Snap as your default coding standard:

        phpcs --config-set default_standard Snap

5. Profit!

        cd /path/to/my/project
        phpcs
        phpcs path/to/my/file.php

Editor integration
------------------

VIM

Add to your .vimrc:

    function! RunPhpcs()
        let l:filename=@%
        let l:phpcs_output=system('phpcs --report=csv '.l:filename)
        let l:phpcs_list=split(l:phpcs_output, "\n")
        unlet l:phpcs_list[0]
        cexpr l:phpcs_list
        cwindow
    endfunction
    set errorformat+=\"%f\"\\,%l\\,%c\\,%t%*[a-zA-Z]\\,\"%m\"\\,%*[a-zA-Z0-9_.-]\\,%*[0-9]
    command! Phpcs execute RunPhpcs()
    nmap <Leader>sn :call RunPhpcs()<cr>

This will allow you to run phpcs with the results in a Quickfix list by entering the command :Phpcs or \sn (mnemonic: sniff).

Alternatively you can try the Vim Syntastic plugin which will use phpcs automatically if it's in your PATH.
