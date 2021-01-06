# How to transfer your Arch\Manjaro installation to another machine

HOWTO from [here](https://classicforum.manjaro.org/index.php?topic=16484.0)

On your old machine, do:

1.  Back up the list of currently installed packages from the standard repositories:

        '''bash
        pacman -Qqen > pkglist-repo.txt
        '''

2.  Back up the list of currently installed packages from the AUR:

        ```bash
        pacman -Qqem > pkglist-aur.txt
        ```

On the other/new machine:

1.  Reinstall from list - repository:

        ```bash
        sudo su
        ```

        ```bash
        for x in $(cat pkglist-repo.txt); do pacman -S --needed $x; done
        ```

2.  Reinstall from list - AUR:

        '''bash
        yaourt -S --needed --noconfirm $(< pkglist-aur.txt)
        '''

> If there are many packages to build, you'll have to re-suppy your password
> again because sudo will time out. The process will just stall, but not stop.
> However, this part may indeed fail to build some packages if the available
> versions are for some reason out of date.
>
> Also, it will fail right at the start if some packages you had installed are
> no longer available!
>
> This happened to me for two packages.
>
> Solution: remove those from the list by editing it.
>
> If one package fails to build, the whole process will end and you'll need to
> restart the process by runing that same command again (possibly after removing
> the broken package from the list).
