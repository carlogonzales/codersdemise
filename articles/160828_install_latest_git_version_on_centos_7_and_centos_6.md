# Install Latest Git Version on Centos 7 and Centos 6 server

If you happen to download the minimal iso of centos on from it's website. You can get Git thru Centos' default repository but you're going to have an older version of Git. _(At the time of writing the default repo has Git version 1.8)_

### Getting Git thru Default Repo

```bash
yum install git
```

### Getting New Version of Git

#### Step 1

Install all required dependency to compile from source

```bash
yum groupinstall 'Development Tools'
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-ExtUtils-MakeMaker
yum install wget
```

#### Step 2

Download the tarbal from Git's Github repository. [Git Releases](https://github.com/git/git/releases)
At the time of writing the latest stable version is 2.9.3.

```bash
wget https://github.com/git/git/archive/v2.9.3.tar.gz
```

Extract the tarbal

```bash
tar -zxf v2.9.3.tar.gz
```

#### Step 3

Go to the extracted directory and compile the source.

```bash
cd git-2.9.3
make prefix=/usr/local/git all
make prefix=/usr/local/git install
echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/bashrc
source /etc/bashrc
```

#### Step 4

To verify the installation check the Git version

```bash
git --version
```
 
#### References

- [Install Git 2.0 on Centos, Rhel and Fedora](http://tecadmin.net/install-git-2-0-on-centos-rhel-fedora/)
- [Digital Ocean's - How to Install Git on Centos 7](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-centos-7)
