# CentOS 6.9

For HPCC in NJU

[TOC levels=1-3]: # " "

- [CentOS 6.9](#centos-69)
- [Change the Home directory](#change-the-home-directory)
- [Upgrade gcc](#upgrade-gcc)
- [Install Linuxbrew](#install-linuxbrew)
- [Mirror to remote server](#mirror-to-remote-server)


```bash
usermod -aG wheel wangq
```

Or use `visudo`.

# Change the Home directory

`usermod` is the command to edit an existing user. `-d` (abbreviation for `--home`) will change the
user's home directory. Adding `-m` (abbreviation for `--move-home` will also move the content from
the user's current directory to the new directory.

```bash
mkdir -p /share/home
usermod -m -d /share/home/wangq wangq
```

# Upgrade gcc

```text
$ cat /etc/centos-release
CentOS release 6.7 (Final)

$ sudo yum install centos-release-scl
$ sudo yum install devtoolset-3-toolchain
$ scl enable devtoolset-3 bash

$ gcc --version
gcc (GCC) 4.9.2 20150212 (Red Hat 4.9.2-6)

```

# Install Linuxbrew

Enable the SCL environment:

```bash
scl enable devtoolset-3 bash
```

Install Linuxbrew:

```bash
git clone https://github.com/Linuxbrew/brew.git ~/.linuxbrew
```

Add these to your `.bashrc`, and source it:

```bash
export PATH="$HOME/.linuxbrew/bin:$PATH"
export MANPATH="$HOME/.linuxbrew/share/man:$MANPATH"
export INFOPATH="$HOME/.linuxbrew/share/info:$INFOPATH"
```

Create symlinks to your new gcc/g++/gfortran:

```bash
ln -s $(which gcc) `brew --prefix`/bin/gcc-$(gcc -dumpversion | cut -d. -f1,2)
ln -s $(which g++) `brew --prefix`/bin/g++-$(g++ -dumpversion | cut -d. -f1,2)
ln -s $(which gfortran) `brew --prefix`/bin/gfortran-$(gfortran -dumpversion | cut -d. -f1,2)
```

Test your installation:

```bash
brew install hello
brew test hello
brew remove hello
```

Some packages have building problems, use bottled or from-source versions.

**Don't `brew install git`**

```bash
brew install --force-bottle gawk
brew install --force-bottle glib
brew install --force-bottle fontconfig
brew install --without-x11 cairo
brew install r # 3.4.3
brew install --force-bottle graphviz
brew install --force-bottle imagemagick
brew install --force-bottle hdf5

brew reinstall --build-from-source lua

brew reinstall --build-from-source lua@5.1
brew reinstall --build-from-source libtiff
brew reinstall --build-from-source --without-webp gd # broken, can't find libwebp.so.6
brew reinstall --build-from-source gnuplot@4 --without-lua@5.1
brew unlink gnuplot
brew link gnuplot@4 --force

brew install --build-from-source oniguruma
brew install --build-from-source jq

brew install --build-from-source htslib
brew install --build-from-source samtools

brew install --build-from-source raxml

```

# Mirror to remote server

```bash
rsync -avP ~/.linuxbrew/ wangq@202.119.37.251:.linuxbrew
rsync -avP ~/share/ wangq@202.119.37.251:share
rsync -avP ~/bin/ wangq@202.119.37.251:bin
rsync -avP ~/.bashrc wangq@202.119.37.251:.bashrc

```

