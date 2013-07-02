.gitconfig
==========

Algumas configurações para o gitconfig

    [user]
        name = Danilo Shiga
        email = daniloshiga@gmail.com

    [diff]
        tool = vimdiff
    [difftool]
        prompt = false
    [alias]
        a = add
        d = difftool
        st = status -sb
        ci = commit -v
        br = branch
        co = checkout
        df = diff -w --word-diff
        lg = log -p
        lol = log --graph --decorate --pretty=oneline --abbrev-commit
        lola = log --graph --decorate --pretty=oneline --abbrev-commit --all
    [color]
        branch = auto
        diff = auto
        interactive = auto
        status = auto
        ui = 1
    [core]
        editor = vim
        excludesfile = /home/drshiga/.gitignore
    [help]
        autocorrect = 1
    [push]
        default = matching
