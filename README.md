# Froot -- A fake-root environment manager

**What is a fake-root?** Glad you asked. It is a directory under which the files
  are arranged in the same sub-directories as they are under the root of your
  file system. To give an example: if <code>/home/joe/froot</code> is the
  directory of the fake-root environment, then <code>/etc</code> is
  <code>/home/joe/froot/etc</code> inside the fake-root.

**Why have a fake-root?** Most of the files under '/' (root) except for those
  under '/home' are only writable by the 'root' user. This is for good reason
  because these files are concerned with the correct operation of your
  computer. However, if you are an advanced user and know what you are doing,
  then you are likely to want to edit some of these files. Usually this means
  running a text editor as the root user. This is fine as long as you are
  careful, however sometimes it can be all too easy to lose track of the changes
  you have made. This is not a problem as long as your system works, you may
  think, but it becomes a problem when you need to re-install because you will
  have forgotten the changes to get your system back to how you had it. This is
  where making the changes in a fake-root becomes very handy. The fake-root need
  only contain the files which you have edited. And because it can be under your
  home directory it is easy to backup and version control.

In a fake-root, files can be edited as you and the changes previewed before
copying them to your system's real root. The Froot automates many of the common
tasks.

Froot is a simple Bash script which you run from the command line; I use it with
GIT to sync my system config between my desktop and laptop.

## What can Froot do?

*  It uses a plain-text file <code>.froot</code> to list all the files in the
   fake-root.

*  Any files listed in the '.froot' file which are not in the fake-root can be
   'pulled-in' using the **pullin** command.

*  The **status** command shows a summary of the differences between the
   fake-root and the rest of the system and makes suggestions of the different
   Froot commands which can be performed.

*  The **diff** command shows a unified diff of the changes that would be made
   to the system when the changes in the fake-root are applied (using the
   'pushout' command). This includes any new files to be created, but not files
   to be removed because Froot doesn't remove files (you must do that yourself).

*  The **pushout** command applies the changes in the fake-root to the
   system. It first shows a diff and provides an opportunity to decline, unless
   the '--no-diff' option is given.

*  The **add** command adds files in the fake-root which are not listed in
   the '.froot' file, so that they become listed.

*  The **clean** command removes entries in '.froot' which arn't found on the
   system or in the fake-root.

The add and status commands ignore the files of all popular version control
systems. They also ignore all files in the root directory of the fake-root, so
this is a useful place to keep notes and any utility scripts.

TODO preserve chown and chmod

## READ ME FIRST

A .froot file must already exist in the root of the fake-root. Froot must be run
from the same directory which contains the .froot file.

## Example .froot file

The following is (most of) my .froot file for my Arch Linux system.

        /boot/grub/menu.lst
        /etc/fstab
        /etc/hosts
        /etc/inittab
        /etc/locale.gen
        /etc/mkinitcpio.conf
        /etc/modprobe.d/modprobe.conf
        /etc/ntpd.conf
        /etc/pacman.conf
        /etc/pacman.d/mirrorlist
        /etc/rc.conf
        /etc/slim.conf
        /etc/X11/xorg.conf
        /etc/yaourtrc
        /home/stepb/.bashrc
        /home/stepb/.emacs
        /home/stepb/.gitconfig
        /home/stepb/.gtkrc-2.0
        /home/stepb/.inputrc
        /home/stepb/.m2/settings.xml
        /home/stepb/.Xdefaults
        /home/stepb/.xinitrc
        /home/stepb/.xmobarrc
        /home/stepb/.Xmodmap
        /home/stepb/.xmonad/xmonad.hs
        /home/stepb/.xscreensaver

Be creative. I also have many sh scripts, but I removed these for
clarity. Actually, I use Froot for any files I have on my system which are not
managed by pacman (Arch Linux package manager).

## Froot TODO

-   Create a PKGBUILD for Arch Linux AUR.

-   Maybe rewrite in something more maintainable than bash.
