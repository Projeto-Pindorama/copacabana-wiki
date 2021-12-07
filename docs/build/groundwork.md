# Laying the groundwork

In this section, we're going to lay the groundwork to start compiling Copacabana
Linux. Its procedures are similar to how Linux from Scratch is built, but with
remarkable differences (and errors) between them.  
To be honest, trying to compile it is a pretty infuriating experience ---
principally if you have a slow machine.  

## Preparing the host system

### Installing needed packages

In case of Arch Linux, the most part of the packages are already installed, but
we will update them. About the kernel: if you have `linux-lts`, update it; if
not, update your kernel variant.    
Copacabana, in other hand, has all these packages or installed into the base
system (such as star or ksh93) or in separated stages, as said before.  

=== "Arch Linux"

    ```console
    fulano@arch-workstation:~$ doas pacman -Syuv linux-lts base-devel util-linux \
				gcc coreutils diffutils findutils patch gawk grep \
				glibc bash ksh python m4 bzip2 pigz xz curl 
    ```
=== "Copacabana"

    ```console
    workstation%; whoami
    fulano 
    workstation%; echo "TODO"
    ```

#### Installing Pindorama packages 

In case of the two Pindorama packages --- Mitzune and L.E.mount --- installing them is
pretty straightfoward, since they're just tarball containing files to be placed
exacty in your \*NIX file system layout.  
**Note**: It's not availiable as formal packages for any Linux distributions nor
as recipes (eg.: AUR) mostly because --- except in case of Mitzune, which uses an
odd packaging format, installing in the `~` and not in the root --- I don't have
patience for it.  

As said in Mitzune's documentation, it needs to be installed in the `~`
directory, since it's designed to be installed as an user-local script.  
This command line below will download it and unpackage it directly to your `~`
directory.  
If `$HOME/.local/bin` isn't on your `$PATH`, remember to set it up.  
**Note**: do this using your own user, not `root` nor `baggio` (we will
talk about him later on).  

```console
workstation%; curl https://get.pindorama.dob.jp/mitzune/releases/mitzune.0.1.NOARCH.Linux.tar.xz -L --output - | xz -cd - | tar -xvf - -C ~/
```

In other hand, L.E.mount needs to be installed in the root file system.  
For installing it, we will use this command line below, that does the same 
thing that the command line above, with the exception of making use of `doas`
and unpackaging into the root file system. You also could run it directly as
`root` (a.k.a `su -c`), but it isn't the safest thing in the world.   

```console
workstation%; curl https://get.pindorama.dob.jp/lemount/releases/lemount-0.1-b.NOARCH.Copacabana.tar.xz -L --output - | xz -cd - | doas tar -xvf - -C /
```

After installing everything, exit your Shell and fire it up again, so the
`$PATH` will be re-cached and the new binaries indexed.   

### Creating the virtual disk image

### Entering `root`

#### Creating an unprivileged user (just for this)
