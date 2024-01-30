## Ubuntu Git SSH Key

Check whether install Git

```cmd
git
```

Install Git

```cmd
sudo apt install git
```

Link Github account

```cmd
git config --global user.name proprozxy
git config --global user.email proprozxy@outlook.com
git config --list
```

Show all SSH

```cmd
ls -al ~/.ssh
```

Generate SSH key

```cmd
ssh-keygen -t -rsa -C "proprozxy@outlook.com"
```

Show public key

```cmd
cat ~/.ssh/id_rsa.pub
```

Login in GitHub

Settings - SSH and GPG keys - New SSH Key

Test connection

```cmd
ssh -T git@github.com
```

