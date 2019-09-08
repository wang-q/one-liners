# CentOS 6.9

For HPCC in NJU

[TOC levels=1-3]: # " "

- [CentOS 6.9](#centos-69)
- [Change the Home directory](#change-the-home-directory)
- [Upgrade gcc](#upgrade-gcc)
- [Install Linuxbrew](#install-linuxbrew)
- [Mirror to remote server](#mirror-to-remote-server)

# Install

```bash
wget -N https://mirrors.nju.edu.cn/centos-vault/6.10/isos/x86_64/CentOS-6.10-x86_64-minimal.iso

```

Let Parallels use the express installation. Configure the VM as 4 cores and 4GB RAM.

Turn Network Conditioner on and ssh in as `root`.

# Change the Home directory

`usermod` is the command to edit an existing user. `-d` (abbreviation for `--home`) will change the
user's home directory. Adding `-m` (abbreviation for `--move-home` will also move the content from
the user's current directory to the new directory.

```bash
pkill -KILL -u wangq

# Change the Home directory
mkdir -p /share/home
usermod -m -d /share/home/wangq wangq

# Development Tools
yum groupinstall 'Development Tools'
yum install curl file git vim

```

# Install Linuxbrew without sudo

* SSH in as `wangq`

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"

# can't sudo
# Ctrl+D to install linuxbrew to PATH=$HOME/.linuxbrew
# RETURN to start installation

echo >> ~/.bashrc
echo '# HOMEBREW' >> ~/.bashrc
echo 'eval $(/share/home/wangq/.linuxbrew/bin/brew shellenv)' >> ~/.bashrc
echo 'export HOMEBREW_NO_ANALYTICS=1' >> ~/.bashrc
echo 'export HOMEBREW_NO_AUTO_UPDATE=1' >> ~/.bashrc

source ~/.bashrc

```

* Fix git

    https://wiki.vcu.edu/display/unix/Install+Linuxbrew+on+RHEL6+or+Centos6

```bash
export HOMEBREW_NO_ENV_FILTERING=1

brew install binutils linux-headers
brew install glibc --force-bottle
brew install gcc --force-bottle
brew install expat --force-bottle
brew install pcre2 --force-bottle
brew install openssl
brew install curl
brew install gettext --force-bottle
brew install pkgconfig --force-bottle
brew install gpatch --force-bottle
brew install ncurses --build-from-source
brew install pkg-config --force-bottle
brew install gettext --force-bottle
brew install git

unset HOMEBREW_NO_ENV_FILTERING
brew update

brew vendor-install ruby

```

* Test your installation:

```bash
brew install hello
brew test hello
brew remove hello
```

* ome packages have building problems, use bottled or from-source versions.

```bash
brew install gawk
brew install glib
brew install fontconfig
brew install cairo
brew install r
brew install graphviz
brew install imagemagick

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

# Sudo

```bash
usermod -aG wheel wangq
visudo
```
