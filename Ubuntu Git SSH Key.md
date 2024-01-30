Ubuntu Git SSH Key

```cmd
git
```

```cmd
sudo apt install git
```

```cmd
git config --global user.name proprozxy
git config --global user.email proprozxy@outlook.com
git config --list
```

```cmd
ls -al ~/.ssh
```

```cmd
ssh-keygen -t -rsa -C "proprozxy@outlook.com"
```

```cmd
cat ~/.ssh/id_rsa.pub
```

Login in GitHub

Settings - SSH and GPG keys - New SSH Key

```cmd
ssh -T git@github.com
```

